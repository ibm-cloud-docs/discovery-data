---

copyright:
  years: 2019, 2023
lastupdated: "2022-09-30"

subcollection: discovery-data

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting {{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}} deployments
{: #troubleshoot}

Learn ways to troubleshoot and address issues that you might encounter while using the product.
{: shortdesc}

![{{site.data.keyword.cpd_full_notm}} only](images/desktop.png) **{{site.data.keyword.cpd_full_notm}} only** 

This information applies only to instances of {{site.data.keyword.discoveryfull}} that are installed on {{site.data.keyword.icp4dfull}}. For troubleshooting tips about adding data to both installed and managed deployments, see [Troubleshooting ingestion](/docs/discovery-data?topic=discovery-data-troubleshoot-ingestion).
{: note}

The information in this topic suggests steps you can take to investigate issues that might occur. For information about known issues and their workarounds per version, see [Known issues](/docs/discovery-data?topic=discovery-data-known-issues).

## Minio pods enter a reboot loop during installation or upgrade
{: #ts-minio-loop}
{: troubleshoot}
<!-- disco support 1566-->

-   **Error**: `Cannot find volume "export" to mount into container "ibm-minio"` is displayed during an installation or upgrade of {{site.data.keyword.discoveryshort}}. When you check the status of the Minio pods by using the command, `oc get pods -l release=wd-minio -o wide`, and then check the `Minio operator` logs by using the commands, `oc get pods -A | grep ibm-minio-operator`, and then `oc logs -n <namespace> ibm-minio-operator-XXXXX`, you see an error similar to the following one in the logs:

    ```text
    ibm-minio/templates/minio-create-bucket-job.yaml failed: jobs.batch "wd-minio-discovery-create-bucket" already exists) and failed rollback: failed to replace object"
    ```
    {: codeblock}

-   **Cause**: A job that creates a storage bucket for Minio and then is deleted after it completes, is not being deleted properly.
-   **Solution**: Complete the following steps to check whether an incomplete `create-bucket` job for Minio exists. If so, delete the incomplete job so that the job can be recreated and can then run successfully.

    1.  Check for the Minio job by using the following command:

        ```bash
        oc get jobs | grep 'wd-minio-discovery-create-bucket'
        ```
        {: codeblock}

    1.  If an existing job is listed in the response, delete the job by using the following command:

        ```bash
        oc delete job $(oc get jobs -oname | grep 'wd-minio-discovery-create-bucket')
        ```
        {: codeblock}

    1.  Verify that all of the Minio pods start successfully by using the following command:

        ```bash
        oc get pods -l release=wd-minio -o wide
        ```
        {: codeblock}

## A `No space left on device` message is displayed in the log
{: #ts-no-space}
{: troubleshoot}

If the a `wd-ibm-elasticsearch-es-server-client` pod restarts repeatedly and then reports the `Crashloopbackoff` state with the message `No space left on device` written to the log for the pod, then the issue might be a lack of memory on the pod. Follow the steps to [troubleshoot out of memory issues](#ts-oom) or contact IBM Support.

## A `java.lang.OutOfMemoryError: Java heap space` message is displayed in the log
{: #ts-oom}
{: troubleshoot}

When indexing a large set of documents that have multiple enrichments applied to them, the worker node can run out of space. To address the issue, first determine which pod is out of memory by completing the following steps:

If the document status cannot be promoted to `Processing`, check the status of the `inlet`, `outlet`, and `converter` pods.

1.  Run the following command:

    ```sh
    oc get pod -l 'tenant=wd,run in (inlet,outlet,converter)'
    ```
    {: pre}

1.  If any of the pods are not showing a `Running` status, restart the failing pod by using the following command:

    ```sh
    oc delete pod <pod_name>
    ```
    {: pre}

1.  Otherwise, open the *Manage collections*>*{collection name}*>*Activity* page. Check the *Warnings and errors at a glance* section for the message, `OutOfMemory happened during conversion. Please reconsider size of documents.` If shown, use the following command to raise the memory size for the converter:

    ```sh
    oc patch wd wd --type=merge \
    --patch='{"spec":{"ingestion":{"converter":b{"maxHeapMemory":"10240m","resources":{"limits":{"memory":"10Gi"}}}}}}'
    ```
    {: pre}

    Adjust the value of `maxHeapMemory` and the container memory according to your cluster resources.
    {: note}

1.  After the `converter` pod restarts successfully, click **Reprocess** from the Activity tab.

If documents are stuck in `Processing` status and cannot be promoted to the `Available` status for a collection, complete the following steps:

1.  Check the status of Hadoop by using the following command:

    ```sh
    oc get pod -l 'tenant=wd,run in (hdp-rm,hdp-worker)'
    ```
    {: pre}

    where `l` is a lowercase L for list.

1.  If any of the pods are not showing a `Running` status, restart the failing pod by using the following command:

    ```sh
    oc delete pod <pod_name>
    ```
    {: pre}

1.  Check whether any of the Hadoop worker nodes has insufficient memory by using the following command to look for the `OOM when allocating` message:

    ```sh
    oc logs -l tenant=wd,run=hdp-worker -c logger --tail=-1 \
    | grep "OOM when allocating"
    ```
    {: pre}

1.  If a match is found, use the following command to patch the resource:

    ```sh
    oc patch wd wd --type=merge \
    --patch='{"spec":{"orchestrator":{"docproc":{"pythonAnalyzerMaxMemory":"8g"}}}}'
    ```
    {: pre}

    The maximum allowed value for `pythonAnalyzerMaxMemory` is `12g`. The default value is `6g`. Increase the value gradually, such as in increments of 2g at a time according to your cluster resources.
    {: note}

1.  Check whether any of the Hadoop worker nodes has insufficient memory by using the following command to look for the `OutOfMemoryError` message:

    ```sh
    oc logs -l tenant=wd,run=hdp-worker -c logger --tail=-1 \
    | grep "OutOfMemoryError"
    ```
    {: pre}

1.  If a match is found, check the current environment variable values and the Hadoop worker node memory resources by using following commands:

    -   To check the `"DOCPROC_MAX_MEMORY"` variable in the orchestrator container:

        ```sh
        oc exec `oc get po -l run=orchestrator -o 'jsonpath={.items[0].metadata.name}'` env \
        | grep DOCPROC_MAX_MEMORY
        ```
        {: pre}

    -   To check the `"YARN_NODEMANAGER_RESOURCE_MEMORY_MB"` variable in the Hadoop worker node container:

        ```sh
        oc exec `oc get po -lrun=hdp-worker -o 'jsonpath={.items[0].metadata.name}'` \
        -c hdp-worker -- env | grep YARN_NODEMANAGER_RESOURCE_MEMORY_MB
        ```
        {: pre}

    -   To check the memory resource of the `hdp-worker` container:

        ```sh
        oc get po -l run=hdp-worker -o 'jsonpath=requests are \
        {.items[*].spec.containers[?(.name=="hdp-worker")].resources.requests.memory}, \
        limits are {.items[*].spec.containers[?(.name=="hdp-worker")].resources.limits.memory}'
        ```
        {: pre}

1.  Patch the environment variable resources gradually by using the following command:

    ```sh
    oc patch wd `oc get wd -o 'jsonpath={.items[0].metadata.name}'` \
    --type=merge --patch='{"spec":{"orchestrator":{"docproc":{"maxMemory":"4g"}}, \
    "hdp":{"worker":{"nm":{"memoryMB":12000}, "resources":{"limits":{"memory":"20Gi"}, \
    "requests":{"memory":"20Gi"}}}}}}'
    ```
    {: pre}

    The default values for the resources are as follows:

    -   `docproc.maxMemory`: 2g 

        Increase in increments of 2g at a time.
    -   `nm.memoryMB`: 10,240 

        Start from 12,000 and increase in increments of 2,000 at a time.
    -   `memory requests/limits`: 13Gi/18Gi 

        Increase in increments of 2Gi at a time.

1.  Check whether the Hadoop pods restart successfully by using the following command:

    ```sh
    oc get pods -l 'tenant=wd,run in (orchestrator,hdp-worker)'
    ```
    {: pre}

1.  Confirm that the new configurations were applied after you patched the cluster.

1.  If the pod is not restarted, check whether the resource got updated by using the following command:

    ```sh
    oc get wd wd -o yaml
    ```
    {: pre}

1.  Check the status of Elasticsearch by checking the client and data nodes separately.

1.  On the client node, run the following command to check whether an out-of-memory exception occurred:

    ```sh
    oc logs -l tenant=wd,ibm-es-data=False,ibm-es-master=False \
    -c elasticsearch --tail=-1 | grep "OutOfMemoryError"
    ```
    {: pre}

1.  If an error message is found, excluding INFO messages, increase the memory resource by using the following command:

    ```sh
    oc patch wd wd --type=merge \
    --patch='{"spec":{"elasticsearch":{"clientNode":{"maxHeap":"896m","resources":{"limits":{"memory":"1792Mi"}}}}}}'
    ```
    {: pre}

1.  After you run this command, the Elasticsearch client pod is restarted about 20 minutes later. Monitor the "AGE" of the pod by using the following command:

    ```sh
    oc get pod -l tenant=wd,ibm-es-data=False,ibm-es-master=False
    ```
    {: pre}

1.  After the pod is restarted successfully, check the new value of `ES_JAVA_OPTS` and the container memory limit by using the following command:

    ```sh
    oc describe $(oc get po -l tenant=wd,ibm-es-data=False,ibm-es-master=False -o name)
    ```
    {: pre}

1.  On the data node, run the following command to check whether an out-of-memory exception occurred:

    ```sh
    oc logs -l tenant=wd,ibm-es-data=True,ibm-es-master=False \
    -c elasticsearch --tail=-1 | grep "OutOfMemoryError"
    ```
    {: pre}

1.  If an error message is found, excluding INFO messages, increase the memory resource by using the following command:

    ```sh
    oc patch wd wd --type=merge \
    --patch='{"spec":{"elasticsearch":{"dataNode":{"maxHeap":"6g","resources":{"limits":{"memory":"10Gi"},"requests":{"memory":"8Gi"}}}}}}'
    ```
    {: pre}

1.  After you run this command, the Elasticsearch client pod is restarted about 20 minutes later. Monitor the "AGE" of the pod by using the following command:

    ```sh
    oc get pod -l tenant=wd,ibm-es-data=True,ibm-es-master=False
    ```
    {: pre}

1.  After the pod is restarted successfully, check the new value of `ES_JAVA_OPTS` and the container memory requests/limit by using the following command:

    ```sh
    oc describe $(oc get po -l tenant=wd,ibm-es-data=True,ibm-es-master=False -o name)
    ```
    {: pre}

    For both nodes (client and data), set the `resources.limits.memory` equal to `2 * maxHeap`.
    {: note}

    If the pod cannot be restarted after 30 mins by applying the `oc patch` command, collect logs to share with IBM Support by using the following command:

    ```sh
    oc logs -l control-plane=ibm-es-controller-manager --tail=-1
    ```
    {: pre}

For both issues, where document status cannot be promoted to `Processing` and where documents are stuck in `Processing` status, if you are using Portworx storage, you can check whether the Elasticsearch disk is full.

1.  Run the following command to check whether the Elasticsearch disk is full:

    ```sh
    oc logs -l tenant=wd,run=elastic,ibm-es-master=True \
    -c elasticsearch --tail=100000|grep 'disk watermark'
    ```
    {: pre}

1.  If the log shows a message such as `watermark exceeded on x-data-1`, it means the disk on the node that is specified is full and you need to increase the disk size by using the following command:

    ```sh
    oc patch pvc $(oc get pvc -l tenant=wd,run=elastic,ibm-es-data=True,ibm-es-master=False \
    -o jsonpath='{.items[N].metadata.name}') \
    -p '{"spec": {"resources": {"requests":{"storage": "60Gi"}}}}'
    ```
    {: pre}

    where `N` denotes the data node number that was reported from the log.

    For example, if the log mentions `data-1` in the node name, then the command to use is:

    ```sh
    oc patch pvc $(oc get pvc -l tenant=wd,run=elastic,ibm-es-data=True,ibm-es-master=False \
    -o jsonpath='{.items[1].metadata.name}') -p '{"spec": {"resources": {"requests":{"storage": "60Gi"}}}}'
    ```
    {: pre}

## Setting the shard limit in Discovery for Cloud Pak for Data
{: #shard-limit}
{: troubleshoot}

In {{site.data.keyword.discoveryshort}} version 2.2.0, there is a limit to the number of shards that can stay open on a cluster. In development instances, the limit is 1,000 open shards, and in production instances, the limit is two data nodes, which is equal to 2,000 open shards, or 1,000 open shards per data node. After you reach either limit, you cannot create any more projects and collections on your cluster, and if you try to create a new project and collection, you receive an error message.

This limit is due to the fact that, when you install {{site.data.keyword.discoveryshort}} version 2.2.0, Elasticsearch version 7.8.0 automatically runs on your clusters. Because this version of Elasticsearch runs on your clusters, a new cluster stability configuration becomes available that limits the number of open shards to 1,000 for each Elasticsearch data node.

If you are unable to create new projects and collections and you receive errors, first check the status of your Elasticsearch cluster and the number of shards on that cluster. Consider increasing the number of data nodes on your cluster to support more shards. This method is optimal for maximizing performance. However, an increased number of nodes uses more memory. If the number of shards reaches the limit, you can also increase the limit in a data node. For more information about increasing the shard limit in a node, see [Increasing the shard limit](/docs/discovery-data?topic=discovery-data-troubleshoot#increase-shards).

This limit of 1,000 shards does not apply to versions of {{site.data.keyword.discoveryshort}} that are earlier than 2.2.0.
{: note}

### Increasing the shard limit
{: #increase-shards}

1.  Log in to your {{site.data.keyword.discoveryshort}} cluster.
1.  Access your data node.
1.  Enter the following command:

    ```sh
    oc exec -it $(oc get pod \
    -l app=elastic,ibm-es-data=True -o jsonpath='{.items[0].metadata.name}') -- bash
    ```
    {: pre}

1.  Enter the following command, replacing the `<>` and the content inside with your port number:

    ```sh
    curl -X POST http://localhost:<port_number>/_cluster/health?pretty
    ```
    {: pre}

    If you do not know what your port number is, enter the following command to find it:

    ```sh
    oc get pod -l app=elastic,ibm-es-data=True -o json \
    | jq .items[].spec.containers[].ports[0].containerPort | head -n 1`
    ```
    {: pre}

    The curl `POST` command returns a value for `active_primary_shards`. If you have one data node that has a value larger than 1,000 or if you have two data nodes that have a value larger than 2,000, you must increase the shard limit to create new projects and collections in your cluster.

    If you increase this limit, the cluster becomes less stable because it contains an increased number of shards.
    {: important}

1.  Enter the following command to increase the number of shards, replacing `<port_number>` with your port number and `<total_shards_per_node>` and `<max_shards_per_node>` with the new shard limit that you want to assign to a node:

    ```sh
    curl -X POST http://localhost:<port_number>/_cluster/settings \
    -d '{"persistent": {"cluster.routing.allocation.total_shards_per_node":<total_shards_per_node>, \
    "cluster.max_shards_per_node":<max_shards_per_node>} }' \
    -XPUT -H 'Content-Type:application/json'
    ```
    {: pre}

    After you increase the shard limit, you can create more projects and collections on your cluster.

## Clearing a lock state
{: #troubleshoot-ls}
{: troubleshoot}

![Cloud Pak for Data only](images/desktop.png) **Installed only**: When the `gateway` pod restarts, it runs a database validation plug-in that checks for changes and applies the latest change sets to the shared database. If the pod is restarted while this check is in process, the plug-in might remain in a lock state, preventing the service from starting. Manual database intervention might be needed to clear the lock.

If the Discovery API does not come online or if the `gateway-0` pod looks like it is in a constant crash loop, you can try checking the Liberty server logs for the API service located here: `/opt/ibm/wlp/output/wdapi/logs/messages.log`

The logs would indicate if Liquibase is failing and unable to run. If the system is locked, you might see something similar to the following:

```text
[11/7/19 5:07:51:491 UTC] 0000002f liquibase.executor.jvm.JdbcExecutor I SELECT LOCKED FROM public.databasechangeloglock WHERE ID=1
[11/7/19 5:07:51:593 UTC] 0000002f liquibase.lockservice.StandardLockService I Waiting for changelog lock....
[11/7/19 5:08:01:601 UTC] 0000002f liquibase.executor.jvm.JdbcExecutor I SELECT LOCKED FROM public.databasechangeloglock WHERE ID=1
[11/7/19 5:08:02:091 UTC] 0000002f liquibase.lockservice.StandardLockService I Waiting for changelog lock....
[11/7/19 5:08:12:097 UTC] 0000002f liquibase.executor.jvm.JdbcExecutor I SELECT LOCKED FROM public.databasechangeloglock WHERE ID=1
[11/7/19 5:08:12:197 UTC] 0000002f liquibase.lockservice.StandardLockService I Waiting for changelog lock....
[11/7/19 5:08:22:203 UTC] 0000002f liquibase.executor.jvm.JdbcExecutor I SELECT ID,LOCKED,LOCKGRANTED,LOCKEDBY FROM public.databasechangeloglock WHERE ID=1
[11/7/19 5:08:22:613 UTC] 0000002f com.ibm.ws.logging.internal.impl.IncidentImpl I FFDC1015I: An FFDC Incident has been created: "org.jboss.weld.exceptions.DeploymentException: WELD-000049: Unable to invoke public void liquibase.integration.cdi.CDILiquibase.onStartup() on liquibase.integration.cdi.CDILiquibase@7f02a07 com.ibm.ws.container.service.state.internal.ApplicationStateManager 31" at ffdc\_19.11.07\_05.08.22.0.log
```

It is possible to manually unlock the plug-in. If you have {{site.data.keyword.discoveryshort}} 2.1.4 or earlier, enter the following command on the postgres database that the `gateway-0` pod is looking at:

```sh
psql dadmin
UPDATE DATABASECHANGELOGLOCK SET LOCKED=FALSE, LOCKGRANTED=null, LOCKEDBY=null where ID=1;
```
{: pre}

If you have {{site.data.keyword.discoveryshort}} 2.2.0 or later, enter the following command on the postgres database that the `gateway-0` pod is looking at:

```sh
oc exec -it wd-discovery-postgres-0 -- bash -c 'env PGPASSWORD="$PG_PASSWORD" psql "postgresql://$PG_USER@$STKEEPER_CLUSTER_NAME-proxy-service:$STKEEPER_PG_PORT/dadmin" -c "UPDATE DATABASECHANGELOGLOCK SET LOCKE
D=FALSE, LOCKGRANTED=null, LOCKEDBY=null where ID=1"'
```
{: pre}

If you can then restart the `gateway` pod, everything should resume normally.

## Environment variable settings for Smart Document Understanding
{: #troubleshoot-sdu}
{: troubleshoot}

There are two environment variables that need to be adjusted for Smart Document Understanding in {{site.data.keyword.discoveryfull}} version 2.1.0. This was resolved in version 2.1.1, see [2.1.1 release, 24 Jan 2020](/docs/discovery-data?topic=discovery-data-release-notes#24jan2020).

```sh
SDU_PYTHON_REST_RESPONSE_TIMEOUT_MS
SDU_YOLO_TIMEOUT_SEC
```
{: pre}

Both of these should be set to their respective `hour` value. These values must be set in the `<release-name>-watson-discovery-hdp` ConfigMap.

The values should be:

`SDU_PYTHON_REST_RESPONSE_TIMEOUT_MS` should be set to `3600000`

`SDU_YOLO_TIMEOUT_SEC` should be set to `3600`

These values should be set when the software is installed or reinstalled.

## Troubleshooting error messages
{: #troubleshoot-errors}

If you receive error messages that are related to timeouts and insufficient memory for your enrichments, you can enter the following commands to change timeout and memory settings to potentially resolve these error messages:

-   Notice message: `<enrichment_name>: Document enrichment timed out`

    Suggested action: Increase the document processing timeout. Enter the following command to increase the default timeout from 10 to 20 minutes:

    ```sh
    oc patch wd wd --type=merge \
    --patch='{"spec": {"orchestrator": {"docproc": {"defaultTimeoutSeconds": 1200 } } } }'
    ```
    {: pre}

-   Notice message: `<enrichment_name>: Document enrichment failed due to lack of memory`

    Suggested action: Increase the orchestrator container memory limit. Enter the following command to increase the memory limit from 4 Gi to 6 Gi:

    ```sh
    oc patch wd wd --type=merge \
    --patch='{"spec": {"orchestrator": {"resources": {"limits": {"memory": "6Gi"} } } } }'
    ```
    {: pre}

-   Notice messsage: `Indexing request timed out`

    Suggested action: Increase the timeout for pushing documents to Elasticsearch. Enter the following command to increase the default timeout from 10 to 20 minutes:

    ```sh
    oc patch wd wd --type=merge \
    --patch='{"spec": {"shared": {"elastic": {"publishTimeoutSeconds": 1200 } } } }'
    ```
    {: pre}
