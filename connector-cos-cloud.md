---

copyright:
  years: 2015, 2023
lastupdated: "2023-02-08"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# IBM Cloud Object Storage
{: #connector-cos-cloud}

Crawl documents that are stored in an {{site.data.keyword.cos_full}} data source.
{: shortdesc}

[IBM Cloud]{: tag-ibm-cloud} **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments.
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

Endpoint
:   The `endpoint` for your {{site.data.keyword.cos_full_notm}} data. For example, `s3.us-south.cloud-object-storage.appdomain.cloud`.

    Do not include `http://` or `https://` in the endpoint value. For more information, see [Regional Endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints-region){: external}.

In addition to the endpoint, you must provide credentials to enable authentication with the object store. You can choose to use one of the following authentication methods:

HMAC
:    Uses a hash-based message authentication code to authenticate users. HMAC is a cryptographic authentication technique that uses a hash function and a secret key. The data is scrambled before it is sent over the internet. Then, the intended recipient uses the secret key to unscrambles the data. For more information, see [HMAC authentication](#connector-cos-cloud-hmac).

IAM
:    Uses the IBM Cloud Identity and Access Management (IAM) service to authenticate users. The advantage of this authentication type is that the user can use the same process to access all of the resources in the IBM Cloud Platform. For more information, see [IAM authentication](#connector-cos-cloud-iam).

To access the credential information, go to the service credentials page of your {{site.data.keyword.cos_full_notm}} service instance. Expand the service credential to see the credential details. 

For more information, see [Service credentials](/docs/cloud-object-storage/iam?topic=cloud-object-storage-service-credentials){: external} in the Object Storage product documentation.

### HMAC authentication
{: #connector-cos-cloud-hmac}

If you want to use HMAC authentication, you must have the following information ready:

Access key id
:   The `access_key_id` that was generated when the {{site.data.keyword.cos_full_notm}} instance was created. For example, `347aa3a4b34344f8bc7c7cccdf856e4c`.

Secret access key
:   The `secret_access_key` to use to sign requests. This key was generated when the {{site.data.keyword.cos_full_notm}} instance was created. For example,  `gvurfb82712ad14W7a7915h763a6i87155d30a1234364f61`.

### IAM authentication
{: #connector-cos-cloud-iam}

If you want to use IAM authentication, you must have the following information ready:

IAM API key
:   For example, `0viPHOY7LbLNa9eLftrtHPpTjoGv6hbLD1QalRXikliJ`.

Resource instance ID
:   For example, `crn:v1:bluemix:public:cloud-object-storage:global:a/3ag0e9402tyfd5d29761c3e97696b71n:d6f74k03-6k4f-4a82-b165-697354o63903::`.

## Connecting to the data source
{: #connector-cos-cloud-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **IBM Cloud Object Storage**, and then click **Next**.
1.  Choose a credential type, and then complete the fields with the information that you collected earlier.

    -   IAM
    -   HMAC
    
    Click **Next**.
1.  Name the collection.
1.  If the language of the documents in storage is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  Choose the buckets that you want to crawl.

    The more buckets that you select, the longer the processing of the documents takes.

1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
