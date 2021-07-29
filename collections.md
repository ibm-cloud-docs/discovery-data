---

copyright:
  years: 2019, 2021
lastupdated: "2021-07-29"

keywords: data sources, supported data sources, supported file types, document types

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

# Creating collections
{: #collections}

<!-- c/s help for the *Manage collections* page. Do not delete. -->

A collection is a set of documents that you upload or crawl from where it resides on a connected data source.
{: shortdesc}

## How do I decide what to add to a collection?
{: #createcollection-why}

There a few things to consider as you decide how to break up your source content into collections.

- Getting content from different data sources

  If you store similar content in more than one type of data source (a website and Salesforce, for example), you can create one project with two separate collections. Each collection adds documents from a single data source. When they are built together into a single project, a user can search across both sources at once.
- Creating separate Smart Document Understanding (SDU) models

  You can use the Smart Document Understanding tool to identify content based on the structure of a document. If you have 20 PDF files that were created by your Sales department and therefore use one template and 20 PDF files that were created by your Research department that use a different template, you might want to group each set into its own collection. You can then use the SDU tool to build a model for each structure separately, a model that understands the unique structure. You can also use the tool to define custom fields that are unique to the source documents.
- Applying enrichments

  Creating a collection is a good way to group documents that you want to enrich in a similar way. For example, you might want to create a collection of documents with frequently asked questions that are formatted in a consistent manner so you can apply the FAQ extraction feature to the collection. Or maybe a subset of your documents contains lots of industry jargon and you want to add a dictionary that recognizes the terms. You can create a separate collection and apply the Parts of Speech enrichment so you can use the term suggestions feature to speed up the process of creating the dictionary.

## Creating a collection
{: #createcollection}

When you create a collection, {{site.data.keyword.discoveryshort}} pulls documents from a data source by *crawling* the data source. Crawling is the process of systematically browsing and retrieving documents from a specified start location.

Before you can create a collection, you must create a project. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).

1.  To create a collection, open a project, go to the **Manage collections** page, and then click **New collection**.

    - The Document Retrieval and Custom project types can contain up to 5 collections. 
    - A Conversational Search project can contain 5 collections but only 1 collection is used by the {{site.data.keyword.conversationshort}} search skill. 
    - A Content Mining project can contain only 1 collection.
    - ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: The number of collections you can create depends on your hardware configuration. {{site.data.keyword.discoveryshort}} supports a maximum of 300 collections per instance and installation, but that number depends on many factors, including memory.
1.  Choose a data source type, reuse data from an existing data collection, or perform a one-time document upload from your local file system.

    - [Uploading data](/docs/discovery-data?topic=discovery-data-upload-data)
    - [Reusing data from a collection](/docs/discovery-data?topic=discovery-data-manage-collections#manage-collections-reuse)
    - For external data sources, see the appropriate topic for your deployment:

      - ![Cloud Pak for Data only](images/desktop.png) [{{site.data.keyword.icp4dfull_notm}}](/docs/discovery-data?topic=discovery-data-collection-types)
      - ![IBM Cloud only](images/ibm-cloud.png) [{{site.data.keyword.cloud_notm}} data sources](/docs/discovery-data?topic=discovery-data-sources)

      A collection can support only one data source.
      {: note}

## Collection limits
{: #collections-limits}

The number of collections you can create per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Collections per service instance |
|--------------|--------------------------------:|
| Cloud Pak for Data |                       300 |
| Premium      |                             300 |
| Plus (includes Trial) |                     40 |
{: caption="Plan details" caption-side="top"}

The maximum number of collections that is allowed per project differs by project type.

For more information about the supported number of collections for Lite and Advanced plan instances, see [Discovery pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans#advanced){: external} in the earlier version of the product documentation.

## Data source overview video
{: #collections-video}

This video provides an overview of connecting to data sources in {{site.data.keyword.discoveryshort}}. The available data sources vary by version:

![Watson Discovery Demo: Connect to the data source you want](https://www.youtube.com/embed/MPCOwMgn1p4){: video output="iframe"  data-script="none" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

To view the transcript, open the video on YouTube.

## Supported file types
{: #supportedfiletypes}

{{site.data.keyword.discoveryshort}} can ingest specific file types. For all other types of files, a warning message is displayed and the file is not ingested. 

The following table shows the supported file types and information about feature support that varies by file type.

| Supported file type | Use Smart Document Understanding to identify fields | Enable OCR to extract text from images |
|---------------------|-----------------------------------------------------|----------------------------------------|
| Contract (written in any supported file type) | A pretrained SDU model is applied automatically | ![checkmark icon](../../icons/checkmark-icon.svg) (Enabled by default) |
| CSV | | |
| DOC, DOCX | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| GIF | | |
| HTML | | |
| JPG | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| JSON | | |
| PDF | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| PNG | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| PPT, PPTX | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| TIFF | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| TXT | | |
| XSL, XSLX | | ![checkmark icon](../../icons/checkmark-icon.svg) |
{: row-headers}
{: class="comparison-table"}
{: caption="Supported file types" caption-side="top"}
{: summary="This table has row and column headers. The row headers identify supported file types. The column headers identify different product features. To understand which features are available for a file type, go to the row that describes the document type, and find the columns for the feature you are interested in."}
    
Files within compressed archive files (ZIP, GZIP, TAR) are extracted. Discovery ingests the supported file types within the archive; it ignores all other file types. Discovery supports MacOS ZIP files only if they are generated by using a command such as: `zip -r my-folder.zip my-folder -x "*.DS_Store"`. ZIP files that are created by right-clicking a folder and clicking *Compress* are not supported.

## Document limits
{: #collections-doc-limits}

The number of documents that are allowed per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

The document limit applies to the number of documents in the index. Upload fewer documents at the start if the enrichments you plan to apply will increase the number of documents later. For example, the following configurations generate more documents:

- Splitting documents segments one document into multiple documents
- Applying FAQ extractions produces one document for each question-and-answer pair that is found
- CSV files that you upload generate one document per line
- Database data sources that you crawl produce one document per database row
- Each object that is defined in an array in a JSON file results in a separate document

| Plan | Documents per service instance |
|------|-------------------------------:|
| Cloud Pak for Data |          Unlimited |
| Premium      |                Unlimited |
| Plus (includes Trial) |         500,000 |
{: caption="Number of documents per service instance" caption-side="top"}

The maximum allowed number can vary slightly depending on the size of the documents. Use these values as a general guideline.
{: note}

The size of each document that you can upload depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | File size per document |
|--------------|--------------------------------:|
| Cloud Pak for Data |                     32 MB |
| Premium      |                           50 MB |
| Plus (includes Trial)         |          10 MB |
{: caption="Maximum document size" caption-side="top"}

For more information about the supported number of documents for Lite and Advanced plan instances, see [Discovery pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans#advanced){: external} in the earlier version of the product documentation.

## Field limits
{: #collections-field-limits}

When a document is added to a collection, content from the document is evaluated and added to the appropriate fields in an internal index. For example, when you crawl a website or upload an HTML file, the HTML content is added to the collection and indexed in an `html` field.

The following table shows the maximum size limit for fields per document.

| Field type | Maximum allowed size per document | 
|-------|------|--------------------------------:|
| `html` field | 5 MB |
| Sum of all other fields | 1 MB |
{: caption="Maximum field sizes" caption-side="top"}

How a document is treated during collection creation if the maximum size of the fields in the document exceeds the allowed limit differs depending on how {{site.data.keyword.discoveryshort}} is deployed.

The following table shows how the fields are processed depending on the deployment type.

| Deployment type | Document with an oversized `html` field | Document with oversized non-HTML fields |
|--------------|--------------------------------|-----------------|
| Cloud Pak for Data | The document is not indexed | The document is not indexed |
| IBM Cloud | All of the fields in the document are indexed except the `html` field | The document is not indexed |
{: caption="Exceeded field size behavior" caption-side="top"}

## Supported data sources
{: #collections-data-sources-table}

The following table shows the supported data sources for each deployment type.

| Data source | IBM Cloud | IBM Cloud Pak for Data |
|-------------|-----------|------------------------|
| Box | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Database (IBM Db2, Microsoft SQL, Oracle, Postgres) | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Filenet P8 | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| HCL Notes | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| IBM Cloud Object Storage | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Local file system | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Salesforce | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Microsoft SharePoint Online | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Microsoft SharePoint On-Premises | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Web site | ![checkmark icon](../../icons/checkmark-icon.svg) | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Windows file system | | ![checkmark icon](../../icons/checkmark-icon.svg) |
{: row-headers}
{: class="comparison-table"}
{: caption="Supported data sources" caption-side="top"}
{: summary="This table has row and column headers. The row headers identify supported data sources. The column headers identify the different product deployment options. To understand which data sources are available for your deployment type, go to the row that describes the data source, and find the columns for the type of deployment you're interested in."}

## Crawl schedule options
{: #crawlschedule}

When you create a collection, the initial crawl starts immediately. The frequency that you choose for the crawl schedule determines when the next crawl will start. 

To create a crawl schedule, complete the following steps:

1.  In the in *Crawl schedule* section, choose a frequency. 

    - If you want to crawl every 12 hours or every 10 days, choose **Custom intervals**. You can schedule the crawler to run on a custom number of days, hours, or minutes.
    - By default, the crawl is scheduled to start during off-peak hours.
    - Do not set the interval to a frequency that is shorter than the time it takes for the crawl to finish.
    - Do not configure multiple crawlers to run at short intervals.
    - ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.discovery-data_short}}**: You can schedule the crawler to run at a specific day and time. This option is helpful if you want to avoid heavy load on a target system during business hours. You can schedule the crawl for 01:00 AM on Saturdays, for example.
    - If you open a collection in a time zone other than the one in which the collection was created, the Coordinated Universal Time (UTC) offset information is displayed.

1.  ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.discovery-data_short}}**: In **More scheduling settings**, you can choose the type of schedule to use to crawl the collection from the following options:

    - To control the frequency of the crawls yourself, choose this option:

      - **Full crawling**:  When you choose a full crawl schedule type, the crawl occurs with the frequency that you specify in the *Crawl schedule* section of the page.

    - To allow the system to manage the frequency of the crawls for you, choose one of the following options:

      - **Crawling updates (look for new, modified, and deleted contents)**
      - **Crawling new and modified contents**

      When you choose a schedule type that crawls for updates or for new and modified contents, the frequency that you specify for the crawl schedule is ignored. The frequency with which each document is crawled is variable and is managed entirely by the service. And the frequency changes depending on how often changes are found in a document. For example, if 5 of the 10 documents in a collection have changed by the end of the first crawl interval, then the frequency is automatically increased for those 5 documents. Currently, the highest frequency at which these self-managed refreshes can run is daily.
      
      You cannot interrupt the automated management of frequency and you cannot trigger a one-off crawl when these types of scheduled crawls are configured.

If you want to change the flexible crawl schedule settings later, you can go to the *Processing settings* page, edit the settings, and then click **Apply changes and reprocess**.
