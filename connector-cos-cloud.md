---

copyright:
  years: 2015, 2021
lastupdated: "2021-07-26"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:beta: .beta}
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

# IBM Cloud Object Storage
{: #connector-cos-cloud}

Crawl documents that are stored in an {{site.data.keyword.cos_full}} data source.
{: shortdesc}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments. If you are using a Discovery service instances that was created with a Lite or an Advanced plan, or that was created with a Premium plan before 16 July 2020, see [IBM Cloud Object Storage](/docs/discovery?topic=discovery-sources#connectcos){: external}.
{: note}

## What documents are crawled
{: #connector-cos-cloud-objects}

During the initial crawl of the content, documents from all of the content that can be accessed from the storage endpoint are crawled and added to your collection. You cannot crawl private endpoints.

During subsequent scheduled recrawls, only new and modified documents are crawled and any changes are reflected in your collection. Documents that are deleted from the external data source are not deleted from the collection.

All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

The following table illustrates the objects that {{site.data.keyword.discoveryshort}} can crawl.

| Data source | Objects that are crawled |
|-------------|--------------------------|
| {{site.data.keyword.cos_full_notm}} | Buckets, files |
{: caption="Table 1. Data sources crawling support" caption-side="top"}

## What you need before you begin
{: #connector-cos-cloud-prereqs}

Obtain any required service licenses for the content on the website that you want to connect to. For more information about licenses, contact the system administrator of the data source.

You must have the following information ready:

- **Endpoint**: The `endpoint` name to use to interact with {{site.data.keyword.cos_full_notm}} data. For example, `s3.us-south.cloud-object-storage.appdomain.cloud`.

  Do not include `http://` or `https://` in the endpoint value. For more information, see [Regional Endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints-region){: external}.
- **Access key id**: The `access_key_id` that was generated when the {{site.data.keyword.cos_full_notm}} instance was created. For example, `apr75g55a35547e6a80d80344b9h55a0`.
- **Secret access key**: The `secret_access_key` to use to sign requests. This key was generated when the {{site.data.keyword.cos_full_notm}} instance was created. For example, `806a16c5d35266db8570a074512972341j82999a5160b3rf`.

## Prerequisite step
{: #connector-cos-cloud-prereq-task}

IAM authentication is not supported currently. 

1.  Set up HMAC authentication before you configure this connector. 

    See [Service Credentials](/docs/cloud-object-storage/iam?topic=cloud-object-storage-service-credentials) for instructions.

## Connecting to the data source
{: #connector-cos-cloud-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **IBM Cloud Object Storage**, and then click **Next**.
1.  Add values to the following fields:

    - Endpoint
    - Access key id
    - Secret access key

    Click **Next**.
1.  Name the collection.
1.  If the language of the documents in storage is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule. 

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  Choose the buckets that you want to crawl. 

    The more buckets that you select, the longer the processing of the documents takes.

1.  If you want to look for and extract question-and-answer pairs, select **Apply FAQ extraction**.

    For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction).

1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    The processing time increases when this feature is enabled.
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection. 

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
