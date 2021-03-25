---

copyright:
  years: 2020, 2021
lastupdated: "2021-03-25"

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

A project is a convenient way to build and manage your {{site.data.keyword.discoveryfull}} application. You can assign a *Project type* and connect your data to the project by creating a collection. After you have configured your project with enrichments and other improvement tools, you can choose which components you'd like to deploy.
{: shortdesc}

A sample project is available for you to explore and experiment with. For more information, see the [Getting started with the Watson Discovery Sample Project](/docs/discovery-data?topic=discovery-data-getting-started).
{: tip} 

To create a project:

1.  Open the *Projects* page by selecting **My Projects**.
1.  Click **New project**. Name your project, and then choose a project type.

    The project type options are as follows:

    - Document Retrieval

      ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: If your data source contains contracts, choose this type, and then select **Apply contracts enrichment**.
      {: important}

      ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: If you installed the add-on, then the project will have contract enrichments applied to it automatically.
    - Conversational Search
    - Content Mining
    - Custom

    For more information about each type, see [Project types](#project-type).

1.  Click **Next**.
1.  Choose and configure a data source or connect to an existing collection.

    For more information about the types of data sources that are supported, see [Creating collections](/docs/discovery-data?topic=discovery-data-collections).

    The Document Retrieval and Custom project types can contain up to 5 collections. A Conversational Search project can contain 5 collections but only 1 collection is used by the {{site.data.keyword.conversationshort}} search skill. A Content Mining project can contain only 1 collection.
    {: note}


To view all the collections in your project, or add a new collection, open the **Manage collections** page from the navigation panel. For more information, see [Managing collections](/docs/discovery-data?topic=discovery-data-collections).

Take advantage of the following resources: 

- To open the product documentation, select the **Help** ![Help icon](images/help_icon.png) icon from the page header.
- To see all of your projects, click **My projects**.
- ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: To view the total number of documents and collections in your environment, select the **Environment details** ![Environment details icon](images/env_icon.png) icon.

  *Environment* refers to the {{site.data.keyword.discoveryshort}} instance that you provisioned in {{site.data.keyword.icp4dfull_notm}}.
  {: tip}

## Project types
{: #project-type}

<!-- c/s help for the *Project types* page. Do not delete. -->

Choose a project type to get the right set of enrichments applied to your documents automatically. The set of improvement tools that are available can differ by project type, and the available deployment methods are optimized for each use case.

The available types include:

- [Document Retrieval](#doc-retrieval)
- [Conversational Search](#conversational)
- [Content Mining](#mining)
- [Custom](#custom)

For more information about the different settings that are applied to each project type, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults).

### Document Retrieval
{: #doc-retrieval}

Use this project type to search and find the most relevant answers from your data. Projects of this type are typically deployed as search field components that are added to websites or other applications.

Documents that you add to a project of this type are automatically enriched in the following ways:

- Entities, such as proper nouns, are identified and tagged.
- Parts of speech are identified and tagged.

This tagged information is used later when a natural language phrase is submitted as a search query to return a smarter response.

#### Adding contract understanding
{: #doc-retrieval-contracts}

If you are working with legal documents or contracts in particular, enable the Content Intelligence feature.

- ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Create a Document Retrieval project, and then select **Apply contracts enrichment**.
- ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: Install the add-on.

In addition to the enrichments that are applied to a typical document retrieval project, the following enrichments are made automatically:

- Content from tables in the source document is tagged so it can be found later.
- Contract details, such as payment terms or parties involved in the contract, are identified and tagged.

For any collection that you add to the project, optical character recognition (OCR) is enabled so that text from scanned documents or other images are processed automatically.

For more information about this type of project, see [{{site.data.keyword.discoveryshort}} for Content Intelligence](/docs/discovery-data?topic=discovery-data-output_schema).

### Conversational Search
{: #conversational}

The *Conversational Search* project makes information from a connected data collection available as the source for answers that a chatbot returns to customers.

Use {{site.data.keyword.conversationfull}} and {{site.data.keyword.discoveryshort}} together to give your virtual assistant access to technical content and other knowledge base resources without needing to relocate or copy your corporate data. The built-in synchronization capabilities mean that your assistant always has the most up-to-date information available. The assistant that uses this project can be deployed to various platforms, including your company website.

The documents that you add to this type of project are not enriched automatically. However, consider enabling the *FAQ extraction* feature when you add a collection. The FAQ extraction feature runs additional processes to identify and tag clear question and answer pairs in your data source. This additional step makes it easier for a virtual assistant to return a concise and accurate answer in response to a question that is the same or similar to its pair.

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Another feature to consider enabling is the *Emphasize the answer* beta feature. When enabled, the answers that are returned to customers who  interact with the assistant show the exact answer highlighted in bold font within the search response. For more information about how the exact answer is determined, see [Answer finding](/docs/discovery-data?topic=discovery-data-query-parameters#answer-finding).

For more information about building a {{site.data.keyword.conversationshort}} search skill, see the appropriate documentation for your deployment:

- ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: [Creating a search skill](/docs/assistant-data?topic=assistant-data-skill-search-add).
- ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: [Embedding existing help content](/docs/assistant?topic=assistant-skill-search-add)

### Content Mining
{: #mining}

Use this project type to discover hidden insights, trends, and relationships in your data.

You can add only one collection to a project of this type.
{: note}

Documents that you add are automatically enriched in the following way:

- Parts of speech are identified and tagged.

A full-featured application is provided that you can use to use to research your data in depth. For more information about using the application, see [Using the deployed Content Mining application](/docs/discovery-data?topic=discovery-data-contentminerapp).

### Custom
{: #custom}

Choose this type if you prefer not to use one of the other project types. No enrichments are applied automatically, so you can add only those enrichments that are necessary for your use case.