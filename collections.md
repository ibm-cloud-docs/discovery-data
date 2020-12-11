---

copyright:
  years: 2019, 2020
lastupdated: "2020-12-10"

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

<!-- c/s help for the *Manage collections* page. Do not delete. -->

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
   -  [{{site.data.keyword.cloud_notm}} data sources](/docs/discovery-data?topic=discovery-data-sources)
   -  [Uploading data](/docs/discovery-data?topic=discovery-data-collections#upload-data)
1. Select **Create collection**, which starts the crawling process. The **Activity** tab opens and updates as documents are added to the collection. The crawl syncs the data initially and updates periodically at the specified frequency.

This video provides an overview of connecting to data sources in {{site.data.keyword.discoveryshort}}. The available data sources vary by version:

![Watson Discovery Demo: Connect to the data source you want](https://www.youtube.com/embed/MPCOwMgn1p4){: video output="iframe" id="youtubeplayer" frameborder="0" width="560" height="315" webkitallowfullscreen mozallowfullscreen allowfullscreen}
</br>
To view the transcript, open the video on YouTube.

![Cloud Pak for Data only](images/cpdonly.png) The number of collections you can create depends on your hardware configuration. {{site.data.keyword.discoveryshort}} supports a maximum of 256 collections per instance and installation, but that number depends on many factors, including memory.
{: note}

To stop a crawler that is in progress, click **Stop**. You can only stop a crawler that is in progress, and the crawler is only stopped for the interval between clicking **Stop** and the next scheduled crawl. For example, if you specified an hourly crawl and you click **Stop**, the crawler stops for an hour and resumes crawling hourly.

If you want to access an existing collection, complete the following steps:

1. Select the **Manage collections** icon on the navigation panel. Existing collections display the document count and last updated date.
1. Select the collection you need. The **Activity** tab displays.

For information about creating a collection by using the API, see [Create a collection](https://{DomainName}/apidocs/discovery-data#createcollection){: external}.

### Supported file types and general requirements
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

\*\*\*Files within compressed archive files (ZIP, GZIP, TAR) are extracted. {{site.data.keyword.discoveryshort}} ingests the supported file types within them; it ignores all other file types. {{site.data.keyword.discoveryshort}} supports MacOS zip files only if they are generated by using a command such as: `zip -r my-folder.zip my-folder -x "*.DS_Store"`. Zip files created by right-clicking on a folder name and selecting `compress` are not supported. 

A connector is a component that provides data connectivity and extraction capabilities for external data sources. In {{site.data.keyword.discoveryshort}}, you establish a connector during the process of creating a collection for a data source. The following general requirements apply to all connectors:

-  Each collection can support only one data source.
-  Connectors are not available when you use the API.
-  You need the credentials and file locations, or URLs, for each data source, which a developer or system administrator of the data source typically provides.
-  You need to manually provide the resources to crawl. Auto discovery is not supported.

### Crawl schedule options
{: #crawlschedule}

When you create a collection, the initial crawl starts immediately. The frequency you choose for the crawl schedule determines when the next crawl starts in relation to the first. In the **How often would you like to crawl?** drop-down menu in **Crawl schedule**, you can schedule crawls to update at the following intervals:

-  **Hourly** - Runs every hour
-  **Daily** - Runs every day at the same time as the initial craw
-  **Weekly** - Runs every week on the same day and time as the initial crawl.
-  **Monthly** - Runs every 30 days at the same time as the initial crawl.
-  **Custom intervals** - Runs on a fixed schedule, for example every 12 hours or every 10 days. You can schedule the crawler to run on a custom number of **Minutes**, **Hours**, or **Days**.

   If you select **Custom intervals** and set the **Minutes** to `0`, the **Hours** to `0`, and the **Days** to `1`, this configuration is the same setting as the **Daily** crawl schedule, so if you click **Processing settings** in your collection during or after collection processing, you can see that the crawler schedule is set to **Daily**. Similarly, if you enter `0` for **Minutes**, `0` for **Hours**, and `30` for **Days**, this configuration is equivalent to setting a **Monthly** crawl schedule.

If you modify crawl settings on the **Processing settings** page and then click **Apply changes and reprocess**, the crawl restarts immediately. If you want to view the collection status, see the **Activity** tab.
{: note}

However, you might want your crawler to run on specific dates and times. For information about flexible crawl schedule settings, see [Flexible crawl schedule settings](/docs/discovery-data?topic=discovery-data-collections#flexible-crawl).

#### Flexible crawl schedule settings
{: #flexible-crawl}

![Cloud Pak for Data only](images/cpdonly.png)</br>

In your **Crawl schedule** settings and in **More scheduling settings**, you can set a flexible crawl schedule so that you have more control over when and how frequently your crawler runs by scheduling your crawler to run at specific times and dates.
{: shortdesc}

For example, if you want to avoid heavy load on a target system during business hours, you might want to use the flexible crawl schedule settings to run your crawler outside of business hours, for example at 10:00 PM on Fridays. If you select **Weekly** or **Monthly** in **How often would you like to crawl?**, you see the following option:

- **Specify days and time in week** (Available option when you select the **Weekly** crawl schedule) - You can schedule the crawler to run at the same time each week. When you enable this option, you can select a day or days and a time, in `HH:MM`, that the crawler runs each week, for example every Monday at 01:00 AM.
- **Specify dates and time in month** (Available option when you select the **Monthly** crawl schedule) - You can schedule the crawler to run on a certain date or dates and time of each month. When you enable this option, specify the date or dates that you want the crawler to run each month in **Dates**, and specify the time, in `HH:MM`, that the crawler runs on the specified dates in **Time**, for example every 5th of the month at 01:00 AM.

In **More scheduling settings**, you can choose from three options in **Schedule type** and specify the date and time for your custom crawler schedule. In **Schedule type**, you can select one of the following three options:

- **Crawling updates (look for new, modified, and deleted contents)**
- **Crawling new and modified contents**
- **Full crawling**

After you select your schedule type, specify the **Date and time for enabling this schedule**. If you open a collection in a time zone other than the one in which the collection was created, the UTC offset information is displayed in the **Processing settings** tab. If you want to edit your flexible crawl schedule settings, click the **Processing settings** tab, edit the settings, and click **Apply changes and reprocess**.

For regular crawl schedule settings, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).

## Uploading data
{: #upload-data}

Use this option to upload data you stored locally. Only documents supported by {{site.data.keyword.discoveryshort}} are crawled; all others are ignored. The file size limit for uploading data is 32MB.
{: shortdesc}

If you upload more than 200 files at one time, {{site.data.keyword.discoveryshort}} might be unable to process all of your files. Therefore, for optimal processing, consider uploading no more than 200 files. Otherwise, upload multiple smaller document sets, or use a data source crawler to process document sets that are larger than 200 files.
{: tip}

For a list of file types that you can upload to {{site.data.keyword.discoveryshort}}, see [Supported file types and general requirements](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes). After the upload begins, the **Activity** tab opens and updates as documents are added to the collection. Your collection is finished processing when the status indicates `Processing finished. Updated documents are ready for you.`.

Optional: Click **More processing settings** to expand the menu, and then click **Apply optical character recognition (OCR)**. By default, this option is set to **Off**. If you set it to **On**, {{site.data.keyword.discoveryshort}} extracts text from images, using Optical Character Recognition (OCR).

For additional information about supported data sources in {{site.data.keyword.discoveryshort}}, see the following links:
- ![Cloud Pak for Data only](images/cpdonly.png) [Configuring Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types)
- ![IBM Cloud only](images/cloudonly.png) [Configuring {{site.data.keyword.cloud_notm}} data sources](/docs/discovery-data?topic=discovery-data-sources)

## Managing collections
{: #manage-collections-public}

<!-- c/s help for the *Manage collections* page tabs: Activity, Processing settings, CSV settings. Do not delete. -->

Click on any collection on the **Manage collections** page to see the options for managing your collection. These tabs are available after collection processing finishes. The tabs contain data that is associated with your collection and options for managing it.
{: shortdesc}

**Activity** tab:

- The number of available documents and the number of documents that are processing
- The collection status. While syncing is in progress, the collection status states, `Sync in progress`. To recrawl your collection, edit the fields that are associated with the data source that you are connnecting to in {{site.data.keyword.discoveryshort}}. When collection processing completes, you receive a status message that states, `Your documents have finished processing! You can now work with your full data set.`.
- The last update date of the collection
- A list of warnings and errors that might appear while your collection processes, such as the affected file name and its associated document ID

**Identify fields** tab:

You can view any fields that the crawler identified from your data. You can annotate the fields in your documents. For more information, see [Identifying fields](/docs/discovery-data?topic=discovery-data-configuring-fields#identify-fields).

**Manage fields** tab:

The **Manage fields** tab contains the following options: **Fields to index**, **Improve query results by splitting your documents**, and **Date format settings**. For more information, see [Managing fields](/docs/discovery-data?topic=discovery-data-configuring-fields#field-settings)

**Enrichments** tab:

You can enrich fields in your collection with cognitive metadata. Many enrichments are available in {{site.data.keyword.discoveryshort}}. You must create some of the enrichments before you apply them. 

You can apply an enrichment to a field by selecting an enrichment, selecting the fields that you want to enrich in the drop-down menu of the chosen enrichment, and clicking **Apply changes and reprocess**.

For more information, see [Managing enrichments](/docs/discovery-data?topic=discovery-data-configuring-fields#enrich-fields).

**Processing settings** tab:

You can change the crawler schedule and your data source configuration settings. If you are uploading your own data, you can set the **Apply optical character recognition (OCR)** option to **On** or **Off**. If you select **Web crawl** and you already entered a start URL, you can access the **Crawl settings** dialog box by clicking the icon next to the delete icon. Both icons are located next to the start URL. In this dialog box, you can specify the **Maximum number of links to follow** or exclude URLs that include specific subdirectories in **Exclude URLs where the path includes**.

**CSV settings** tab:

If you upload CSV files, you can specify how these files are parsed by selecting a delimiter in **Column delimiter**. You can also specify an escape character in **Escape character**.

For information about creating a collection, see [Creating a collection](/docs/discovery-data?topic=discovery-data-collections).
