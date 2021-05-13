---

copyright:
  years: 2019, 2021
lastupdated: "2021-05-13"

keywords: data sources, supported data sources

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

Creating a collection is a good way to group documents that you want to enrich in a similar way. For example, you might want to create a collection of documents that have a similar visual structure so that you can use the collection to define custom fields with the Smart Document Understanding tool. Or maybe you want to create a collection of documents that contain frequently asked questions that are formatted in a consistent manner so you can apply the FAQ extraction feature to the collection.

## Creating a collection
{: #createcollection}

When you create a collection, {{site.data.keyword.discoveryshort}} pulls documents from a data source, by using a process called crawling. Crawling is the process of systematically browsing and retrieving documents from a specified start location.

Before you can create a collection, you must create a project. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).

1.  To create a collection, open a project, go to the **Manage collections** page, and then click **New collection**.

    - The Document Retrieval and Custom project types can contain up to 5 collections. 
    - A Conversational Search project can contain 5 collections but only 1 collection is used by the {{site.data.keyword.conversationshort}} search skill. 
    - A Content Mining project can contain only 1 collection.
1.  Choose a data source type. A collection can support only one data source.

    You can connect to an external data source or perform a one-time document upload from your local file system.

    For external data sources, be prepared to provide details such as file locations or URLs, and any necessary credentials.
1.  Name your collection, and then choose the language of the collection. 

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Select the crawl schedule. 

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  Configure the data source.

    For more information, see the appropriate topic for your deployment:

    - [Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types)
    - [{{site.data.keyword.cloud_notm}} data sources](/docs/discovery-data?topic=discovery-data-sources)
    - [Uploading data](/docs/discovery-data?topic=discovery-data-upload-data)
1.  Click **Create collection** to start the crawl.

    The **Activity** page opens and shows the progress of the collection creation. Only [supported file types](/docs/discovery-data?topic=discovery-data-upload-data#supportedfiletypes) are crawled; all others are ignored.

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: The number of collections you can create depends on your hardware configuration. {{site.data.keyword.discoveryshort}} supports a maximum of 256 collections per instance and installation, but that number depends on many factors, including memory.
{: note}

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

This video provides an overview of connecting to data sources in {{site.data.keyword.discoveryshort}}. The available data sources vary by version:

![Watson Discovery Demo: Connect to the data source you want](https://www.youtube.com/embed/MPCOwMgn1p4){: video output="iframe"  data-script="none" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

To view the transcript, open the video on YouTube.

### Crawl schedule options
{: #crawlschedule}

When you create a collection, the initial crawl starts immediately. The frequency that you choose for the crawl schedule determines when the next crawl will start. 

To create a crawl schedule, complete the following steps:

1.  In the in *Crawl schedule* section, choose a frequency. 

    - If you want to crawl every 12 hours or every 10 days, choose **Custom intervals**. You can schedule the crawler to run on a custom number of days, hours, or minutes.
    - By default, the crawl is scheduled to start during off-peak hours.
    - ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.discovery-data_short}}**: You can schedule the crawler to run at a specific day and time. This option is helpful if you want to avoid heavy load on a target system during business hours. You can schedule the crawl for 01:00 AM on Saturdays, for example.

1.  ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.discovery-data_short}}**: In **More scheduling settings**, you can choose the type of update to make from the following options:

    - Crawling updates (look for new, modified, and deleted contents)
    - Crawling new and modified contents
    - Full crawling

If you want to edit your flexible crawl schedule settings, go to the *Processing settings* page, edit the settings, and click **Apply changes and reprocess**. If you open a collection in a time zone other than the one in which the collection was created, the Coordinated Universal Time (UTC) offset information is displayed.
