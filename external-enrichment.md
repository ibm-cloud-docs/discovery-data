---

copyright:
  years: 2019, 2025
lastupdated: "2024-06-10"

keywords: external-enrichment,webhook

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Using the External enrichment API
{: #external-enrichment}

The external enrichment feature is not supported in the Analyze API.
{: note}

The external enrichment feature allows you to annotate documents with a model of your choice. Through a webhook interface, you can use custom models or advanced foundation models, and other third-party models for enriching your documents in a collection. The documents are enriched by your external application and then merged to a collection in a Discovery project.

[IBM Cloud Pak for Data]{: tag-cp4d} When you run {{site.data.keyword.discoveryshort}} in an air-gapped environment, you must connect to the external application through an HTTP proxy. For more information, see [Setting up HTTP proxy in air-gapped environments](/docs/discovery-data?topic=discovery-data-collection-types#sethttpproxyae).
{: note}

For using the external enrichment feature, do the following things:

1.  Set up the external application that can receive webhook notifications from Discovery and annotate documents.

    To do so, you must register your external app as a webhook endpoint on a project by using the `create enrichment` method. For more information, see [Create enrichment](https://{DomainName}/apidocs/discovery-data#createenrichment){: external} in the API reference.
    
    After setting up the external enrichment for a project, it becomes available to all collections in the project. The external application also receives a webhook `ping` event, which notifies that an external enrichment is created.

1.  Specify the collection in which you want to apply the external enrichment. You can use the API to apply the external enrichment to a collection. For more information, see [Using the API to manage enrichments](/docs/discovery-data?topic=discovery-data-manage-enrichments#enrichments-api).

    Alternatively, on the user interface, you can browse to the *Manage collections* page, and choose the collection where you want to apply the external enrichment. Then, open the **Enrichments** tab, and apply your external enrichment to a field in the collection.

    When documents are processed or uploaded to this collection, Discovery creates a batch of documents with a unique `batch_id`. The external application also receives a webhook `enrichment.batch.created` event, which notifies that batches are ready to be pulled. Your external application can then pull batches from Discovery for external enrichment. 

    If the external application shuts down or restarts in between, you can get the following by using the List batches method:

    - Notified batches that are not yet pulled by the external enrichment application.
    - Batches that are pulled, but not yet pushed to Discovery by the external enrichment application.

    For more information, see [List batches](https://{DomainName}/apidocs/discovery-data#listbatches){: external} in the API reference.

1.  Specify the `batch_id` provided by Discovery in the `pull batches` method to pull the documents from Discovery for enrichment by your external application. For more information, see [Pull batches](https://{DomainName}/apidocs/discovery-data#pullbatches){: external} in the API reference.

    The `pull batches` method returns a binary file attachment from Discovery. For more information about the binary attachment, see [Binary attachment from the pull batches method](#binary-attachment-pull-batches).

1.  Specify the same `batch_id` in the `push batches` method after your external enrichment annotates the documents in the batch. For more information, see [Push batches](https://{DomainName}/apidocs/discovery-data#pushbatches){: external} in the API reference.

    The documents are pushed to Discovery as a binary attachment. For more information, see [Binary attachment in the push batches method](#binary-attachment-push-batches).

1.  Verify that the documents are merged and indexed in the collection. The documents must contain the annotations that are applied by your external application.

{{site.data.content.webhook-security-reuse}}

{{site.data.content.ping-event-reuse}}

## Data model of the `enrichment.batch.created` event
{: #enrichment.batch.created}

Following are the `enrichment.batch.created` event parameters:

| Parameter | Description |
|-----------|----------------------|
| `event` | The event name is `enrichment.batch.created`. |
| `instance_id` | The UUID of the {{site.data.keyword.discoveryshort}} instance, which is also known as the tenant ID. |
| `version` | The webhook event version date in the `yyyy-mm-dd` format. |
| `data` | An object with the event specific information: `project_id`, `collection_id`, `enrichment_id`, and `batch_id`.  \n  \n  - `project_id`: The Universally Unique Identifier (UUID) of a project.  \n  \n  - `collection_id`: The Universally Unique Identifier (UUID) of a collection.  \n  \n  - `enrichment_id`: The Universally Unique Identifier (UUID) of an enrichment. \n  \n  - `batch_id`: The Universally Unique Identifier (UUID) of a batch.|
| `created_at` | The date and time the event was created. |
{: caption="Enrichment.batch.created" caption-side="top"}

## External enrichment limits
{: #external-enrichment-limits}

| Plan | Maximum amount of webhook enrichment per collection | Maximum amount of webhook enrichment per tenant |
|---------|-----------------------|----------------------|
| Enterprise | 1 | 100 |
| Plus | 1 | 10 |
| Premium | 1 | 100 |
{: caption="External enrichment limits" caption-side="top"}

## Binary attachment from the pull batches method
{: #binary-attachment-pull-batches}

The `pull batches` method returns a binary attachment file from Discovery.

The returned file is a compressed newline-delimited JSON (NDJSON) file. This file contains structured data that represents the document properties. For example, the following is a JSON value included in the NDJSON file:

```json
{
    "document_id": "3bafc09abfaacd90d66f57181b50d041",
    "location_encoding": "utf-16",
    "language": "en",
    "artifact": "{\"text_positions\":[0,21],\"space_above\":93.07864284515381,\"space_below\":32.53530788421631,\"is_start_of_block\":true,\"image_id\":-1}{\"text_positions\":[22,63],\"space_above\":32.53530788421631,\"space_below\":13.935576438903809,\"is_start_of_block\":true,\"image_id\":-1}{\"parent_document_id\":\"3bafc09abfaacd90d66f57181b50d041\",\"source\":{\"ListId\":\"f0ac1d32-b9e5-41af-b9da-e1e37e965d99\",\"UniqueId\":\"357d7a48-4460-442c-be56-d8bdd40a8c36\",\"ServerRelativeUrl\":\"/Lists/list1/Attachments/1/addattachments.csv\",\"FileNameAsPath\":{\"DecodedUrl\":\"addattachments.csv\"},\"ListItemId\":\"284dcb51-8021-56d0-9213-7f4eb134e083\",\"FileName\":\"addattachments.csv\",\"ServerRelativePath\":{\"DecodedUrl\":\"/Lists/list1/Attachments/1/addattachments.csv\"},\"WebId\":\"ad5bf592-3b4e-4dd1-bd3e-abc0ef179b03\"},\"ingest_datetime\":\"2023-06-26T09:24:02.573Z\",\"application_id\":\"sharepoint\",\"application_sub_type\":\"ListItemAttachmentCollection\"}0.51vanilla ice creamcontamination_tamperingotherchange_of_propertiesI love the ads for the new milk chocolate. Could you tell me the name of the actor in the commercial?{\"metadata\":{\"numPages\":\"54\",\"title\":\"\",\"publicationdate\":\"2010-06-03\"},\"info\":{\"histogram\":{\"mean-char-height\":{},\"mean-char-width\":{},\"number-of-chars\":{}},\"styles\":[]}}1451692800000",
    "features": [
        {
            "type": "field",
            "location": {
                "begin": 0,
                "end": 128
            },
            "properties": {
                "field_name": "multi_nested",
                "field_index": 0,
                "field_type": "json"
            }
        },
        {
            "type": "field",
            "location": {
                "begin": 128,
                "end": 258
            },
            "properties": {
                "field_name": "multi_nested",
                "field_index": 1,
                "field_type": "json"
            }
        },
        {
            "type": "field",
            "location": {
                "begin": 258,
                "end": 889
            },
            "properties": {
                "field_name": "metadata",
                "field_index": 0,
                "field_type": "json"
            }
        },
        {
            "type": "field",
            "location": {
                "begin": 889,
                "end": 892
            },
            "properties": {
                "field_name": "claim_score",
                "field_index": 0,
                "field_type": "double"
            }
        },
        {
            "type": "field",
            "location": {
                "begin": 892,
                "end": 893
            },
            "properties": {
                "field_name": "claim_id",
                "field_index": 0,
                "field_type": "long"
            }
        },
        {
            "type": "field",
            "location": {
                "begin": 893,
                "end": 910
            },
            "properties": {
                "field_name": "claim_product",
                "field_index": 0,
                "field_type": "string"
            }
        },
        {
            "type": "field",
            "location": {
                "begin": 910,
                "end": 933
            },
            "properties": {
                "field_name": "label",
                "field_index": 0,
                "field_type": "string"
            }
        },
        {
            "type": "field",
            "location": {
                "begin": 933,
                "end": 938
            },
            "properties": {
                "field_name": "label",
                "field_index": 1,
                "field_type": "string"
            }
        },
        {
            "type": "field",
            "location": {
                "begin": 938,
                "end": 958
            },
            "properties": {
                "field_name": "label",
                "field_index": 2,
                "field_type": "string"
            }
        },
        {
            "type": "field",
            "location": {
                "begin": 958,
                "end": 1059
            },
            "properties": {
                "field_name": "body",
                "field_index": 0,
                "field_type": "string"
            }
        },
        {
            "type": "field",
            "location": {
                "begin": 1059,
                "end": 1230
            },
            "properties": {
                "field_name": "nested",
                "field_index": 0,
                "field_type": "json"
            }
        },
        {
            "type": "field",
            "location": {
                "begin": 1230,
                "end": 1243
            },
            "properties": {
                "field_name": "claim_date",
                "field_index": 0,
                "field_type": "date"
            }
        }
    ]
}
```
{: codeblock}

Following are the binary file properties:

| Property | Type | Description |
|---------|-----------------------|----------------------|
| `document_id` | `string` | The identifier of the document. |
| `location_encoding` | `string` | The encoding type used to calculate the location of each feature. The supported types are: `utf-8`, `utf-16`, and `utf-32`. The external enrichment application must calculate the location of each feature based on the `location_encoding` of the corresponding document from Discovery. The location of features in a string representation of data varies depending on the encoding type of the programming language that is used for implementing the external enrichment. For example, C++ and Go use UTF-8, Java and JavaScript use UTF-16, and Python uses UTF-32. |
| `language` | `string` | The content language of the document. |
| `artifact` | `string` | The package of all the text values. |
| `features` | `array` | The list of features in a document. For more information, see [Feature types](#feature-types). |
{: caption="Pull method binary file properties" caption-side="top"}

## Binary attachment in the push batches method
{: #binary-attachment-push-batches}

After external enrichment, the documents can be pushed to Discovery as a binary attachment in the `push batches` method.

The file must be a compressed NDJSON file with structured data that represents the document properties. For example, the following is an NDJSON file:

```json
{
  "document_id": "3bafc09abfaacd90d66f57181b50d041",
  "features": [
    {
      "type": "annotation",
      "location": {
        "begin": 958,
        "end": 1000
      },
      "properties": {
        "type": "element_classes",
        "class_name": "expression",
        "confidence": 0.7905777096748352
      }
    },
    {
      "type": "annotation",
      "location": {
        "begin": 1001,
        "end": 1059
      },
      "properties": {
        "type": "element_classes",
        "class_name": "question",
        "confidence": 0.9507029056549072
      }
    },
    {
      "type": "annotation",
      "location": {
        "begin": 1035,
        "end": 1040
      },
      "properties": {
        "type": "entities",
        "entity_type": "JobTitle",
        "entity_text": "actor",
        "confidence": 0.70953685
      }
    },
    {
      "type": "annotation",
      "properties": {
        "type": "document_classes",
        "class_name": "amount.shortage",
        "confidence": 0.43297016620635986
      }
    },
    {
      "type": "notice",
      "properties": {
        "description": "something wrong happened",
      }
    },
    {
      "type": "notice",
      "properties": {
        "description": "something wrong happened again",
        "created": 1689076276402,
      }
    }
  ]
}
```
{: codeblock}

Following are the binary file properties:

| Property | Type | Description |
|---------|-----------------------|----------------------|
| `document_id` | `string` | The identifier of the document. |
| `features` | `array` | The list of features in a document. For more information, see [Feature types](#feature-types). |
{: caption="Push method binary file properties" caption-side="top"}

## Feature types
{: #feature-types}

A feature `type` can be one of the following in a binary file:

| Feature | Type | Description |
|---------|-----------------------|----------------------|
| `field` | `string` | Represents a specific field value of the document. |
| `annotation` | `string` | Represents a specific annotation that can enrich the document. |
| `notice` | `string` | Represents any error that might occur in the external application during document enrichment. The information in `notice` is used to generate a message on the Discovery UI. |
{: caption="Feature types" caption-side="top"}

The following are the other properties in the binary file:

| Feature | Type | Description |
|---------|-----------------------|----------------------|
| `location` | `object` | Location information to get the text value from the `artifact` by using the `begin` and `end` values. The `begin` value is a string value that represents the begin location in the artifact. The `end` value is a string value that represents an exclusive end location in the artifact. This property is null when a feature represents a document level information. For example, when `type=annotation` and `properties.type=document_classes`. |
| `properties` | `object` | The properties of a feature in the document. Supported properties vary depending on the `type` of feature. For more information, see [Field type properties](#field-type), [Annotation type properties](#annotation-type), and [Notice type properties](#notice-type). |
{: caption="Other properties in the binary file" caption-side="top"}

## Field type properties
{: #field-type}

For `field` type, the following properties represent a certain field of the document that was converted by Discovery from an original file:

| Property | Type | Description |
|---------|-----------------------|----------------------|
| `field_name` | `string` | The name of the field. |
| `field_index` | `int` | The index of a field value. This value is `0` for a single-valued field, but can be `> 0` when a field is multi-valued, such as, for an array of values. |
| `field_type` | `string` (enum: `long`, `double`, `date`, `json`) | The data type of the feature. This value determines how to parse the text representation of the feature in a programming language. |
{: caption="Field type properties" caption-side="top"}

## Annotation type properties
{: #annotation-type}

For `annotation` type, the following properties represent an annotation that can enrich a document:

| Property | Type | Description |
|---------|-----------------------|----------------------|
| `type` | `string` (enum: `entities`, `element_classes`, `document_classes`) | The type of enriched annotation that a feature represents. The `entities` are merged to entities of enriched fields. The `element_classes` are merged to element classes of enriched fields. The `document_classes` are merged to classes of document level enrichment field. |
| `confidence` | `double` | The optional confidence score by the external model. It is between `0` to `1`, and is `0` by default. |
| `entity_type` | `string` | The type of entity that an external model assigns to a thing. Required for the `entities` type. |
| `entity_text` | `string` | The representative text of an entity that the external application extracts. Required for the `entities` type. |
| `class_name` | `string` | The name of a class that the external application assigns to a thing. Required for the `element_classes` and `document_classes` type. |
{: caption="Annotation type properties" caption-side="top"}

## Notice type properties
{: #notice-type}

For `notice` type, the following properties represent errors and exceptions that occurred in the external application while enriching a document:

| Property | Type | Description |
|---------|-----------------------|----------------------|
| `description` | `string` | The message that describes an error that occurred during external enrichment. |
| `created` | `long` | Unix epoch time in milliseconds when an error occurred during external enrichment. |
{: caption="Notice type properties" caption-side="top"}
