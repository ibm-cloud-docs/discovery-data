---

copyright:
  years: 2019, 2024
lastupdated: "2024-02-28"

keywords: external-enrichment,webhook

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Document status webhook API
{: #document-status-api}

[IBM Cloud]{: tag-ibm-cloud}

The document status webhook API is beta functionality that is only available from the API. This feature is available only from service instances that are managed by IBM Cloud.
{: beta}

You can use the document status webhook feature to send a webhook event to your external application when the status of ingested documents becomes `available` or `failed`. The webhook event helps you to take the next action on indexed documents, without having to get the document status first through the [Get document details API](https://{DomainName}/apidocs/discovery-data#getdocument){: external}.

For using the document status webhook feature, do the following things:

1.  Set up the external application that can receive webhook notifications from {{site.data.keyword.discoveryshort}}.

    To do so, you must register your external application as a webhook endpoint on a collection by using the `create collection` or `update collection` API methods. For more information, see [Create collection](https://{DomainName}/apidocs/discovery-data#createcollection){: external} or [update collection](https://{DomainName}/apidocs/discovery-data#updatecollection){: external} in the API reference.
    
    The external application receives a webhook `ping` event, which notifies that the webhook is sucessfully created. The external application must be accessible from IBM Cloud.

1.  Ingest the documents to the collection. When the status of the ingested documents becomes `available` or `failed`, the external application receives the `document.status`  webhook event.

    You can verify the status of the ingested documents in the `data` object of the `document.status` webhook event. The `document_ids` and `status` parameters show the IDs of the ingested documents and their status. For more information, see [Data model of the `ping` event](#ping-event) and [Data model of the `document.status` event](#ocument.status-event).

The following image shows the webhook configuration flow.

![Shows the document status webhook feature configuration flow](images/webhook-conf-flow.png){: caption="Figure 1. Document status webhook feature configuration flow" caption-side="bottom"}

The following image shows the document status webhook feature process flow.

![Shows the document status webhook feature process flow](images/webhook-process-flow.png){: caption="Figure 2. Document status webhook feature process flow" caption-side="bottom"}

For more information about the query API, see [Query a project API method](https://{DomainName}/apidocs/discovery-data#query){: external} in the API reference.

You can also refer to the webhook-doc-status-sample application for the document status webhook API feature. To view the sample application, you must have access to the Discovery [doc-tutorial-downloads](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/webhook-doc-status-sample){: external} repository.

## Webhook security
{: #webhook-security}

To authenticate the webhook request, verify the JSON Web Token (JWT) that is sent with the request. The webhook microservice automatically generates a JWT and sends it in the `Authorization` header with each webhook call. It is your responsibility to add code to the external service that verifies the JWT.

For example, if you specify `sample secret` in the `Secret` field of the Webhooks object in the [Create collection](https://{DomainName}/apidocs/discovery-data#createcollection){: external} or [update collection](https://{DomainName}/apidocs/discovery-data#updatecollection){: external} APIs, you might add sample code such as the following in Node.js:

```sh
const jwt = require('jsonwebtoken');
...
const token = request.headers.authentication; // grab the "Authentication" header
try {
  const decoded = jwt.verify(token, 'sample secret');
} catch(err) {
  // error thrown if token is invalid
}
```
{: codeblock}

## Data model of the `ping` event
{: #ping-event}

Following are the `ping` event parameters:

| Parameter | Description |
|-----------|----------------------|
| `event` | The event name is `ping`. |
| `instance_id` | The {{site.data.keyword.discoveryshort}} instance ID. |
| `version` | The {{site.data.keyword.discoveryshort}} API version in the format `yyyy-mm-dd`. |
| `data` | An object with the event information: `url`, `events`, and `metadata`.  \n  \n  - `url`: The configured webhook endpoint (URL).  \n  \n  - `events`: An array of event string values. The events in this array are sent to the webhook URL.  \n  \n  - `metadata`: An object with information that is specific to the created webhook.|
| `created_at` | The date and time the event was created. |
{: caption="Ping event" caption-side="top"}

For example, following is a `ping` event that is sent to a webhook:

```sh
POST https://example.com/webhook

Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l
X-Global-Transaction-ID: 5144bb45-dc81-402c-a045-249fd1318515
Content-Type: application/json
{
  "event": "ping",
  "version": "2023-03-31",
  "instance_id": "1a5d4916-6097-4150-977a-ca897226565c",
  "data": {
    "url": "https://example.com/webhook",
    "events": [
      "document.status"
    ],
    "metadata": {
      "project_id": "02a803f9-c814-4fcb-a764-e01e3d4dd002",
      "collection_id": "f41ae858-0ca9-d0ed-0000-01890118cc5b"
    }
  },
  "created_at": "2023-08-16T08:34:46.000Z"
}
```
{: codeblock}

## Data model of the `document.status` event
{: #document.status-event}

Following are the `document.status` event parameters:

| Parameter | Description |
|-----------|----------------------|
| `event` | The event name is `document.status`. |
| `instance_id` | The {{site.data.keyword.discoveryshort}} instance ID. |
| `version` | The {{site.data.keyword.discoveryshort}} API version in the format `yyyy-mm-dd`. |
| `data` | An object with the event specific information: `project_id`, `collection_id`, and `document_ids`. |
| `status` | The status of the documents. |
| `created_at` | The date and time the event was created. |
{: caption=" Document.status event" caption-side="top"}

For example, following is a `document.status` event that is sent to a webhook:

```sh
POST https://example.com/webhook

Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l
X-Global-Transaction-ID: 5144bb45-dc81-402c-a045-249fd1318515
Content-Type: application/json
{ 
  "event": "document.status",
  "version": "2023-03-31",
  "instance_id": "1a5d4916-6097-4150-977a-ca897226565c",
  "data": {
    "project_id": "02a803f9-c814-4fcb-a764-e01e3d4dd002",
    "collection_id": "f41ae858-0ca9-d0ed-0000-01890118cc5b",
    "document_ids": [
      "1a5d4916-6097-4150-977a-ca897226565b",
      "2a5d4916-6097-4150-977a-ca897226565b"
    ],
    "status": "available"
  },
  "created_at": "2023-08-16T08:34:46.000Z"
}
```
{: codeblock}
