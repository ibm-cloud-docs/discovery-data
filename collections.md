---

copyright:
  years: 2019, 2023
lastupdated: "2023-01-05"

keywords: data sources,supported data sources,supported file types,document types,file size,field limits,OCR,optical character recognition,file limits

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Creating collections
{: #collections}

<!-- c/s help for the *Manage collections* page. Do not delete. -->

A collection is a set of documents that you add to a project so that you can analyze, enrich, and extract useful information from it.
{: shortdesc}

You can add data to your project in the following ways:

-   Upload locally-accessible files by using the product user interface. This method is the best way to get started and test your use case.
-   Set up a scheduled crawl of documents that are stored on an external data source.

    The product user interface offers several built-in data source connectors for you to choose from. The options differ depending on your deployment type. For more information, see [Supported data sources](#collections-include-data-sources-reuse).
-   Connect to an external data source for which there is no built-in support:

    ![IBM Cloud only](images/ibm-cloud.png) {{site.data.keyword.cloud_notm}}
    :    Use IBM App Connect to set up a scheduled crawl of documents that are stored on other external data sources.
    
    ![Cloud Pak for Data only](images/desktop.png) {{site.data.keyword.icp4dfull_notm}}
    :    Build a connector to crawl documents that are stored on other external data sources.

-   To automate the process of adding data to your project, use the Discovery APIs to create a collection and upload documents to it.

## How do I decide what to add to a collection?
{: #createcollection-why}

There a few things to consider as you decide how to break up your source content into collections.

-   Getting content from different data sources

    If you store similar content in more than one type of data source (a website and Salesforce, for example), you can create one project with two separate collections. Each collection adds documents from a single data source. When they are built together into a single project, a user can search across both sources at the same time.
-   Applying enrichments

    Creating a collection is a good way to group documents that you want to enrich in a similar way. For example, you might want to create a collection of documents with frequently asked questions that are formatted in a consistent manner. After you group the documents, you can apply the FAQ extraction feature to the collection. Or maybe a subset of your documents contains industry jargon and you want to add a dictionary that recognizes the terms. You can create a separate collection and apply the Parts of Speech enrichment so you can use the term suggestions feature to speed up the process of creating the dictionary.
-   Creating separate Smart Document Understanding (SDU) models

    You can use the Smart Document Understanding tool to identify content based on the structure of a document. If you have 20 PDF files that were created by your Sales department that use one template and 20 PDF files that were created by your Research department that use a different template, group each set into its own collection. You can then use the SDU tool to build a model for each structure separately, a model that understands the unique structure. You can also use the tool to define custom fields that are unique to the source documents.

## Creating a collection
{: #createcollection}

Before you can create a collection, you must create a project. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).

Things to keep in mind:

-   A collection can support only one external data source.
-   Documents in the collection must be in one language only, the language that you specify for the collection.

To create a collection, complete the following steps:

1.  Open a project, go to the **Manage collections** page, and then click **New collection**.

    -   The Conversational Search, Document Retrieval, and Custom project types can contain up to 5 collections.
    -   A Content Mining project can contain only 1 collection.

1.  Choose how you want to add data to your collection.

    -   [Uploading data](/docs/discovery-data?topic=discovery-data-upload-data)
    -   [Reusing data from a collection](/docs/discovery-data?topic=discovery-data-manage-collections#manage-collections-reuse)
    -   Crawling an external data source.
    
        For supported data sources, see the appropriate topic for your deployment type:

        -   ![Cloud Pak for Data only](images/desktop.png) [{{site.data.keyword.icp4dfull_notm}}](/docs/discovery-data?topic=discovery-data-collection-types)
        -   ![IBM Cloud only](images/ibm-cloud.png) [{{site.data.keyword.cloud_notm}} data sources](/docs/discovery-data?topic=discovery-data-sources)

        These topics also describe how to connect to data sources that are not supported by default per deployment type.
        {: tip}

For information about how to troubleshoot issues that you might encounter when you add documents to a collection, see [Troubleshooting ingestion](/docs/discovery-data?topic=discovery-data-troubleshoot-ingestion).

For more information about how to create a collection programmatically, see the [API reference documentation](/apidocs/discovery-data#createcollection){: external}.

## Optical character recognition
{: #ocr}

One of the optional features that you can apply to a collection when you create it is optical character recognition. The optical character recognition (OCR) feature extracts text from images. This capability is useful for preserving information that is depicted in diagrams or graphs, or in text that is embedded in files such as scanned PDFs. By converting the visual information into text, it can later be searched.

![IBM Cloud only](images/ibm-cloud.png) A new version of the technology was introduced in cloud-managed instances. OCR v2 was developed by IBM Research to be better at extracting text from scanned documents and other images that have the following limitations:

-   Low quality images due to incorrect scanner settings, insufficient resolution, bad lighting (such as with mobile capture), loss of focus, misaligned pages, and badly printed documents
-   Documents with irregular fonts or a variety of colors, font sizes, and backgrounds

Things to keep in mind when you enable OCR:

-   The time that it takes to ingest a document with images increases when OCR is enabled.
-   OCR can read both clear and noisy images. It can convert noisy images to gray scale, and smooth and de-skew them. However, the image quality must meet the minimum requirement of **80 DPI** (dots per inch).
-   OCR can recognize many languages, but the language of the text in the image must be the same as the language that is specified for the collection where the file is added. 

For more information about languages for which OCR v1 and OCR v2 are supported, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

For a list of files types where you can apply OCR, see the [Supported file types](#supportedfiletypes) table.

## Collection limits
{: #collections-limits}

The number of collections that you can create per project differs by project type.

| Project type | Collections per project |
|--------------|------------------------:|
| Document Retrieval |                 5 |
| Document Retrieval for Contracts |   5 |
| Conversational Search |              5 |
| Content Mining |                     1 |
| Custom |                             5 |
{: caption="Collections per project limits" caption-side="top"}

The number of collections you can create per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Collections per service instance |
|------|---------------------------------:|
| Cloud Pak for Data |                300 |
| Premium      |                      300 |
| Enterprise |                        300 |
| Plus (includes Trial) |              40 |
{: caption="Plan details" caption-side="top"}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: The number of collections you can create depends on your hardware configuration. {{site.data.keyword.discoveryshort}} supports a maximum of 300 collections per instance and installation, but that number depends on many factors, including memory.

## Data source overview video
{: #collections-video}

This video provides an overview of connecting to data sources in {{site.data.keyword.discoveryshort}}. The available data sources vary by version:

![Watson Discovery Demo: Connect to the data source that you want](https://www.youtube.com/embed/MPCOwMgn1p4){: video output="iframe"  data-script="none" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

To read a transcript of the video, [open the video on YouTube.com](https://www.youtube.com/watch?v=MPCOwMgn1p4), click the *More actions* icon, and then choose *Open transcript*.

## Supported file types
{: #supportedfiletypes}

{{site.data.keyword.discoveryshort}} can ingest specific file types. For all other types of files, a warning message is displayed and the file is not ingested.

The following table shows the supported file types and information about feature support that varies by file type.

| File type | Text extraction support | Smart Document Understanding (SDU) support | Optical Character Recognition (OCR) support |
|-----------|:------------------------|-------------------------------------------:|:-------------------------------------------:|
| CSV | ![checkmark icon](../icons/checkmark-icon.svg) | | |
| DOC, DOCX | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| GIF | ![checkmark icon](../icons/checkmark-icon.svg) | | |
| HTML | ![checkmark icon](../icons/checkmark-icon.svg) | | |
| JPG | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| JSON | ![checkmark icon](../icons/checkmark-icon.svg) | | |
| PDF | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| PNG | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| PPT, PPTX | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| TIFF | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| TXT | ![checkmark icon](../icons/checkmark-icon.svg) | | |
| XLS, XLSX | ![checkmark icon](../icons/checkmark-icon.svg) | | ![checkmark icon](../icons/checkmark-icon.svg) |
{: row-headers}
{: class="comparison-table"}
{: caption="Supported file types" caption-side="top"}
{: summary="This table has row and column headers. The row headers identify supported file types. The column headers identify different product features. To understand which features are available for a file type, go to the row that describes the document type, and find the columns for the feature you are interested in."}

-  PDF files that are secured with a password or certificate are not supported.
-  Files within compressed archive files (ZIP, GZIP, TAR) are extracted. Discovery ingests the supported file types within the archive; it ignores all other file types. The file names must be encoded in UTF-8. Files with names that include Japanese characters, for example, must be renamed before they are added to the ZIP file.
-  Discovery supports MacOS ZIP files only if they are generated by using a command such as: `zip -r my-folder.zip my-folder -x "*.DS_Store"`. ZIP files that are created by right-clicking a folder and clicking *Compress* are not supported.
-  PDF files that you upload as part of an archive file are not displayed in the advanced view for a query result that you open from the *Improve and customize* page. If you want the file to be viewable from the advanced view, reimport the PDF file separately from the archive file.

When you add files to a Document Retrieval for Contracts project type, any file types that support SDU and OCR are processed with a pretrained Smart Document Understanding model and Optical Character Recognition automatically.
{: note}

## Document limits
{: #collections-doc-limits}

The number of documents that are allowed per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

The document limit applies to the number of documents in the index. Upload fewer documents at the start if the enrichments that you plan to apply might increase the number of documents later. For example, the following configurations generate more documents:

- Splitting documents segments one document into multiple documents
- Applying FAQ extractions produces one document for each question-and-answer pair that is found
- CSV files that you upload generate one document per line
- Database data sources that you crawl produce one document per database row
- Each object that is defined in an array in a JSON file results in a separate document

| Plan | Documents per service instance |
|------|-------------------------------:|
| Cloud Pak for Data |          Unlimited |
| Premium      |                Unlimited |
| Enterprise |                  Unlimited |
| Plus (includes Trial) |         500,000 |
{: caption="Number of documents per service instance" caption-side="top"}

The maximum allowed number can vary slightly depending on the size of the documents. Use these values as a general guideline.
{: note}

## File size limits
{: #collections-file-size-limits}

### Crawled documents

The maximum size of each file that you can crawl by using a connector differs by deployment type.

![IBM Cloud only](images/ibm-cloud.png) Managed deployments on {{site.data.keyword.cloud_notm}}
    
-   Premium plans only:

    -   Box: 50 MB
    -   IBM Cloud Object Store: 50 MB
    -   Salesforce Files objects: 50 MB
    -   All other data sources: 10 MB

-   All other plans: 10 MB

![Cloud Pak for Data only](images/desktop.png) Installed deployments on {{site.data.keyword.icp4dfull_notm}}

-   All data sources: 32 MB

### Uploaded documents

The size of each file that you can upload depends on your {{site.data.keyword.discoveryshort}} plan type. See the *Maximum document size table for details.

| Plan | File size per document |
|--------------|--------------------------------:|
| Cloud Pak for Data |                     50 MB |
| Premium      |                           50 MB |
| Enterprise |                             10 MB |
| Plus (includes Trial)         |          10 MB |
{: caption="Maximum document size" caption-side="top"}

## Field limits
{: #collections-field-limits}

When a document is added to a collection, content from the document is evaluated and added to the appropriate fields in an internal index.

You cannot assign the data type, such as Date or String, of a field. The data type is detected automatically and assigned to the field during document ingestion. The assignment is based on the data type that is detected from the first document that is indexed. Ingestion errors can occur in subsequent documents if a different data type is detected for the value in the same field. Therefore, if your documents have a mix of data types in a single field, first ingest the document that has a value with the most flexible data type, such as String, in the field.

When you crawl a website or upload an HTML file, the HTML content is added to the collection and indexed in an `html` field.

The following table shows the maximum size limit for fields per document.

| Field type | Maximum allowed size per document |
|------------|----------------------------------:|
| `html` field | 5 MB |
| Sum of all other fields | 1 MB |
{: caption="Maximum field sizes" caption-side="top"}

If the maximum size of the fields in the document exceeds the allowed limits, they are treated as follows:

-   For a document with an oversized `html` field, all of the fields in the document are indexed except the `html` field. 

    For {{site.data.keyword.icp4dfull_notm}} version 4.0 and earlier, the entire document is not indexed.
    {: note}
-   For a document with oversized non-HTML fields, the document is not indexed.

If you are uploading a Microsoft Excel file and a message is displayed that indicates that the non-HTML field size limit is exceeded, consider converting the XLS file into a CSV file. When you upload a comma-separated value (CSV) file, each row is indexed as a separate document. As a result, no field size limits are exceeded.
{: tip}

For more information about how fields in uploaded files are handled, see [How fields are handled](/docs/discovery-data?topic=discovery-data-index-overview#field-name-limits).

{{site.data.content.data-sources-reuse}}

## Crawl schedule options
{: #crawlschedule}

When you create a collection, the initial crawl starts immediately. The frequency that you choose for the crawl schedule determines when the next crawl will start.

To create a crawl schedule, complete the following steps:

1.  In the in *Crawl schedule* section, choose a frequency.

    -   If you want to crawl every 12 hours or every 10 days, choose **Custom intervals**. You can schedule the crawler to run on a custom number of days, hours, or minutes.
    -   By default, the crawl is scheduled to start during off-peak hours.
    -   Do not set the interval to a frequency that is shorter than the time it takes for the crawl to finish.
    -   Do not configure multiple crawlers to run at short intervals.
    -   ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**: You can schedule the crawler to run at a specific day and time. This option is helpful if you want to avoid heavy load on a target system during business hours. If you specify an hour in the range 1 - 9, add a zero before the hour digit. You can schedule the crawl for `01:00 AM` on Saturdays, for example.
    -   If you open a collection in a time zone other than the one in which the collection was created, the Coordinated Universal Time (UTC) offset information is displayed.
1.  ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**: In **More scheduling settings**, choose the type of schedule to use to crawl the data source. 

    The choices for all of the connectors (except the *Web crawl* connector) are as follows:

    -   **Full crawling**: Recrawls the external data source to update documents in the collection.
    -   **Crawling updates (look for new, modified, and deleted contents)**: Only updates the collection if data in the external data source was added, modified, or deleted since the last crawl.
    -   **Crawling new and modified contents**: Only updates the collection if data in the external data source that was added or modified since the last crawl.
    
    **Web crawl connector only**: The *Web crawl* connector schedules crawls differently from the other connector types. For the *Web crawl* connector only, choose among the following options:

    -   To control the frequency of the crawls yourself, choose this option:

        **Full crawling**  
        
        When you choose a full crawl schedule type, the crawl occurs with the frequency that you specify in the *Crawl schedule* section of the page.

    -   To allow the system to manage the frequency of the crawls for you, choose one of the following options:

        **Crawling updates (look for new, modified, and deleted contents)** or **Crawling new and modified contents**

        When you choose a schedule type that crawls for updates or for new and modified contents, the frequency that you specify for the crawl schedule is ignored. The frequency with which each document is crawled is variable and is managed entirely by the service. And the frequency changes depending on how often changes are found in a document. For example, if 5 of the 10 documents in a collection changed by the end of the first crawl interval, then the frequency is automatically increased for those 5 documents. Currently, the highest frequency at which these self-managed refreshes can run is daily.

        You cannot interrupt the automated management of frequency and you cannot trigger a one-off crawl when these types of scheduled crawls are configured.

If you want to change the flexible crawl schedule settings later, you can go to the *Processing settings* page, edit the settings, and then click **Apply changes and reprocess**.

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}} only**: The next scheduled crawl is displayed on the Activity page.

If you change the schedule frequency, the next scheduled crawl time might not be what you expect. The crawls are set up to occur on a regular schedule at a specific time or day by default. For example, if you change the crawl schedule from weekly to monthly on 11 August, the next crawl might be scheduled for 31 August instead of 11 September. It is not scheduled for exactly a month from the day that you made the change. Instead, it is scheduled to run on the day that is designated as the default run day for the selected crawl frequency.

## Stopping a crawl
{: #collections-crawl-stop}

To stop a crawl, complete the following steps:

1.  Open the *Manage collections* page from the navigation panel.
1.  From the *Activity* page, if the crawl is not in progress, click **Recrawl** to start the crawl, and then click **Stop**.
    
    ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}} only**: After you stop a crawl, the crawl will not start again until you click **Recrawl** to restart it. When restarted, data from the data source is ingested from scratch, overwriting existing documents and adding new ones.
