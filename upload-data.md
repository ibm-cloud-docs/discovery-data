---

copyright:
  years: 2019, 2021
lastupdated: "2021-06-04"

keywords: upload, one-time upload

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
{:external: target="_blank" .external}
{:video: .video}

# Uploading data
{: #upload-data}

You can perform a one-time document upload from your local file system at any time to add data to a project.
{: shortdesc}

You can upload up to 200 files at a time. The maximum size allowed for each file is 32 MB.

To process document sets that are larger than 200 files, add them to an external data source and use a data source crawler to upload them. For {{site.data.keyword.icp4dfull_notm}} deployments, you can use a *Local File System* data source for this purpose.

Before you upload a CSV file to a Content Mining project, decide whether you want to apply enrichments to the content. If so, consider adding headers to the source file so that any fields that are generated have meaningful names. Without headers, fields are given generic names, such as `column_0`, `column_1`, and so on.
{: tip}

To upload data, complete the following steps:

1.  Open your project, go to the **Manage collections** page, and then click **New collection**.
1.  Choose **Upload data** as your data source, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents in storage is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: If you want to look for and extract question-and-answer pairs, select **Apply FAQ extraction**.

    For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction).
1.  Optionally, click **More processing settings** to expand the menu, and then click **Apply optical character recognition (OCR)**. 

    By default, this option is set to **Off**. If you set it to **On**, {{site.data.keyword.discoveryshort}} extracts text from images, by using optical character recognition. When OCR is enabled and your documents contain images, processing takes longer.

1.  Click **Next**.
1.  Browse for the files you want to crawl.

    ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: You can drag documents that you want to add to your collection.

    For more information about supported file types, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
1.  Click **Finish**.

The file upload is completed quickly. It takes more time for the data to be processed as it is added to the collection. After the files are uploaded and processed, the Activity page shows the upload results.
