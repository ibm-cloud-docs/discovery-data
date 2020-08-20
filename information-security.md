---

copyright:
  years: 2020
lastupdated: "2020-07-15"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'} 
{:url: data-credential-placeholder='url'}
{:curl: .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Information security 
{: #information-security}

![IBM Cloud only](images/cloudonly.png)</br>
IBM is committed to providing our clients and partners with innovative data privacy, security and governance solutions.
{: shortdesc}

**Notice:**
Clients are responsible for ensuring their own compliance with various laws and regulations, including the European Union General Data Protection Regulation. Clients are solely responsible for obtaining advice of competent legal counsel as to the identification and interpretation of any relevant laws and regulations that may affect the clients' business and any actions the clients may need to take to comply with such laws and regulations.

The products, services, and other capabilities described herein are not suitable for all client situations and might have restricted availability. IBM does not provide legal, accounting, or auditing advice or represent or warrant that its services or products ensure that clients are in compliance with any law or regulation.

If you need to request GDPR support for {{site.data.keyword.cloud}} {{site.data.keyword.watson}} resources that are created, see [GDPR Subject Access Request](/docs/watson?topic=watson-gdpr-sar).

## European Union General Data Protection Regulation (GDPR)
{: #gdpr}

IBM is committed to providing our clients and partners with innovative data privacy, security and governance solutions to assist them on their journey to GDPR compliance.

Learn more about IBM's own GDPR readiness journey and our GDPR capabilities and offerings to support your compliance journey [here](https://www.ibm.com/data-responsibility/gdpr/){: external}.

## Labeling and deleting data in {{site.data.keyword.discoveryshort}}
{: #gdpr-discovery}

{{site.data.keyword.discoveryshort}} includes an API to label data per call. For details on how to label data using either the API or the {{site.data.keyword.discoveryshort}} tooling, see [Labeling data](/docs/discovery-data?topic=discovery-data-information-security#labeling).

Customer data can be deleted using the API. For information about deleting customer data, see [Deleting labeled data](/docs/discovery-data?topic=discovery-data-information-security#deletingdata).

Experimental and beta features are not intended for use with a production environment and, therefore, are not guaranteed to function, as expected, when labeling and deleting data. Do not use experimental and beta features when implementing a solution that requires the labeling and deletion of data.
{: note}

## Methods that support labeling data
{: #pi_methods}

The following stored information can be deleted using a `customer_id` if the `customer_id` was specified when the information was originally added using the associated method:

- queries (`/v2/projects/{project_id}/query`) Only when used with the `passages` or `natural_language_query` parameters
- documents (`/v2/projects/{project_id}/collections/{collection_id}/documents`)
- notices (`/v2/projects/{project_id}/notices`) Only ingestion `notices` are labeled. 
- training data (`/v2/projects/{project_id}/training_data/queries`)
- dictionaries (Only when created in the {{site.data.keyword.discoveryshort}} tooling)
- exported documents (Only when created in the Content Miner using the {{site.data.keyword.discoveryshort}} tooling)
- reports (Only when created in the Content Miner using the {{site.data.keyword.discoveryshort}} tooling)

Exported documents and reports can be viewed in the [Repository](/docs/discovery-data?topic=discovery-data-contentminerapp#cmorp) and [Report](/docs/discovery-data?topic=discovery-data-contentminerapp#cmorepv) panes of the Content Miner. They are not available using the API.

For information about the options for labeling data in {{site.data.keyword.discoveryshort}}, see [Labeling data](/docs/discovery-data?topic=discovery-data-information-security#labeling).

The following stored information is not explicitly labeled and cannot be deleted by specifying the `customer_id`. Personal Data is not supported in these fields.

Any string fields (including but not limited to `name` and `description`) of the following stored items:
- collections
- projects

## Labeling data
{: #labeling}

Data can be labeled using the API, or using the {{site.data.keyword.discoveryshort}} tooling. For more information about labeling with the tooling, see [Labeling data with the Discovery tooling ](/docs/discovery-data?topic=discovery-data-information-security#labelingtooling).

Data is labeled by adding the `customer_id` of your choice to the optional `X-Watson-Metadata` header. {{site.data.keyword.discoveryshort}} can then delete it by `customer_id`.

There are several options to label data with the API:

  - When ingesting documents using the `POST /v2/projects/{project_id}/collections/{collection_id}/documents` or `POST /v2/projects/{project_id}/collections/{collection_id}/documents/ID` operations, send an optional header `X-Watson-Metadata`. This header must include:
    -  Semicolon separated `field=value` pairs (for example: `customer_id=123`) 
       OR
    -  Add the `customer_id` field to the `X-Watson-Metadata` header. By adding the `customer_id` in `X-Watson-Metadata` header, the request indicates that it contains data that belongs to this `customer_id`.
  - Optionally, you can include the `customer_id` field with the `metadata` multi-part form part instead of using the `X-Watson-Metadata` header.

If you specify a `customer_id` in the `metadata` multi-part form part and the `X-Watson-Metadata` header for the same document, then the `customer_id` in the `X-Watson-Metadata` header is used.
{: note}
 

This example adds the `customer_id` to both the `X-Watson-Metadata` header and the `metadata`:

```bash
curl -k -u "apikey:$API_KEY" \
        -H "x-watson-userinfo:bluemix-instance-id=asdf" \
        -H "x-watson-metadata:customer_id=customer_header_123" \
        -H "x-watson-discovery-next:true" \
        -F "file=@$FILENAME" \
        -F "metadata={\"customer_id\": \"new123\"}" \
        -X POST "$API_URL/v2/projects/$PROJECT_ID/collections/$COLLECTION_ID/documents?version=2020-03-08" \
```
{: pre}

Example output:

```json
{
    "document_id":"8b152926-e9f5-4f34-940a-c02da7ef3af4",
    "result_metadata":{
      "collection_id":"24265c0b-2a55-3ccf-0000-017334467b6e"
    },
    "metadata":{
      "date":1594319812384,
      "parent_document_id":"8b152926-e9f5-4f34-940a-c02da7ef3af4",
      "customer_id":"customer_header_123"
    },
    "extracted_metadata":{
      "sha1":"CEC7C1D3423C7D4ED58FC448F52681ECA93CED8A",
      "numPages":"1",
      "filename":"Simple.pdf",
      "author":[
          "Simple Man"
      ],
      "subject":"Simple Metadata",
      "file_type":"pdf",
      "title":"Simple Title",
      "publicationdate":"2016-10-05"
},
```
{: pre}

If your documents are already ingested, you must reingest them to add the `X-Watson-Metadata` header and `customer_id`.
{: important}

Restrictions:

- The value of the `X-Watson-Metadata` header cannot exceed 4 kilobytes of text.
- The `X-Watson-Metadata` header must contain a semicolon separated list of `field=value` pairs. The `field` and `value` must not contain semicolons (`;`) or equals signs (`=`).
- `customer_id`s are unique within each {{site.data.keyword.discoveryshort}} instance. They are NOT unique per project or collection.
- A `customer_id` cannot be more than 256 characters in length.
- If a `customer_id` contains only whitespace or is empty, it is treated as though the `customer_id` was not provided at all, and no error messages are returned.

### Labeling data with the Discovery tooling
{: #labelingtooling}

Data can be labeled using the {{site.data.keyword.discoveryshort}} tooling, or using the API. For more information about labeling with the API, see [Labeling data](/docs/discovery-data?topic=discovery-data-information-security#labeling).

To label data with the tooling:

1.  Open the **Projects** page by selecting **My Projects**.
1.  Select **Data usage and GDPR**. 
1.  Choose the **GDPR data label** tab.
1.  Set the **Label data with customer ID** toggle to `on`. The **Customer ID** field appears.
1.  Enter a unique ID for the customer in the **Customer ID** field. Do not include personal data in a **Customer ID**.
1.  Click **Save ID**.

After the **Customer ID** (`customer_id`) field is set, all data uploaded or crawled during the current browser session is labeled with the specified **Customer ID**. 

Adding a **Customer ID** labels the documents, notices, dictionaries, and training data within that URL domain from that point forward, including each instance under that domain. Any actions, including document uploads, that occurred in the {{site.data.keyword.discoveryshort}} tooling before adding the **Customer ID** field are not labeled.

If you switch domains or browsers, empty the browser cache, or start an incognito session after you specify your **Customer ID** using the {{site.data.keyword.discoveryshort}} tooling, the **Customer ID** is not retained, and your data is not labeled. If you must switch domains or browsers, after the switch, open the **GDPR data label** tab, re-enter the **Customer ID** and click **Save ID**.
{: note}

If an existing **Customer ID** needs to be changed:

1. Delete the data associated with that **Customer ID**. For instructions, see [Deleting labeled data](/docs/discovery-data?topic=discovery-data-information-security#deletingdata).
1. Follow the instructions to label data with the {{site.data.keyword.discoveryshort}} tooling, or using the API.
1. Upload or crawl the data.

## Deleting labeled data
{: #deletingdata}

Customer data labeled with a `customer_id` can be deleted using the API. For details on how to label data using either the API or the {{site.data.keyword.discoveryshort}} tooling, see [Labeling data](/docs/discovery-data?topic=discovery-data-information-security#labeling).

You cannot delete labeled data using the {{site.data.keyword.discoveryshort}} tooling.
{: note}

1. Use the `DELETE /v2/user_data` operation and provide the `customer_id` of the data you wish to delete. 
   -  `DELETE /v2/user_data` deletes all data associated with a particular `customer_id` within that service instance, as specified in [Methods that support labeling data](/docs/discovery-data?topic=discovery-data-information-security#pi_methods). Also see **Delete labeled data** in the [API reference](https://{DomainName}/apidocs/discovery-data#deleteuserdata){: external}
1. To ensure all labeled content is correctly removed, run `user_delete` after the `processing` and `pending` counts for all collections in your environment return `0`.

Notes on deleting labeled data:

- Deletions are performed asynchronously. You cannot track the progress of deletions.
- If a non-existent `customer_id` is provided, nothing is deleted, but a `202 - Accepted` response is returned.
- Projects and collections are not labeled with a `customer_id`, even if a `X-Watson-Metadata` header is included in the request to create the project or collection. Only the individual documents within a collection are labeled. Therefore when data is deleted, individual projects and collections are NOT deleted.