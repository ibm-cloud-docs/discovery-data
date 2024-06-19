---

copyright:
  years: 2019, 2023
lastupdated: "2023-06-26"

keywords: ingestion performance

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Sizing the deployment for ingestion
{: #size-cp4d}

When you deploy {{site.data.keyword.discoveryshort}}, the default deployment configuration requests a set of resources from the {{site.data.keyword.icp4dfull_notm}} cluster, such as cores and memory, that are sufficient for using the product in many scenarios. Learn about changes you can make to the configuration to help speed up the ingestion of larger collections and those with different enrichment needs.
{: shortdesc}

As your collections grow in size or as the complexity of the operations that you want to apply to them increases, you can allocate more resources to improve the response time of the service.

In some cases, you can improve the ingestion performance without having to change the deployment configuration. For example, you can add data into separate collections in the same project in parallel. Discovery attempts to process data in different collections at the same time. Dividing the documents into separate collections does not limit your ability to query the data later. Remember, data in collections that are created in the same project can be queried at the same time. However, often the best way to improve performance requires updates to the deployment configuration. 

You can make configuration changes by applying a patch to the custom resource for the service. For more information, see [Scaling Watson Discovery](https://www.ibm.com/docs/SSQNUZ_4.6.x/svc-discovery/discovery-admin-scale.html){: external} in the {{site.data.keyword.icp4dfull_notm}} product documentation.

The best configuration to use for optimal ingestion performance in your deployment depends on the types of documents in your data set and the enrichments that are being applied to them.

## General processing enhancements
{: #size-cp4d-scenario1}

The following adjustments reduce the amount of time it takes to load and start processing documents by boosting the overall throughput for collections with many documents.

These settings are optimal when no enrichments are applied to the documents. However, different project types apply different enrichments to their collections automatically. Only *Custom* project types apply no enrichments by default. For adjustments to make to collections where enrichments are applied, see [Improving enrichment processing](#size-cp4d-enrichment).

Try the following adjustments for collections with 20,000 or more documents:

-   Increase the memory limit and sharedBuffer size of the PostgreSQL pod.
-   Double the size of the Java Heap size, memory, and CPU limits for the Gateway pod.
-   Double the memory limit and Java Heap size of the ingestion-api container of the Ingestion API pod.
-   Double the Java Heap size and increase the CPU and memory limits by 4 times for the ingestion container of the Ingestion API pod.

| Pod | CR setting | Value |
|-----|----------------------|------------|
| PostgreSQL | postgres.database.resources.limits.memory | 8 Gi |
| PostgreSQL | postgres.database.sharedBuffer  | 2,048 MB |
| Gateway | api.api.resources.limits.cpu | 4 |
| Gateway | api.api.resources.limits.memory | 2 Gi |
| Gateway | api.api.wlpMaxHeap | 1,024 MB |
| IngestionAPI | coreapi.ingestionApi.resources.limits.memory | 4 Gi |
| IngestionAPI | coreapi.wlpMaxHeap | 2,048 MB |
| IngestionAPI | coreapi.ingestionApi.ingestion.resources.limits.cpu | "2" |
| IngestionAPI | coreapi.ingestionApi.ingestion.resources.limits.memory | 4 Gi |
{: caption="Table 1. Configuration parameters for best ingestion performance" caption-side="top"}

The following YAML excerpt shows a sample custom resource patch file that applies these changes:

```yaml
cat <<EOF | oc patch wd wd --type=merge --patch -
spec:
  api:
    api:
      wlpMaxHeap: 1024m
      resources:
        limits:
          memory: 2Gi
          cpu: "4"
  coreapi:
    ingestionApi:
      wlpMaxHeap: 2048m
      resources:
        limits:
          memory: 2Gi
      ingestion:
        resources:
          limits:
            cpu: "2"
            memory: 4Gi
  postgres:
    database:
      resources:
        limits:
          memory: 8Gi
      sharedBuffer: 2048MB
EOF
```
{: codeblock}

## Improving enrichment processing
{: #size-cp4d-enrichment}

When enrichments are applied to a collection, more resources are needed to process the documents. Some project types apply enrichments to their collections automatically. If you create a *Document Retrieval* project type, for example, the *Part of Speech* and *Entities* enrichments are applied to the collections.

The default configuration for {{site.data.keyword.discoveryshort}} uses one *hdp-worker* pod per collection to process enrichments. When you ingest data into separate collections, each collection is processed in parallel. Increasing the number of hdp-worker pods allows for more collections to be processed at the same time. However, if you are adding documents to only one collection, or need the processing of enrichments per collection to go faster, increasing the number of hdp-worker pods will not improve performance. Instead, you must change the `docproc job number` parameter value. 

To increases the number of enrichment jobs that run on the same hdp-worker pod at the same time, increase the `docproc job number` parameter value. Be careful when you change the `docproc job number` value. Increase the value slowly, and check its impact. For example, increase the value from 1 to 2, and then watch for potential memory issues in the pods. If no issues arise, you then can increase the value in increments of 2. Again, watch for potential problems after each change. If ingestion starts to fail for some documents due to a lack of memory, you can either decrease the value of the `docproc job number` parameter or increase the value of the `hdp-worker memory` parameter.

The results from the worker pod are sent to the Elasticsearch service pod for indexing. When you increase the parallelism of enrichment processing, more documents are sent to the indexer pod at the same time. Therefore, you might need to increase the size of the indexer pods to handle the higher volume.

You can try the following adjustments in addition to the general processing enhancement settings to optimize ingestion for collections where enrichments are applied:

-  Double the Java Docproc job max memory size and indexing document batch sizes.
-  Increase the Docproc job number that can be executed for each collection.
-  Double the Java Heap size, memory, and cpu limits and replicas of the indexer pod.
-  Double the Java Heap size, memory, and cpu limits and replicas of the Elasticsearch Data Node pod.

| Pod | Configuration setting | Value |
|-----|-----------------------|-------|
| HDP worker | hdp.worker.replicas | 6 |
| HDP worker | hdp.worker.resources.limits.cpu | "16" |
| HDP worker | hdp.worker.resources.limits.memory | 36 Gi |
| Orchestrator | orchestrator.docproc.maxMemory | 4 g |
| Orchestrator | orchestrator.esPublishBatchSize | 400 |
| Orchestrator | orchestrator.esPublishDataSizeThreshold | "20" |
| Orchestrator | orchestrator.docproc.pythonAnalyzerMaxMemory | 10 |
| Indexer | foundation.indexer.replicas | 4 |
| Indexer | foundation.indexer.resources.limits.cpu | 2 |
| Indexer | foundation.indexer.resources.limits.memory | 8 Gi |
| Indexer | foundation.indexer.javaOptions | "-Xmx4096m -Xms512m" |
| ES Data | elasticsearch.dataNode.replicas | 4 |
| ES Data | elasticsearch.clientNode.dataNode.resources.limits.cpu | "4" |
| ES Data | elasticsearch.clientNode.dataNode.resources.limits.memory | 16 Gi|
| ES Data | elasticsearch.clientNode.dataNode.maxHeap | 8 g|
{: caption="Configuration parameters for enriched documents" caption-side="top"}

The following YAML excerpt shows a sample custom resource patch file that applies these changes:

```yaml
cat <<EOF | oc patch wd wd --type=merge --patch -
spec:
  postgres:
    database:
      resources:
        limits:                               
          memory: 8Gi                         
      sharedBuffer: 2048MB                    
  hdp:
    worker:
      replicas: 6                             
      resources:
        limits:
          cpu: "16"                           
          memory: 36Gi                        
        requests:
          cpu: "6"                            
          memory: 24Gi                        
  orchestrator:
    esPublishBatchSize: 400                   
    esPublishDataSizeThreshold: "20"          
    docproc:
      maxMemory: 4g                           
      workerNum: "10"                         
  foundation:
    indexer:
      replicas: 4                             
      javaOptions: "-Xmx4096m -Xms512m"       
      resources:
        limits:
          cpu: "2"                            
          memory: 8Gi                         
  elasticsearch:
    dataNode:
      replicas: 4
      maxHeap: 8g
      resources:
        limits:
          cpu: "4"
          memory: 16Gi
EOF
```
{: codeblock}

## Improving Smart Document Understanding processing
{: #size-cp4d-sdu}

When a Smart Document Understanding (SDU) model is applied to a collection, other additional resources are needed to process the documents. Some project types apply an SDU model to their collections automatically. If you create a *Document Retrieval for Contracts* project type, for example, the SDU enrichment is applied to the collections.

If a user-trained or the pretrained Smart Document Understanding (SDU) model is applied to a large collection, you can increase the number of hdp-worker pods to reduce the time it takes to process the documents. The hdp-worker pods need a large number of cores and memory to start. Be sure to check the number of replicas that are requested against the size and number of the worker nodes that are available in your cluster to be sure you have enough nodes to handle the demand.

Try the following adjustments for collections with SDU models applied to them:

- Increase the number of hdp-worker replicas in increments of 2. For example, go from 4 to 6, and then watch for issues.

| Pod | Configuration setting | Value |
|-----|-----------------------|-------|
| HDP worker | hdp.worker.replicas | 6 |
{: caption="Configuration parameters for annotated documents" caption-side="top"}

## Improving image processing
{: #size-cp4d-ocr}

Enabling optical character recognition (OCR) for your collection is an expensive operation. Only apply OCR to your collections if you know that the regions of interest in your document are in images. If your document contains no images or if the images are mostly stylistic in nature, they are logos or pictures with no relevant text, for example, disable OCR on the collection.
