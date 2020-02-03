---

copyright:
  years: 2019
lastupdated: "2019-12-18"

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
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Creating projects
{: #projects}

<!-- c/s help for the *Projects* page. Do not delete. -->

A project is a convenient way to build and manage your {{site.data.keyword.discovery-data_long}} application. You can assign a **Project type** (`Document Retrieval`, `Conversational Search`, `Content Mining`, or `Custom`) and add data quickly by creating a collection, or reusing an existing one. After you have configured your project with enrichments and other improvement tools, you can choose which components you'd like to deploy.
{: shortdesc}

A sample project is available for you to explore and experiment with. For details, see the [Getting started with {{site.data.keyword.discovery-data_short}} tutorial](/docs/discovery-data?topic=discovery-data-getting-started). 

To create a project:

1.  Open the **Projects** page by selecting the **Projects** icon on the navigation panel.
1.  Select **New project**. Name your project and choose a **Project type**: `Document Retrieval`, `Conversational Search`, `Content Mining`, or `Custom`. 
1.  Click **Next**.
1.  Choose and configure a data source (see [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections)), or you can reuse an existing collection by selecting **Reuse data from an existing collection**. 

To keep track of collection sharing and clean up unused collections, select **Collection usage and sharing** on the **Projects** page. For more information see [Collection usage and sharing](/docs/discovery-data?topic=discovery-data-projects#collection-usage).

To view all the collections in your project, or add a new collection, select the **Manage collections** icon on the navigation panel. For more information, see [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections).

A **Document Retrieval**, **Conversational Search**, or **Custom** project type can contain a maximum of `5` collections. If the project type is **Content Miner**, the project can contain only `1` collection.
{: important}

**Tips**

Options available at the top of the tooling: 

-  To open the documentation, select the **Help** ![Help icon](images/help_icon.png) icon.
-  To view the available storage space and the number of documents and collections in your environment, select the **Environment details** ![Environment details icon](images/env_icon.png) icon. To delete all the collections in your environment, choose **Delete environment**.
-  To open the **IBM Cloud Pak for Data** hub, select **IBM Watson Discovery**.

## Project types
{: #project-type}

<!-- c/s help for the *Project types* page. Do not delete. -->

There are four available **Project types**: `Document Retrieval`, `Conversational Search`, `Content Mining`, or `Custom`. 

### Document Retrieval
{: #doc-retrieval}

Use this project type to search and find the most relevant answers from your data.

If you have purchased and installed {{site.data.keyword.discovery-data_short}} for Content Intelligence, you should use this **Project type**. For details see [{{site.data.keyword.discovery-data_short}} for Content Intelligence](/docs/discovery-data?topic=discovery-data-output_schema). 

#### Document retrieval defaults
{: #doc-retrieval-defaults}

-  **Settings**: Optical Character Recognition (OCR) `on` 
-  **Enrichments applied**: Entities, Parts of speech
-  **Improvement tools enabled**: Facets (by Entity), Dynamic Facets, Passages

Changing the Optical Character Recognition (OCR) setting to `off` will increase processing speed. For details see [Processing settings](/docs/discovery-data?topic=discovery-data-collections#processing-options).
{: note}

### Conversational Search
{: #conversational}

Use this project type to supply answers to a virtual agent built with {{site.data.keyword.conversationfull}} for {{site.data.keyword.icp4dfull}}. For more information about building a {{site.data.keyword.conversationfull}} search skill, see [Creating a search skill](/docs/assistant-data?topic=assistant-data-skill-search-add).

At this time, the {{site.data.keyword.conversationfull}} for {{site.data.keyword.icp4dfull}} search skill only supports one collection.
{: note}


#### Conversational Search defaults
{: #conversational-defaults}

-  **Settings**: Optical Character Recognition (OCR) `on`
-  **Enrichments applied**: None
-  **Improvement tools enabled**: Passages

Changing the Optical Character Recognition (OCR) setting to `off` will increase processing speed. For details see [Processing settings](/docs/discovery-data?topic=discovery-data-collections#processing-options).
{: note}


### Content Mining
{: #mining}

Use this project type to discover hidden insights, trends, and relationships in your data.

Each **Content Mining** project can contain only one collection.
{: note}

#### Content Mining defaults
{: #mining-defaults}

-  **Settings**: Optical Character Recognition (OCR) `on`
-  **Enrichment applied**: Parts of speech
-  **Improvement tools enabled**: None
-  **CSV settings**: No header, selected delimiters are comma and semicolon

Changing the Optical Character Recognition (OCR) setting to `off` will increase processing speed. For details see [Processing settings](/docs/discovery-data?topic=discovery-data-collections#processing-options).
{: note}


### Custom
{: #custom}

This option is for those who prefer not to use one of the other project types.

#### Custom defaults
{: #custom-defaults}

-  **Settings**: Optical Character Recognition (OCR) `on`
-  **Enrichments applied**: None
-  **Improvement tools enabled**: Passages

Changing the Optical Character Recognition (OCR) setting to `off` will increase processing speed. For details see [Processing settings](/docs/discovery-data?topic=discovery-data-collections#processing-options).
{: note}

## Collection usage and sharing
{: #collection-usage}

<!-- c/s help for the *Collection usage and sharing* page. Do not delete. -->

To access the **Collection usage and sharing** page, open the **Projects** page and select **Collection usage and sharing**.

Collections can be:

-  Associated with a single project
-  Shared by two or more projects
-  Not associated with any project. Collections not associated with a project can be deleted.

You can share collections across projects. The following is shared:

- The processed data
- Configured connector

If you make any of the following changes to a shared collection, *those changes will be applied to that collection in every project it is shared with*. These changes include:

-  Changing the **Run OCR (Optical Character Recognition)** setting
-  Annotating fields or adding fields using Smart Document Understanding
-  Enabling/disabling fields
-  Changing the setting for Document splitting
-  Changing any of the connector settings

The enrichments and other improvement tools are not included when a collection is shared, because they are set at the project level.
{: important}
