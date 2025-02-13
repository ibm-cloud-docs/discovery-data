---

copyright:
  years: 2019, 2025
lastupdated: "2025-02-13"

keywords: upload,one-time upload,add document,add files

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Uploading data
{: #upload-data}

You can perform a one-time document upload from your local file system at any time to add data to a project.
{: shortdesc}

You can upload up to 200 files at a time.

To process document sets that are larger than 200 files, you can add them to an external data source and use a data source crawler to upload them. For {{site.data.keyword.icp4dfull_notm}} deployments, you can use a *Local File System* data source for this purpose.

For more information about the maximum size allowed for each file, see [Document limits](/docs/discovery-data?topic=discovery-data-collections#collections-doc-limits).

Before you upload a CSV file to a Content Mining project, consider adding headers to the source file so that any fields that are generated from the file have meaningful names. Without headers, fields are given generic names, such as `column_0`, `column_1`, and so on.
{: tip}

To upload data, complete the following steps:

1.  Open your project, go to the **Manage collections** page, and then click **New collection**.
1.  Do the following based on your deployement type:

    [IBM Cloud Pak for Data]{: tag-cp4d} [IBM Software Hub]{: tag-teal}
    1.  Choose Upload data as your data source and then click Next.

        You can also connect to a different data source instead of uploading data such as reusing data from a collection or crawling an external data source. For more information, see [Reusing data from a collection](/docs/discovery-data?topic=discovery-data-manage-collections#manage-collections-reuse) and [Overview of Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types).

    1.  Name the collection. If the language of the documents in storage is not English, select the appropriate language. For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
    1.  Optionally, click **More processing settings** to expand the menu. You can select the following settings:
    
        -  Set **Apply optical character recognition (OCR)** switcher to **On** to enable OCR.

           When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
           {: note}

        -  Set **Use stemming instead of lemmatization when indexing** switcher to *On* to use stemming instead of lemmatization to normalize words in the index and queries. For more information, see [Enabling stemming for uncurated data](/docs/discovery-data?topic=discovery-data-collections#stemmer).

    1.  Click **Next**

    1.  Upload data by browsing for the files you want to crawl.

        You can drag documents that you want to add to your collection.

        For more information about supported file types, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).

    1.  Click **Finish**.

    [IBM Cloud]{: tag-ibm-cloud}
    1.  Name the collection. If the language of the documents in storage is not English, select the appropriate language. For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

    1.  Upload data by browsing for the files you want to add.

        You can drag documents that you want to add to your collection.

        For more information about supported file types, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).

        You can also connect to a different data source instead of uploading data such as reusing data from a collection or crawling an external data source. To connect to a different data source, click the link next to the **Need to connect to a data source**? field. For more information, see [Reusing data from a collection](/docs/discovery-data?topic=discovery-data-manage-collections#manage-collections-reuse) and [Overview of Cloud data sources](/docs/discovery-data?topic=discovery-data-sources).

    1.  Optionally, click **More processing settings** to expand the menu. You can select the following:
    
        -  Set **Apply optical character recognition (OCR)** switcher to **On** to enable OCR.

           When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
           {: note}

        -  Set **Use stemming instead of lemmatization when indexing** switcher to **On** to use stemming instead of lemmatization to normalize words in the index and queries. For more information, see [Enabling stemming for uncurated data](/docs/discovery-data?topic=discovery-data-collections#stemmer)

    1.  Click **Finish**.

The file upload is completed quickly. It takes more time for the data to be processed as it is added to the collection. After the files are uploaded and processed, the *Activity* page shows the upload results.

Unlike crawled data sources, you cannot schedule regular updates for uploaded files. If you want to add a later version of a file, delete the earlier version of the file, and then upload the latest version.

For information about how to troubleshoot issues that you might encounter when adding documents to a collection, see [Troubleshooting ingestion](/docs/discovery-data?topic=discovery-data-troubleshoot-ingestion).

For more information about what happens next, see [How your data source is processed](/docs/discovery-data?topic=discovery-data-index-overview).
