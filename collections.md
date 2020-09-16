---

copyright:
  years: 2019, 2020
lastupdated: "2020-09-16"

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

# Creating and managing collections
{: #collections}

<!-- c/s help for the *Managing collections* page. Do not delete. -->

A collection is a set of documents you upload or crawl. You can also enrich, train, and query collections.
{: shortdesc}


## Creating a collection
{: #createcollection}

When you create a collection, {{site.data.keyword.discoveryshort}} pulls documents from a data source, using a process called crawling. Crawling is the process of systematically browsing and retrieving documents from a specified start location. {{site.data.keyword.discoveryshort}} only crawls items that you explicitly specify.

1. To create a collection, first create a **Project** and choose a **Project type**. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects). Alternately, you can open your project, select the **Manage collections** icon on the navigation panel, and then click **New collection**. 
1. Choose a data source, or select **Use an existing collection**.
1. Name your collection, and choose the language of that collection. For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1. Select the crawl schedule. For available options and details, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1. Configure the data source.
   -  [Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types)
   -  [IBM Cloud data sources](/docs/discovery-data?topic=discovery-data-sources)
   -  [Uploading data](/docs/discovery-data?topic=discovery-data-collections#upload-data)
1. Select **Create collection**, which starts the crawling process. The **Activity** tab opens and updates as documents are added to the collection. The crawl syncs the data initially and updates periodically at the specified frequency.

This video provides an overview of connecting to data sources in {{site.data.keyword.discoveryshort}}. The available data sources vary by version:

![Watson Discovery Demo: Connect to the data source you want](https://www.youtube.com/embed/MPCOwMgn1p4){: video output="iframe" id="youtubeplayer" frameborder="0" width="560" height="315" webkitallowfullscreen mozallowfullscreen allowfullscreen}

![Cloud Pak for Data only](images/cpdonly.png) The number of collections you can create depends on your hardware configuration. {{site.data.keyword.discoveryshort}} supports a maximum of 256 collections per instance and installation, but that number depends on many factors, including memory.
{: note}

To stop a crawler that is in progress, click **Stop**. You can only stop a crawler that is in progress, and the crawler is only stopped for the interval between clicking **Stop** and the next scheduled crawl. For example, if you specified an hourly crawl and you click **Stop**, the crawler stops for an hour and resumes crawling hourly.

If you want to access an existing collection, complete the following steps:

1. Select the **Manage collections** icon on the navigation panel. Existing collections display the document count and last updated date.
1. Select the collection you need. The **Activity** tab displays.

For information about creating a collection by using the API, see [Create a collection](https://{DomainName}/apidocs/discovery-data#createcollection){: external}.

## Supported file types and general requirements
{: #supportedfiletypes}

{{site.data.keyword.discoveryshort}} can ingest the following file types; it ignores all other document types:
   
   - PDF
   - Microsoft Word (doc; docx)
   - Microsoft PowerPoint (ppt; pptx)
   - Microsoft Excel (xls; xlsx)
   - TXT\*
   - CSV \*
   - JSON\*
   - HTML\* 
   - PNG\*\*
   - TIFF\*\*
   - JPG\*\*
   - ZIP\*\*\*
   - GZIP\*\*\*
   - TAR\*\*\*
    
\* JSON, HTML, TXT, and CSV documents are supported by {{site.data.keyword.discoveryshort}}, but you cannot customize fields within these files using the Smart Document Understanding editor.

\*\* Individual image files (PNG, TIFF, JPG) are scanned, and any text is extracted. PNG, TIFF, and JPEG images embedded in PDF, Word, PowerPoint, and Excel files are also scanned, and any text is extracted.

\*\*\*Files within compressed archive files (ZIP, GZIP, TAR) are extracted. {{site.data.keyword.discoveryshort}} ingests the supported file types within them; it ignores all other file types.

A connector is a component that provides data connectivity and extraction capabilities for external data sources. In {{site.data.keyword.discoveryshort}}, you establish a connector during the process of creating a collection for a data source. The following general requirements apply to all connectors:

-  Each collection can support only one data source.
-  Connectors are not available when you use the API.
-  You need the credentials and file locations, or URLs, for each data source, which a developer or system administrator of the data source typically provides.
-  You need to manually provide the resources to crawl. Auto discovery is not supported.

## Crawl schedule options
{: #crawlschedule}

When you create a collection, the initial crawl starts immediately. The frequency you choose for the crawl schedule determines when the next crawl starts in relation to the first. You can schedule crawls to update at the following intervals:
    
-  Hourly: runs every hour
-  Daily: runs every day at the same time as the initial crawl
-  Weekly: runs every week on the same day and time as the initial crawl
-  Monthly: runs every 30 days at the same time as the initial crawl

If you modify crawl settings on the **Processing settings** page and then click **Save collection**, the crawl restarts immediately. To view the collection status, see the **Activity** tab. 
{: note}

## Uploading data
{: #upload-data}

Use this option to upload data you stored locally. Only documents supported by {{site.data.keyword.discoveryshort}} are crawled; all others are ignored.
{: shortdesc}

For a list of file types that you can upload to {{site.data.keyword.discoveryshort}}, see [Supported file types and general requirements](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes). After the upload begins, the **Activity** tab opens and updates as documents are added to the collection. Your collection is finished processing when the status indicates `Processing finished. Updated documents are ready for you.`.

Optional: Click **More processing settings** to expand the menu, and then click **Apply optical character recognition (OCR)**. By default, this option is set to **Off**. If you set it to **On**, {{site.data.keyword.discoveryshort}} extracts text from images, using Optical Character Recognition (OCR).

For additional information about supported data sources in {{site.data.keyword.discoveryshort}}, see the following links:
- ![Cloud Pak for Data only](images/cpdonly.png) [Configuring Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types)
- ![IBM Cloud only](images/cloudonly.png) [Configuring IBM Cloud data sources](/docs/discovery-data?topic=discovery-data-sources)
