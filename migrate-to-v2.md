---

copyright:
  years: 2019, 2021
lastupdated: "2022-07-28"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Migrating to Discovery v2
{: #migrate-to-v2}

A redesign of the product, Discovery v2, was introduced in November 2019. Discovery v2 offers significant advantages over Discovery v1.
{: shortdesc}

The information in this topic describes how to migrate a v1 Discovery service instance to Discovery v2, including how to move data and update your applications.

The major structural differences between Discovery v1 and v2 include:

- There is no concept of an environment in v2. The deployment details such as size and index capacity are managed for you when you choose the appropriate service plan for your needs. For managed deployments, you can choose a Plus, Enterprise, or Premium plan, for example. For installed deployments, the sizing is managed by the deployment type that you specify when you install the service in Cloud Pak for Data.
- There is no single configuration object in v2. Control of the enrichments that are applied to documents is managed in the collections and project objects in v2. Other v1 configuration capabilities, such as the ability to customize the conversion step of ingestion, are not available in v2.
- Greater programmatic support is available for custom enrichments in v2. New enrichment API methods are available that you can use to create enrichments. v2 also introduces document classifier API methods that you can use to train document classifier models programatically. You can subsequently apply these custom enrichments to a collection by using the API.
- The capabilities of a natural language query search are expanded in v2 to enable the return of the top passages per document and of succinct answers from passages. Other advanced search capabilities are introduced, including table retrieval. In v2, the deduplication parameter is not available and the continuous relevancy training and query logging functions are not available.

-  For more information about feature differences, see [the feature comparison table](/docs/discovery-data?topic=discovery-data-version-choose#version-choose-comparison).
-  For more information about detailed API differences, see [API version comparison](/docs/discovery-data?topic=discovery-data-migrate-to-v2-api).

Discovery v2 is available for all users of Plus or Enterprise plan instances, or Premium plan instances that were created after 15 July 2020. v2 is also available for {{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}} users.

## Migration overview
{: #migrate-to-v2-overview}

Migrating from Discovery v1 to v2 is a multistep process that you can do independently.

The two versions of the {{site.data.keyword.discoveryshort}} service have many differences, but you can adopt techniques and utilities that were applied to a v1 instance for use with your new v2 instance.

To migrate from v1 to v2, you must complete the following high-level steps:

1.	[Plan the migration](#migrate-to-v2-plans).
1.	[Transfer your documents](#migrate-to-v2-docs).
1.	[Update your application to use the v2 API](#migrate-to-v2-difs).
1.  Regression test and deploy the updated application.

Some steps require you to make programmatic changes by using the API and others involve changes that you can make from the product user interface.
{: note}

## Plan the migration
{: #migrate-to-v2-plans}

Get familiar with what's new in v2 and learn about how it differs from v1 before you provision a v2 instance. Your first v2 Plus plan trial instance is available at no charge for 30 days. Learn about and plan for the migration before you provision the instance so that you can get the most from your free trial.

When you're ready to start the migration, create a migration schedule that you and your team can follow as you complete the process. Be sure to set up the new v2 service instance and get projects and collections recreated in the new service instance before you switch over to using the v2 service and before you delete your v1 instance.

Learn about the Discovery v2 plan options, so you can choose the right plan for your long term needs. The Plus plan that you use to get started might be sufficient. However, you might choose to use an Enterprise or Premium plan instead. From a Plus plan, you can do an in-place upgrade to an Enterprise plan, but not to a Premium plan.

### Plan how to adapt your application
{: #migrate-to-v2-projects}

One of the main changes between versions is that Discovery v2 introduces projects. A project consists of one or more collections. The advantage of using projects is that one query can run against many collections at the same time. Each collection can contain documents that you upload or that you crawl from a single data source, such as a website, Microsoft SharePoint, and more.

Things to consider when you adapt your application to use projects:

-   Although the concept of an environment does not exist in v2, data is still organized into collections. In v2, collections are grouped into projects. In most cases, you will want to migrate a single v1 collection to a single v2 collection.

    If you want to keep relevancy training information that is applied to a v1 collection, add the collection documents to a single collection in your v2 project.

-   Decide how many collections you want to add to each v2 project. All project types, except Content Mining projects, can contain up to 5 collections. Choose the right type of project for your data. 

    To optimize search results, different enrichments and configuration options are applied automatically to collections that are added to different project types. For more information, see the following topics:

    -   [Project descriptions](/docs/discovery-data?topic=discovery-data-projects#project-descriptions)
    -   [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults)
    -   [Default query settings](/docs/discovery-data?topic=discovery-data-query-defaults)

-   The Discovery v2 API changed to account for projects and collections, among other enhancements. Some API calls changed to support actions at the project level instead of the collection level, such as submitting a query and running relevancy training. Many other API methods changed and some are not available in v2. For a detailed comparison of the v1 and v2 API methods, see [API version comparison](/docs/discovery-data?topic=discovery-data-migrate-to-v2-api).

### Picking a service plan
{: #migrate-to-v2-plan-overview}

Choose among the *Plus*, *Enterprise*, and *Premium* managed plans or opt for an on-premises installation by purchasing the {{site.data.keyword.discoveryshort}} Cartridge for {{site.data.keyword.icp4dfull_notm}}. Review the benefits and limits of each type of plan before you choose one.

-   For more information about the plans, see [Discovery pricing plans](/docs/discovery-data?topic=discovery-data-pricing-plans).
-   For more information about artifact limits, see [Limit details](/docs/discovery-data?topic=discovery-data-version-choose#plan-limit-links).

The following table shows plan types for managed deployments that are generally similar between v1 and v2.

| Current v1 plan | Example v1 data usage | Similar v2 plan | 
|-----------------|-----------------------|---------------------|
| Lite | Not applicable | Plus Trial (no charge for 30 days only) |
| Advanced (low usage) | 10,000 documents, 10,000 queries per month  | Plus |
| Advanced (high usage) | 100,000 documents, 100,000 queries per month | Enterprise |
| Premium | Not applicable | Enterprise or Premium |
{: caption="Similar plans" caption-side="top"}

To get information about the current storage, documents, and collections used, click the *Environment details* icon from the product user interface header.
{: tip}

You cannot do an in-place upgrade from a v1 plan, such as Lite or Advanced, to a v2 plan. You must create a new v2 plan, and then move your data to the new service instance. While you migrate your data from v1 to v2, you will likely have both a v1 and v2 instance deployed at the same time. Consider leveraging the 30-day no charge trial that is available with your first Plus plan instance during this time.

## Collecting metrics 
{: #migrate-to-v2-metrics}

Make a note of the following information so you can compare it to your service instance data after the migration:

-   Number of collections

    To get the number of collections in an instance in v1, use the [List collections](https://cloud.ibm.com/apidocs/discovery#listcollections) API.

-   Number of documents per collection

    To get the number of documents in a collection in v1, use the [Get collection details](https://cloud.ibm.com/apidocs/discovery#getcollection) API. 
    
    ```sh
    GET {url}/v1/environment/{environment_id}/collections/{collection_id}`
    ```
    {: codeblock}
    
    The API returns information about the status of the documents in the collection, which includes the total number of available documents.

    ```json
    "document_counts": {
        "available": 34,
        "{other}":"{values...}"
    }
    ```
    {: codeblock}

## Transferring documents from v1 to v2
{: #migrate-to-v2-docs}

How you transfer your documents depends on the technique that was used to ingest the documents in v1.

Recreate one collection at a time. If you start multiple ingestion processes at once, you can tax the system resources and increase the overall time it takes for the processing to be completed. You also want to keep an eye out for any informational messages that are generated by the ingestion process. It is easier to troubleshoot an ingestion issue, for example, when you ingest one collection at a time.

### Uploaded data
{: #docs-uploaded}

If you used the API to upload documents into Discovery v1, a similar API is available in v2 to upload documents into collections. You must update any workflows you use to automate the process to account for the new arrangement of projects and collections.

If the original documents that you ingested into Discovery v1 are no longer available, you can use the query API to extract the document text from Discovery v1. You can then add the text to a collection in Discovery v2. For more information, see [Recovering documents](#migrate-to-v2-advanced-transfer).

### Crawled data
{: #docs-crawled}

If you crawled data from an external data source in v1, you can continue to crawl data from the same external data source in v2. All of the same data sources are supported.

To use data from an external data source, you must re-create the collections within a v2 project, and configure how the data source is crawled. For more information, see [Overview of data sources](/docs/discovery-data?topic=discovery-data-sources).

The service needs time and resources to crawl and ingest documents from external data sources. Re-create the connectors one at a time. Factor the time it will take to recrawl the data into your migration plan schedule.

### Prebuilt data collections
{: #docs-prebuilt-collections}

The following built-in data source collections are not available in v2:

Watson Discovery News
:   This pre-enriched data source is not offered in v2. For more information about an alternative way to get news data, see [Using a news service with v2](#migrate-to-v2-news).

COVID-19 kit
:   This pre-built collection was designed to help you fuel a dynamic chatbot that is built with IBM Watson™ Assistant and Discovery to answer your customers' questions about COVID-19. In v2, you can build a similar solution. Create a *Conversational Search* project type with collections that crawl trusted websites for answers to COVID-19 questions. For more information, see the [Helping your chatbot get answers from existing help content](/docs/discovery-data?topic=discovery-data-tutorial-convo) tutorial.

## Ingesting data
{: #migrate-to-v2-ingest}

To ingest v1 data into a Discovery v2 instance, complete the following steps:

1.  Create a v2 service instance.
1.  Create a project.
1.  Add a collection to the project. 

    -   Uploaded data: 
    
        From the API, you create a collection and add documents to it with two separate methods. Use the [Create a collection](/apidocs/discovery-data#createcollection){: external} method to create the collection. Next, add the same source documents that you added to your v1 collection to the v2 collection. Use the [Add document](/apidocs/discovery-data#adddocument){: external} or [Update document](/apidocs/discovery-data#updatedocument){: external} methods. To assign the same v1 document ID to the document as you add it to the v2 collection, append the document ID to the endpoint. For more information, see [Retaining document IDs](#migrate-to-v2-keep-docid).
    
        From the v2 product user interface, upload the same source documents that you added to your v1 collection to the v2 collection.
    
    -   Crawled data: You cannot crawl data from an external data source programmatically in v2. From the product user interface, re-create the connection to the external data source, and then crawl the external data source from scratch.

1.  From the product user interface, you can configure the Discovery v2 collection. For example, you can choose whether to enable optical character recognition or FAQ extraction. For an external data source, you can set the crawl schedule.
1.  Apply enrichments to your data. You can apply pre-built Natural Language Processing enrichments or custom enrichments that you create.

    In v1, enrichments are associated with the configuration that is generated when you create the environment. In v2, enrichments are associate with the collection configuration. Some enrichments are applied to your collection by default, depending on the type of project used. For more information, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults). In v2, you can configure the collection to use any subset of available enrichments on the fields of your document.

### Retaining document IDs
{: #migrate-to-v2-keep-docid}

Document IDs are assigned to the documents that you add to a v2 collection when you upload them from the product user interface or add them by using the [Add a document](/apidocs/discovery-data#adddocument) API method.

You might want to retain the IDs of your v1 documents in v2 if you are using processes that depend on these unique identifiers. For example, regression testing for the application might verify specific documents are returned by checking the document IDs. Relevancy training uses the document IDs to track documents between training runs. These processes are easier to adapt if the document IDs are the same between your v1 and v2 instances. Otherwise, the processes that are used with the Discovery v1 instance must be remapped to the IDs that are assigned to the documents after they are added to the Discovery v2 instance.

If you specified your own documents IDs when you added documents to the v1 service instance, you can retain the IDs by using the *Update a document* method instead of the *Add a document* method. With the update method, you can assign a document ID to the document as you add it to the v2 collection. For more information, see [Update a document](/apidocs/discovery-data#updatedocument){: external}.

If your data is stored in a JSON file, an array in the original document generates a document ID with a number appended to it. For example, `original_id_n`. To retain the original document ID without the number suffix, remove the array in the JSON file. Change `[ {"name": "value"} ]` to `{"name": "value"}`, for example.
{: note}

If your v1 documents have system-generated IDs, you can submit an empty [search query](https://cloud.ibm.com/apidocs/discovery#query) to retrieve a list of the documents and their IDs. You can then assign the same ID to each document as you add it to your new collection in v2.

### Recovering documents
{: #migrate-to-v2-advanced-transfer}

In some cases, the original documents that were ingested into Discovery V1 are no longer available. You can use the Discovery v1 instance to retrieve information from the document. Discovery creates a text copy of each document that it ingests. The copy is text only, so any documents in HTML, PDF, or other nontext formats are converted to a text-only version.

You can recover only the first 10,000 documents in a collection by using this method.
{: important}

To transfer document information from v1 to v2, complete the following steps:

1.  Extract the documents from v1 by using the API to [submit an empty query](https://cloud.ibm.com/apidocs/discovery#query).

    For example, `GET {url}/v1/environment/{environment_id}/collections/{collection_id}/query?q=`.

    The API returns the results. the `matching_results` field specifies the total number of results. The results object returns the matching documents. Each document is returned as a separate JSON object. It returns a maximum of 10 documents by default.

    ```json
    {
      "matching_results": 34,
      "session_token": "nnn",
      "results": [
        {"{result objects}":"{maximum of 10 by default}"}
      ]
    }
    ```
    {: codeblock}

1.  You can use the `count` and `offset` parameters to page through the query results and save all of the documents. 

    For example, to get 100 documents at a time, you can set the `count` to `100` and `offset` to `0` and submit the query.

    ```sh
    GET {url}/v1/environment/{environment_id}/collections/{collection_id}/query?q=&count=100&offset=0
    ```
    {: codeblock}

    Next, you can again set the count to 100, but this time set the offset to 100 to get the next 100 documents.

    ```sh
    GET {url}/v1/environment/{environment_id}/collections/{collection_id}/query?q=&count=100&offset=100`
    ```
    {: codeblock}

    Repeat this process, incrementing the offset by 100, until you retrieve all of the documents.
    
1.  Prepare the exported documents to be ingested into v2.

    Each resulting JSON file that you get from Discovery v1 contains data that is extracted from the original document, such as text, html, and other fields. If custom metadata was associated with the document when it was uploaded to v1, it is also present in the JSON file. In addition, the file contains several fields that were generated by the v1 analysis. Retain only a subset of this data as part of the document that you add to Discovery v2. 
    
    The following tips can help you decide which fields to keep:

    -   Include the `text` field or any other field with textual content that you want to be able to enrich or search in Disocvery v2.
    -   Include any custom metadata that is stored in the document. This metatdata is typically specific to the application that leverages Discovery and is used to filter documents in a search. For example, `metadata.customer_id`.
    -   Do not include enrichments from Discovery v1. For example, `enriched_text.entities`. Discovery v2 generates its own enrichments.
    -   Exclude fields that are generated by Discovery unless they are leveraged by your application and contain information that is unique to the v1 version of the document. In that case, rename the field so that it does not get replaced when the document is ingested into Discovery v2. For example, `extracted_metadata.publicationdate` is a field that is generated by Discovery when a document is ingested. Maybe you want to retain the `metadata.parent_document_id` information from v1 to understand how subdocuments were originally generated from a single source document.
    -   Avoid fields that have reserved field names. For more information, see [How fields are handled](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-index-overview#field-name-limits).

1.  Ingest each edited v1 JSON document into the Discovery v2 instance. The Discovery v1 document ID can be maintained in Discovery v2. For more information about how to retain the document ID, see [Retaining document IDs](#migrate-to-v2-keep-docid).

## Transferring relevancy training
{: #migrate-to-v2-transfer-relevance}

Relevancy training that was done in Discovery v1 can be transferred to Discovery v2. Transferring the training works best with a Discovery v2 project that has one collection that contains the same documents from the Discovery v1 collection.

Even if collections were added or documents changed, the relevancy training can be transferred. However, you must update the training to account for the changes.

To transfer relevancy training, complete the following steps:

1.  Load the documents in Discovery v2.
1.  Programmatically download the queries that were used for relevancy training in Discovery v1. For more information, see [List training data](https://cloud.ibm.com/apidocs/discovery#listtrainingdata){: external}.
1.  Programmatically re-create the relevancy training data in Discovery v2. Add each training query separately by using the *Create a query* method. For more information, see [Create a training query](https://cloud.ibm.com/apidocs/discovery-data#createtrainingquery){: external}.

    Be sure to specify the v2 collection ID. You must also specify the document ID also. 
    
    If you did not [retain the document IDs](#migrate-to-v2-keep-docid) between the v1 and v2 collections, then you must find the v2 document ID that corresponds to the v1 document ID that is referenced in the downloaded query example.
    {: note}

## Transferring models
{: #migrate-to-v2-models}

You can reuse some of the models that you created in v1 with your v2 project.

SDU models
:   You can use an SDU model that you built in v1. However, you cannot edit the migrated SDU model in v2. If you want to reuse a model as-is, you can [export it from v1](/docs/discovery?topic=discovery-sdu#import){: external} and [import the SDU model](/docs/discovery-data?topic=discovery-data-configuring-fields#import) to v2.

Machine learning models
:   You can import machine learning models that you create and export from Watson Knowledge Studio. The model must have been exported from Knowledge Studio after 16 July 2020. If you have a model that was exported before that date, you must re-export the model from Watson Knowledge Studio. Only paid Knowledge Studio plans support exporting models. 

    For more information, see one of the following topics:
    
    -   **{{site.data.keyword.icp4dfull}}**: [Exporting a machine learning model](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-publish-ml#exporting-a-machine-learning-model){: external}

    -   **{{site.data.keyword.cloud_notm}}**: [Deploying a machine learning model to Watson Discovery](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-publish-ml#wks_madiscovery){: external}
    
    For information about how to import a model to Discovery v2, see [Importing Machine Learning models](/docs/discovery-data?topic=discovery-data-domain-ml).

## Update your application to use the v2 API
{: #migrate-to-v2-difs}

The Watson Developer SDKs support both Discovery v1 and v2.

These instructions assume that your application is using the latest version of the v1 API (version `2019-04-30`).

When you port an application that currently uses the Discovery v1 API to use v2, you must plan how to address the following high-level differences between the two versions. 

In addition to these high-level changes, review the differences at a per-method level to understand what else you might need to change. For more information, see [API version comparison](/docs/discovery-data?topic=discovery-data-migrate-to-v2-api).

-   v2 organizes data by project and collections; there is no concept of an environment. For example, compare the following requests to get a collection:

    v1 [Get collection](https://cloud.ibm.com/apidocs/discovery#getcollection){: external}

    ```sh
    GET {url}/v1/environments/{environment_id}/collections/{collection_id}
    ```
    {: codeblock}

    v2 [Get collection](https://cloud.ibm.com/apidocs/discovery-data#getcollection){: external}

    ```sh
    GET {url}/v2/projects/{project_id}/collections/{collection_id}
    ```
    {: codeblock}

-   In v1, relevancy training runs on a single collection. In v2, relevancy training runs on a project. The project might contain many collections. If so, relevancy training is applied across all of the collections. For information about how to transfer relevancy training, see [Transferring relevancy training](#migrate-to-v2-transfer-relevance).

    For example, compare the following requests that return the status of relevancy training:

    v1 [Get collection](https://cloud.ibm.com/apidocs/discovery#getcollection){: external}

    ```sh
    GET {url}/v1/environments/{environment_id}/collections/{collection_id}
    ```
    {: codeblock}

    v2 [Get project](https://cloud.ibm.com/apidocs/discovery-data#getproject){: external}

    ```sh
    GET {url}/v2/projects/{project_id}
    ```
    {: codeblock}

-   Submitting a query is similar between the two versions. In v2, you can query all of the collections in a project or you can limit the query to one or more collections by specifying a `collection_ids` parameter. For example, compare the following requests to query data:

    v1 [Query](https://cloud.ibm.com/apidocs/discovery#query){: external} request

    ```sh
    POST {url}/v1/environments/{environment_id}/collections/{collection_id}/query
    ```
    {: codeblock}

    Data that is submitted with the request:

    ```json
    {
      "query": "text:IBM"
    }
    ```
    {: codeblock}

    v2 [Query](https://cloud.ibm.com/apidocs/discovery-data#query){: external} request

    ```sh
    POST {url}/v2/projects/{project_id}/query
    ```
    {: codeblock}

    Data that is submitted with the request:

    ```json
    {
      "collection_ids": [
        "{collection_id_1}",
        "{collection_id_2}"
      ],
      "query": "text:IBM"
    }
    ```
    {: codeblock}

    You can optionally omit the `collection_ids` parameter to query across all of the collections in the project.

-   The `passage` parameter for a query has a new `per_document` option that ranks the documents by document quality, and then returns the highest-ranked passages per document in a `document_passages` field for each document entry in the results list of the response. If false, ranks the passages from all of the documents by passage quality regardless of the document quality and returns them in a separate passages field in the response.

-   When passages are returned for a query, you can also enable answer finding. When true, answer objects are returned as part of each passage in the query results. When `find_answers` and `per_document` are both set to true, the document search results and the passage search results within each document are reordered using the answer confidences. The goal of this reordering is to place the best answer as the first answer of the first passage of the first document. Similarly, if the `find_answers` parameter is set to true and per_document parameter is set to false, then the passage search results are reordered in decreasing order of the highest confidence answer for each document and passage.

### Update how your application handles query results
{: #migrate-to-v2-result-difs}

The way that your application shows query results might need to be updated due to the following differences between the query results document syntax between the v1 and v2 queries:

-   At the entity enrichment level, the following information is not supported in v2:

    -   Sentiment
    -   Disambiguation

    The *Part of Speech* enrichment is applied automatically to documents in most project types in v2, but the index fields that are generated by the enrichment are not displayed in the JSON representation of the document.

    ![Difference in entities data structure](/images/compare-result-syntax.png)

-   Instead of the `count` and `relevance` in v1, v2 includes the mentions. 

    Each entry in the mention corresponds to an occurrence of the entity in the document text. In the following example, seven occurrences are found. For each occurrence, a confidence score and the offsets of the mention text are displayed. You can use the offsets to highlight the mention in the document text when the result is displayed in a user interface.

    ![Mentions in Discovery v2](/images/result-detail.png)

-   The JSON structure of query responses is rearranged slightly in v2.
-   Deduplication information is not included in the v2 query response.
-   In v2, `enriched_text` is an array instead of an object.
-   In Discovery v2, the Entities v2 enrichment is used. Entity type names in v2 are specified in headline case, instead of all uppercase letters. If you use a query or aggregation that specifies an entity name, you must change the capitalization. For example, change `PERSON` to `Person`.
-   Fields from JSON files that are added to a collection are converted differently during ingestion between v1 and v2. If your application manipulates these results, you might need to make adjustments.

    | Original JSON field content | v1 representation | v2 representation | Notes |
    |-----------------------------|-------------------|-------------------|-------|
    | `"field": null` | `"field": null` | N/A | v1 retains the null value. v2 skips the null field altogether. |
    | `"field": ""` | `"field": ""` |  N/A  | v1 retains the empty text value. v2 skips the empty text field altogether. |
    | `"field": "value2"` | `"field": "value2"` | `"field": "value2"` | No difference. |
    | `"field": []` | `"field": []` | N/A | v1 retains the empty array. v2 skips the field with the empty array altogether. |
    | `"field": [ "value4" ]` | `"field": [ "value4" ]` | `"field": "value4"` | v1 retains the singleton array. v2 converts the singleton array into the value only; it is not stored as part of an array. |
    | `"field": [ 1, 2, 3 ]` | `"field": [ 1, 2, 3 ]` | `"field": [ 1, 2, 3 ]` | No difference. |
    | `"field": [ "v6", "v7", "v8" ]` | `"field": [ "v6", "v7", "v8"]` | `"field": [ "v6", "v7", "v8"]` | No difference. |
    {: caption="How JSON source fields are handled" caption-side="top"}

## Verifying that your data was migrated successfully
{: #migrate-to-v2-verify}

To verify that the migration was successful, compare the following metrics to the [metrics that you noted before the migration](#migrate-to-v2-metrics).

-   Number of collections

    Be sure to recreate all of the collections that you used in v1 and want to keep. With the v2 [List collections](https://cloud.ibm.com/apidocs/discovery-data#listcollections) API method, you can get a list of collections, but you must submit a request per project. You cannot use one call to get the total number of collections per service instance.

-   Number of documents per collection

    For collections with uploaded data, check the number of documents in the collection by sending an empty query with the [Query a project](https://cloud.ibm.com/apidocs/discovery-data#query) API method. Specify the collection ID parameter to limit the results to only documents in one collection. An empty query returns all documents. Therefore, you can get the total number of documents from the `matching_results` value in the response.

    The number of documents per collection should be close to the number of documents that were stored in the same collection in v1. The numbers might not be exactly the same. 
    
    For crawled data, do not be surprised if the v2 collection has fewer documents. The v1 connectors do not delete documents from a Discovery collection that are deleted from the external data source. Your v2 version of the collection will be a fresher crawl of the data as it exists in the external data source today.

Do not expect the search results to be exactly the same for queries that you submit in the v1 and v2 instances.
{: tip}

## Using a news service with v2
{: #migrate-to-v2-news}

If you used the Watson Discovery News data source in v1 and want to create a data source with equivalent function in v2, consider using the Webz.io News API. You can use the Webz.io News API to extract news articles in JSON format, and then upload the JSON files to create a News collection in your v2 project.
 
To figure out how many API calls you need to make to Webz.io, determine the number of news documents that you're currently retrieving from Watson Discovery News per month. One document in Discovery News is equivalent to one article (JSON object) from the Webz.io News API. A single Webz.io News API call returns approximately 100 news articles. Therefore, if you're using 50,000 Discovery News documents per month, you need to make approximately 500 Webz.io News API calls per month (50,000/100 = 500). For more information, see [Webz.io News API](https://webz.io/data-apis/news-api){: external}.
