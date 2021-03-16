---

copyright:
  years: 2020, 2021
lastupdated: "2021-03-16"

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

# Creating projects
{: #projects}

<!-- c/s help for the *Projects* page. Do not delete. -->

A project is a convenient way to build and manage your {{site.data.keyword.discoveryfull}} application. You can assign a **Project type** (`Document Retrieval`, `Conversational Search`, `Content Mining`, or `Custom`) and add data quickly by creating a collection, or reusing an existing one. After you have configured your project with enrichments and other improvement tools, you can choose which components you'd like to deploy.
{: shortdesc}

A sample project is available for you to explore and experiment with. For more information, see the [Getting started with the Watson Discovery Sample Project](/docs/discovery-data?topic=discovery-data-getting-started).
{: tip} 

To create a project:

1.  Open the **Projects** page by selecting the **My Projects**.
1.  Select **New project**. Name your project and choose a **Project type**: `Document Retrieval`, `Conversational Search`, `Content Mining`, or `Custom`. 
1.  Click **Next**.
1.  Choose and configure a data source (see [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections)), or you can reuse an existing collection by selecting **Reuse data from an existing collection**. 

To keep track of collection sharing and clean up unused collections, complete the appropriate step for your deployment:
 
  - ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: Select **Collection usage and sharing**. 
  - ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Select **Data usage and GDPR**, then **Collection usage and sharing**.


To view all the collections in your project, or add a new collection, select the **Manage collections** icon on the navigation panel. For more information, see [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections).

A **Document Retrieval**, **Conversational Search**, or **Custom** project type can contain a maximum of `5` collections. If the project type is **Content Miner**, the project can contain only `1` collection.
{: important}

**Tips**

Options available at the top of the tooling: 

-  To open the documentation, select the **Help** ![Help icon](images/help_icon.png) icon.
-  To view the available storage space and the number of documents and collections in your environment, select the **Environment details** ![Environment details icon](images/env_icon.png) icon. To delete all the collections in your environment, choose **Delete environment**.
-  To open the **{{site.data.keyword.icp4dfull_notm}}** hub, select **IBM Watson Discovery**.
-  To return to the **My projects** page, click **My projects**.

## Project types
{: #project-type}

<!-- c/s help for the *Project types* page. Do not delete. -->

There are four available **Project types**: `Document Retrieval`, `Conversational Search`, `Content Mining`, or `Custom`. 

### Document Retrieval
{: #doc-retrieval}

Use this project type to search and find the most relevant answers from your data.

You should use this **Project type** for [{{site.data.keyword.discoveryshort}} for Content Intelligence](/docs/discovery-data?topic=discovery-data-output_schema) projects. 

#### Document retrieval defaults
{: #doc-retrieval-defaults}

-  **Settings**: Optical Character Recognition (OCR) `off` 
-  **Enrichments applied**: Entities, Parts of speech
-  **Improvement tools enabled**: Facets (by Entity), Dynamic Facets, Passages

Setting Optical Character Recognition (OCR) to `off` increases processing speed.

Document retrieval defaults for [{{site.data.keyword.discoveryshort}} for Content Intelligence](/docs/discovery-data?topic=discovery-data-output_schema):

- **Settings**: Optical Character Reader Advanced `on`
- **Enrichments applied**: Entities, Parts of speech, Table Understanding, and Contracts
- **Improvement tools enabled**: Facets (by Category, Nature, Contract Term, Contract Payment Term, Contract Type, Contract Currency, Invoice Buyer, Invoice supplier, Invoice Currency, Purchase Order Buyer, Purchase Order Supplier, Purchase Order Payment Term) and Table Retrieval

For additional default settings, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults).

### Conversational Search
{: #conversational}

Use this project type to supply answers to a virtual agent built with {{site.data.keyword.conversationfull}} for {{site.data.keyword.icp4dfull}}. For more information about building a {{site.data.keyword.conversationfull}} search skill, see [Creating a search skill](/docs/assistant-data?topic=assistant-data-skill-search-add).

#### Conversational Search defaults
{: #conversational-defaults}

-  **Settings**: Optical Character Recognition (OCR) `off`
-  **Enrichments applied**: None
-  **Improvement tools enabled**: Passages
-  **API enabled**: [Answer finding (beta)](/docs/discovery-data?topic=discovery-data-query-parameters#answer-finding) ![IBM Cloud only](images/cloudonly.png)

Setting Optical Character Recognition (OCR) to `off` increases processing speed.

For additional default settings, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults).


### Content Mining
{: #mining}

Use this project type to discover hidden insights, trends, and relationships in your data.

Each **Content Mining** project can contain only one collection.
{: note}

#### Content Mining defaults
{: #mining-defaults}

-  **Settings**: Optical Character Recognition (OCR) `off`
-  **Enrichment applied**: Parts of speech
-  **Improvement tools enabled**: None
-  **CSV settings**: No header, selected delimiters are comma and semicolon

Setting Optical Character Recognition (OCR) to `off` increases processing speed.

For additional default settings, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults).


### Custom
{: #custom}

This option is for those who prefer not to use one of the other project types.

#### Custom defaults
{: #custom-defaults}

-  **Settings**: Optical Character Recognition (OCR) `off`
-  **Enrichments applied**: None
-  **Improvement tools enabled**: Passages

Setting Optical Character Recognition (OCR) to `off` increases processing speed.

## Collection usage and sharing
{: #collection-usage}

<!-- c/s help for the *Collection usage and sharing* page. Do not delete. -->

To access the **Collection usage and sharing** page, open the **Projects** page, then:

  - ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: Select **Data usage**, then **Collection usage and sharing**. 
  - ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Select **Data usage and GDPR**, then **Collection usage and sharing**.

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

### API usage ![Cloud Pak for Data only](images/desktop.png)
{: #api-usage}

This information applies to {{site.data.keyword.discovery-data_short}} only.
{: important}

To access the **API usage** page: open the **Projects** page, select **Data usage**, then **API usage**.

This page is used to monitor the usage of the Analyze API, which supports stateless document ingestion workflows. For more information, see [Analyze API](/docs/discovery-data?topic=discovery-data-analyzeapi).

-  **Start date**: The start date of the API call monitoring period.
-  **End date**: The end date of the API call monitoring period.
-  **30-day call total**: This number indicates the number of calls to the Analyze API in the 30-day time interval indicated by the **Start date** and **End date**. The 30-day time interval displayed is determined by calculating the consecutive time period with the highest number of API calls. The 30-day window will update as the time interval with the highest number of API calls changes. 

The **API usage** will not be displayed until some time after API usage monitoring begins. There might be a delay in displaying the final total number of the **30-day call total**, even if the 30-day period listed includes the current date.
{: note}

### GDPR data label ![IBM Cloud only](images/ibm-cloud.png)
{: #project-gdpr}

This information applies to {{site.data.keyword.discoveryshort}} Premium instances that are hosted on {{site.data.keyword.cloud_notm}} only.
{: important}

To access the **GDPR data label** page: open the **Projects** page, select **Data usage and GDPR**, then **GDPR data label**.

For more information about GDPR and labeling data in the {{site.data.keyword.discoveryshort}} tooling, see [European Union General Data Protection Regulation (GDPR)](/docs/discovery-data?topic=discovery-data-information-security#gdpr).