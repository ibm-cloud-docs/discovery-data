---

copyright:
  years: 2019, 2021
lastupdated: "2022-05-19"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# API version comparison
{: #migrate-to-v2-api}

For most API methods, the request parameters and response bodies differ between v1 and v2. Learn about the equivalent or alternative v2 methods that you can use to do actions that are supported by the v1 API.

The comparison information assumes you are using the latest version of the v1 API (version `2019-04-30`) and compares it to the latest version of the v2 API (version `2020-08-30`).

## Environments
{: #migrate-to-v2-api-environments}

There is no concept of an *environment* in v2. The deployment details such as size and index capacity are managed based on the service plan type. In v2, collections are organized in projects. You can create different types of projects to apply default configuration settings to the collections that you add to the projects.

There are no equivalent methods in v2 for the v1 environment methods. However, the following table shows v2 methods that serve similar functions to the corresponding v1 methods. The supported parameters and response bodies that are returned for each method differ also.

| Action | v1 API | Related v2 API |
|--------|--------|----------------|
| Create an environment | [`POST /v1/environments`](/apidocs/discovery#createenvironment) | [`POST /v2/projects`](/apidocs/discovery-data#createproject) |
| List environments    | [`GET /v1/environments`](/apidocs/discovery#listenvironments) | [`GET /v2/projects`](/apidocs/discovery-data#listprojects) |
| Get environment info | [`GET /v1/environments/{environment_id}`](/apidocs/discovery#getenvironment) | [`GET /v2/projects/{project_id}`](/apidocs/discovery-data#getproject) |
| Update an environment | [`PUT /v1/environments/{environment_id}`](/apidocs/discovery#updateenvironment) | [`POST /v2/projects/{project_id}`](/apidocs/discovery-data#updateproject)  \n v2 uses `POST` instead of `PUT`. |
| Delete an environment | [`DELETE /v1/environment/{environment_id}`](/apidocs/discovery#deleteenvironment) | [`DELETE /v2/projects/{project_id}`](/apidocs/discovery-data#deleteproject) |
| List fields across collections | [`GET /v1/environments/{environment_id}/fields`](/apidocs/discovery#listfields) | [`GET /v2/projects/{project_id}/fields`](/apidocs/discovery-data#listfields) |
{: caption="Environment API action support details" caption-side="top"}

## Configurations
{: #migrate-to-v2-api-configurations}

The v2 API does not have an endpoint that is dedicated to configurations. Instead, configuration settings for projects, collections, and queries are specified directly in the API for those objects. Not all of the configuration parameters that are available in v1 are available or applicable in v2.

In the [v1 configuration API](/apidocs/discovery#createconfiguration), the JSON object that is used to specify a configuration object contains several parameters that are either available in different formats from other v2 endpoints or are not available in v2. The following table describes how to find related parameters in v2.

You cannot customize the conversion of documents during the ingestion process in v2 as you can in v1.

| v1 configuration parameter | v2 API |
|----------------------------|--------|
| `"conversions.html": { ... }` | Not available |
| `"conversions.image_text_recognition": { ... }` | Not available from the API. However, you can enable optical character recognition (OCR) for a collection from the product user interface to extract text from images. OCR has other benefits, too. For example, if a page in a document can't be processed, OCR converts the page into an image and scans it to ensure that the document is uploaded successfully.
| `"conversions.json_normalizations": { ... }` | Not available |
| `"conversions.pdf": { ... }` | Not available |
| `"conversions.segment": { ... }` | Not available programmatically. You can split a document at each occurrence of an SDU-generated field such as `subtitle` from the product user interface. You can also apply FAQ extraction to a collection from the product user interface in v2 to generate a separate question-and-answer document for each FAQ that is found in a single source document. |
| `"conversions.word": { ... }` | Not available |
| `"enrichments": { ... }` | [`/v2/projects/{project_id}/enrichments`](/apidocs/discovery-data#listenrichments), [`/v2/projects/{project_id}/collections/{collection_id}`](/apidocs/discovery-data#getcollection)  \n Use the enrichments API to explore existing enrichments. Use the collections API to see and change the enrichments that are enabled on a field in a collection.  \n Some enrichments are applied to the service by default based on the type of project that you create. For more details, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults). |
| `"normalizations": [ ... ]` | Not available |
| `"source": { ... }` | Not available. Configure connections to external data sources through the user interface. For more information, see [Creating collections](/docs/discovery-data?topic=discovery-data-collections). |
{: caption="Configuration setting details" caption-side="top"}

## Collections
{: #migrate-to-v2-api-collections}

| Action | v1 API | v2 API |
|--------|--------|--------|
| Create a collection | [`POST /v1/environments/{environment_id}/collections`](/apidocs/discovery#createcollection) | [`POST /v2/projects/{project_id}/collections`](/apidocs/discovery-data#createcollection)  \n The supported parameters and responses differ between the two versions. See the [collection notes](#migrate-to-v2-api-collection-notes). | 
| List collections | [`GET /v1/environments/{environment_id}/collections`](/apidocs/discovery#listcollections) | [`GET /v2/projects/{project_id}/collections`](/apidocs/discovery-data#listcollections)  \n In v2, only the collection ID and name of each collection are returned in the list. You must use the *Get collection* method to return more details about each collection. |
| Get collection details | [`GET /v1/environments/{environment_id}/collections/{collection_id}`](/apidocs/discovery#getcollection) | [`GET /v2/projects/{project_id}/collections/{collection_id}`](/apidocs/discovery-data#getcollection)  \n See the [collection notes](#migrate-to-v2-api-collection-notes). |
| Update a collection | [`PUT /v1/environments/{environment_id}/collections/{collection_id}`](/apidocs/discovery#updatecollection) | [`POST /v2/projects/{project_id}/collections/{collection_id}`](/apidocs/discovery-data#updatecollection)  |
| Delete a collection | [`DELETE /v1/environments/{environment_id}/collections/{collection_id}`](/apidocs/discovery#deletecollection) | [`DELETE /v2/projects/{project_id}/collections/{collection_id}`](/apidocs/discovery-data#deletecollection)  \n In v2, the `status` field is not returned in the response. |
| List collection fields | [GET /v1/environments/{environment_id}/collections/{collection_id}/fields](/apidocs/discovery#listcollectionfields)  \n v1 lists the fields per collection. | [GET /v2/projects/{project_id}/fields](/apidocs/discovery-data#listfields)  \n v2 lists fields per project instead. You can pass a single collection ID with the `collection_ids` parameter to get fields from a single collection. |
{: caption="Collections API support details" caption-side="top"}

### Collections API notes
{: #migrate-to-v2-api-collection-notes}

The following table shows the important differences between the v1 and v2 collection APIs.

| Method | Notes |
|--------|-------|
| Create a collection | The v2 response doesn't include the `status` and `configuration_id` fields. You can get status information for a specific document by using the [Get document details](/apidocs/discovery-data#getdocument) method.  \n The objects `disk_usage`, `training_status`, `crawl_status`, and `smart_document_understanding` are not present in the response body in v2. The `document_counts` object is not present in the response body in v2 currently. Training status is returned in the [Get project](/apidocs/discovery-data#getproject){: external} method response. The other information is not available in v2.  In v2, you can define the enrichments to apply to the documents in the collection by specifying an optional `enrichments` object. |
| Get collection details | The v2 response doesn't include the `status` and `configuration_id` fields. You can get status information for a specific document by using the [Get document details](/apidocs/discovery-data#getdocument) method.  \n The objects `document_counts`, `disk_usage`, `training_status`, `crawl_status`, and `smart_document_understanding` are not present in the response body in v2. Training status is returned in the *Get project* method response. The other information is not available in v2. For example, you cannot get the document count for a collection and cannot get the crawl status for a collection that connects to an external data source in v2. In v2, you can get information about the enrichments that are applied to the collection. |
| Update a collection | v2 uses `POST` instead of `PUT`. In v2, you can update the enrichments that are applied to the documents in the collection by specifying an optional `enrichments` object.  \n The v2 response doesn't include the `status` and `configuration_id` fields. |
{: caption="Collections API notes" caption-side="top"}

## Query modifications
{: #migrate-to-v2-api-query-modifications}

The methods that were available in v1 for configuring the query behavior programmatically are not supported in the v2 API currently. Some of the actions are available only from the v2 product user interface.

| v1 API | v2 product user interface |
|--------|--------|
| [Tokenization dictionary API](/apidocs/discovery#createtokenizationdictionary) | Not available from the v2 API or product user interface. |
| [Expansions API](/apidocs/discovery#listexpansions) | No API is available in v2 currently. To add or manage expansions, create synonyms in the v2 product user interface. For more information, see [Expanding the meaning of queries](/docs/discovery-data?topic=discovery-data-search-settings). |
| [Stopwords API](/apidocs/discovery#getstopwordliststatus) | No API is available in v2 currently. You can update stop words only from the v2 product user interface. For more information, see [Identifying words to ignore](/docs/discovery-data?topic=discovery-data-stopwords). |
{: caption="Query modifications API support details" caption-side="top"}

## Documents
{: #migrate-to-v2-api-documents}

| Action | v1 API | v2 API |
|--------|--------|--------|
| List documents | Not available from the v1 API | [GET /v2/projects/{project_id}/collections/{collection_id}/documents](/apidocs/discovery-data#listdocuments) |
| Create a document  | [`POST /v1/environments/{environment_id}/collections/{collection_id}/documents`](/apidocs/discovery#adddocument) | [`POST /v2/projects/{project_id}/collections/{collection_id}/documents`](/apidocs/discovery-data#adddocument)  \n Unlike v1, the v2 response does not include a notices object. However, you can get notices information by using the *Get document details* method in v2. |
| Update a document | [`POST /v1/environments/{environment_id}/collections /{collection_id}/documents/{document_id}`](/apidocs/discovery#updatedocument) | [`POST /v2/projects/{project_id}/collections/{collection_id}/documents/{document_id}`](/apidocs/discovery-data#updatedocument)  \n When you update a document that was split, all of the document segments are overwritten. |
| Get document details | [`GET /v1/environments/{environment_id}/collections /{collection_id}/documents/{document_id}`](/apidocs/discovery#getdocumentstatus) | [GET /v2/projects/{project_id}/collections/{collection_id}/documents/{document_id}](/apidocs/discovery-data#getdocument)  \n In v2, there is no `statusDescription`. v2 has a `children` object with information about any notices that are associated with the child documents that are generated during ingestion.|
| Delete a document | [`DELETE /v1/environments/{environment_id}/collections /{collection_id}/documents/{document_id}`](/apidocs/discovery#deletedocument) | [`DELETE /v2/projects/{project_id}/collections/{collection_id}/documents/{document_id}`](/apidocs/discovery-data#deletedocument)  \n Segments of an uploaded document cannot be deleted individually. Delete all segments with a DELETE request that includes the parent_document_id of a segment result. |
{: caption="Documents API support details" caption-side="top"}

v2 introduces a custom header that is named `X-Watson-Discovery-Force` that is not available in v1. You must include the header when you perform an operation on data that is shared across many collections to indicate that you want to perform the operation in each collection. If you do not include the header, a `403` error is returned.

## Queries
{: #migrate-to-v2-api-queries}

| Action | v1 API | v2 API |
|--------|--------|--------|
| Query a collection | Supports a GET or POST request.  \n [GET or POST /v1/environments/{environment_id}/collections/{collection_id}/query](/apidocs/discovery#queryusingget) | Queries a project. To specify a single collection, include the {collection_id} parameter. Supports a POST request only.  \n [POST /v2/projects/{project_id}/query](/apidocs/discovery-data#query) |
| Query multiple collections | [GET or POST /v1/environments/{environment_id}/query](/apidocs/discovery#federatedquery) | [POST /v2/projects/{project_id}/query](/apidocs/discovery-data#query) |
| Query system notices | [GET /v1/environments/{environment_id}/collections/{collection_id}/notices](/apidocs/discovery#querynotices) | [GET /v2/projects/{project_id}/collections/{collection_id}/notices](/apidocs/discovery-data#querycollectionnotices) |
| Query multiple collection system notices | [GET /v1/environments/{environment_id}/notices](/apidocs/discovery#federatedquerynotices) | [GET /v2/projects/{project_id}/notices](/apidocs/discovery-data#querynotices) |
| Get Autocomplete suggestions | [/v1/environments/{environment_id}/collections/{collection_id}/autocompletion](/apidocs/discovery#getautocompletion) | [GET /v2/projects/{project_id}/autocompletion](/apidocs/discovery-data#getautocompletion)  \n See the [query notes](#migrate-to-v2-api-queries-notes). |
{: caption="Documents API support details" caption-side="top"}

Some query result configurations are applied to the service by default based on the type of project that you create. For more details, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults).

### Query notes
{: #migrate-to-v2-api-queries-notes}

-   v2 queries return results from all of the collections in the project. To restrict the query to use only certain collections within the project, use the `collection_ids` query parameter. You cannot query multiple collections that are added to different projects with one v2 query request.
-   Use POST calls (instead of GET calls) to submit queries with v2.
-   v1 queries accept many parameters. The *Query parameters comparison* table maps v1 parameters to v2 parameters.

    | v1 parameter | v2 parameter | Notes
    |--------------|--------------|-------|
    | N/A | collection_ids | Use this parameter in v2 to specify collection ids. |
    | filter | filter | Same expression language. |
    | query | query | Same expression language. |
    | natural_language_query | natural_language_query | No notes. |
    | passages | passages | The passage format changed and was enhanced in v2. The `passages:true` parameter changed to `passages.enable:true`. In addition to the `count`, `characters`, and `fields` options, you can specify `per_document`, which ranks the documents by document quality, and then returns the highest-ranked passages per document. You can also specify `find_answers` to return an answer object per passage, which contains a succinct answer to the query. |
    | aggregation | aggregation | Same expression language. |
    | count  | count | No notes. |
    | offset | offset | No notes. |
    | return | return | No notes. |
    | sort | sort | No notes. |
    | highlight | highlight | If `passages.enabled` and `passages.per_document` are `true`, then passages are returned for each document instead of highlights. |
    | spelling_suggestions | spelling_suggestions | No notes. |
    | deduplicate | **N/A** | Not supported in v2. |
    | similar     | **N/A** | Not supported in v2. |
    | bias        | **N/A** | Not supported in v2. |
    {: caption="Query parameters comparison" caption-side="top"}

## Training data
{: #migrate-to-v2-api-trainingd-data}

You can use the v1 training data API to work with two related objects: 

-   trained queries
-   examples that are used to train the queries

These two objects have separate API endpoints in v1. In v2, the examples that are used to train each query are provided together with the query and only one top-level endpoint is used to work with the training data. 

For example, to add a trained query and its training example documents in v2, you use the request `POST /v2/projects/{project_id}/training_data/queries` and pass the query and all examples in the payload of one call. Similarly, if you want to update one example in the training set in v2, you must pass the query and the modified example (along with all of the other examples) to the v2 update endpoint. In v1, to update the example information, you use the update example endpoint to modify one example only.

Another important difference between v1 and v2 is that in v1, the trained model is associated with a particular collection. In v2, the trained model is associated with a project. You can use the data from multiple collections within a project to train a relevancy model. When you create or update training examples in v2, the API requires the `collection_id` for the collection where the document is stored.

| Action | v1 API | v2 API |
|--------|--------|--------|
| List training data | [`GET /v1/environments/{environment_id}/collections/{collection_id}/training_data`](/apidocs/discovery#listtrainingdata) | [`GET /v2/projects/{project_id}/training_data /queries`](/apidocs/discovery-data#listtrainingqueries) |
| Add query to training data | [`POST /v1/environments/{environment_id}/collections/{collection_id}/training_data`](/apidocs/discovery#addtrainingdata) | [`POST /v2/projects/{project_id}/training_data /queries`](/apidocs/discovery-data#createtrainingquery) |
| Delete all training data | [`DELETE /v1/environments/{environment_id}/collections/{collection_id}/training_data`](/apidocs/discovery#deletealltrainingdata) | [`DELETE /v2/projects/{project_id}/training_data /queries`](/apidocs/discovery-data#deletetrainingqueries) |
| Get details about a query | [`GET /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}`](/apidocs/discovery#gettrainingdata) | [`GET /v2/projects/{project_id}/training_data /queries/{query_id}`](/apidocs/discovery-data#gettrainingquery) |
| Delete a training data query | [`DELETE /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}`](/apidocs/discovery#deletetrainingdata) | [`DELETE /v2/projects/{project_id}/training_data /queries/{query_id}`](/apidocs/discovery-data#deletetrainingquery) |
| List examples for a training data query | [`GET /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}/examples`](/apidocs/discovery#listtrainingexamples) | [`GET /v2/projects/{project_id}/training_data /queries/{query_id}`](/apidocs/discovery-data#gettrainingquery)  \n The examples are in the list that is returned with the query. |
| Add example to training data query | [`POST /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}/examples`](/apidocs/discovery#createtrainingexample) | [`POST /v2/projects/{project_id}/training_data /queries/{query_id}`](/apidocs/discovery-data#updatetrainingquery)  \n Use the *Create training query* method in v2 and pass all examples when you create the query. Otherwise, use the update API. |
| Delete example for training data query | [`DELETE /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}/examples/{example_id}`](/apidocs/discovery#deletetrainingexample) | [`POST /v2/projects/{project_id}/training_data/ queries/{query_id}`](/apidocs/discovery-data#updatetrainingquery)  \n Use the v2 training_data update method. |
| Change label or cross-reference for example | [`PUT /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}/examples/{example_id}`](/apidocs/discovery#updatetrainingexample) | [`POST /v2/projects/{project_id}/training_data/ queries/{query_id}`](/apidocs/discovery-data#updatetrainingquery)  \n Use the v2 training_data update method. |
| Get details for a training data example | [`GET /v1/environments/{environment_id}/collections/{collection_id}/training_data/{query_id}/examples/{example_id}`](/apidocs/discovery#gettrainingexample) | Not available. Use the Read all examples call to get all examples associated with a query and find the example that you need in the returned list. |
{: caption="Training data API support details" caption-side="top"}

## User data
{: #migrate-to-v2-api-user-data}

The user data API is the same in v2 and v1.

| Action | v1 API | v2 API |
|--------|--------|--------|
| Delete | [`DELETE /v1/user_data`](/apidocs/discovery#deleteuserdata) | [`DELETE /v2/user_data`](/apidocs/discovery-data#deleteuserdata)  \n Similar to v1. Use `customer_id` to delete the data associated with that customer ID. |
{: caption="User data API support details" caption-side="top"}

## Events and feedback
{: #migrate-to-v2-api-events}

The v1 events and feedback API (`/v1/events`) is not available in v2.

## Credentials
{: #migrate-to-v2-api-credentials}

The v1 credentials API (`/v1/environments/{environment_id}/credentials`) is not available in v2. The function is available from the v2 product user interface.

## Gateway configuration
{: #migrate-to-v2-api-gateway-configuration}

The v1 gateways API (`/v1/environments/{environment_id}/gateways`) is not available in v2. The function is available from the v2 product user interface. For more information, see [Installing IBM Secure Gateway for on-premises data](/docs/discovery-data?topic=discovery-data-sources#gatewaypublic).

## Status codes
{: #migrate-to-v2-api-status-codes}

For almost every API method, the status codes that are returned for v2 requests are different from the status codes that are returned for v1 requests.