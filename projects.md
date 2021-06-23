---

copyright:
  years: 2020, 2021
lastupdated: "2021-06-21"

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

A project is a convenient way to collect and manage the resources in your {{site.data.keyword.discoveryfull}} application. You can assign a *Project type* and connect your data to the project by creating a collection.
{: shortdesc}

Before you create a project, decide which project type best fits your needs.

| Need | Goal | Project type |
|--------------------|------|--------------|
| *Which document contains the answer to my question?* | Find meaningful information in sources that contain a mix of structured and unstructured data, and surface it in a stand-alone enterprise search application or in the search field of a business application. | **Document Retrieval** |
| *Where is the part of the contract that I need for my task?* | Quickly extract critical information from contracts. | **Document Retrieval for Contracts** |
| *I want the chatbot I'm building to use knowledge that I own* | Give a virtual assistant quick access to technical information that is stored in various external data sources and document formats to answer customer questions. | **Conversational Search** |
| *I want to uncover insights I didn't know to ask about.* | Gain insights from pattern analysis or perform root cause analysis. | **Content Mining** |
{: caption="Project type use cases" caption-side="top"}

To create a project, complete the following steps:

1.  Open the *Projects* page by selecting **My Projects**.
1.  Click **New project**. Name your project, and then choose the project type.

    For more information about each type, see [Project types](#project-type).

    Otherwise, choose **None of the above** and a *Custom* project type is created for you.

1.  ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}** only: If you choose a *Document Retrieval* project type and your data sources are in English, decide whether to enable the Content Intelligence feature.

    If your data source contains contracts, enable the feature by selecting **Apply contracts enrichment**. Scroll to see the checkbox, if necessary.

    ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}** only: If you enabled the Content Intelligence feature when you installed the {{site.data.keyword.discoveryshort}} service, then the contract enrichment is applied to it automatically. No action is required.
    {: note}
1.  Click **Next**.
1.  Choose and configure a data source or connect to an existing collection.

    For more information about supported data sources, see [Creating collections](/docs/discovery-data?topic=discovery-data-collections).

Take advantage of the following resources that are available from the page header: 

- To open the product documentation, select the **Help** ![Help icon](images/help_icon.png) icon.
- To see all of your projects, click **My projects**.

## Project types
{: #project-type}

<!-- c/s help for the *Project types* page. Do not delete. -->

Choose a project type to get the correct set of enrichments applied to your documents automatically. The improvement tools that are available differ by project type, as do the deployment methods, which are optimized for each use case.

The following project types are available:

- [Document Retrieval](#doc-retrieval)
- [Document Retrieval for Contracts](#doc-retrieval-contracts) ![Premium plan](images/Premium.png) ![Cloud Pak for Data](images/cp4d.png)
- [Conversational Search](#conversational)
- [Content Mining](#mining) ![Premium plan](images/Premium.png) ![Cloud Pak for Data](images/cp4d.png)
- [Custom](#custom)

For more information about the different settings that are applied to each project type, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults).

### Document Retrieval
{: #doc-retrieval}

Use this project type to search and find the most relevant answers from your data. Projects of this type are typically deployed as search field components that are added to websites or other applications.

Documents that you add to a project of this type are automatically enriched in the following ways:

- Entities, such as proper nouns, are identified and tagged.
- Parts of speech are identified and tagged.

This tagged information is used later when a natural language phrase is submitted as a search query to return a smarter response.

A sample Document Retrieval project is available for you to explore. For more information, see [Getting started with the Watson Discovery Sample Project](/docs/discovery-data?topic=discovery-data-getting-started).
{: tip}

### Document Retrieval for Contracts ![Premium plan](images/Premium.png) ![Cloud Pak for Data](images/cp4d.png)
{: #doc-retrieval-contracts}

If you are working with English-language legal contracts, enable the Content Intelligence feature to apply a contracts enrichment that can recognize and tag contract-related concepts in your data. Use this project type to automate complex business processes, such as contract review and negotiation. This project type can help to increase productivity, minimize costs, and reduce your legal exposure.

Only users of installed deployments ({{site.data.keyword.icp4dfull_notm}}) or Premium plan managed deployments can create this type of project.
{: note}

In addition to the enrichments that are applied to a typical document retrieval project, the following enrichments are made automatically:

- Content from tables in the source document is tagged so that it can be found later.
- Contract details, such as payment terms or parties that are involved in the contract, are identified and tagged.

For any collection that you add to the project, optical character recognition (OCR) is enabled automatically so that text from scanned documents or other images is processed.

When you apply the contracts enrichment, you cannot use Smart Document Understanding to annotate documents. A pretrained SDU model that can recognize contract-related information is applied automatically. The Table understanding enrichment is automatically applied.
{: note}

- ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Create a Document Retrieval project, and then select **Apply contracts enrichment**.
- ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: Enable the Content Intelligence feature when you install the {{site.data.keyword.discoveryshort}} service

For more information, see [Understanding contracts](/docs/discovery-data?topic=discovery-data-contracts-schema).

### Conversational Search
{: #conversational}

The *Conversational Search* project returns information from a connected data collection as answers to questions that customers ask a chatbot, which is also known as an *assistant*.

Use {{site.data.keyword.conversationfull}} and {{site.data.keyword.discoveryshort}} together to give your assistant access to technical content and other knowledge base resources without having to relocate or copy your corporate data. The built-in synchronization capabilities mean that your assistant can share the most up-to-date information available. Use the integrations that are provided with {{site.data.keyword.conversationshort}} to deploy an assistant that connects to this project to various platforms, including your company website, in minutes.

The documents that you add to this type of project are not enriched automatically.

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}} only**:

- Consider enabling the *FAQ extraction* feature when you add a collection. The FAQ extraction feature runs extra processes to identify and tag clear question-and-answer pairs in your data source. This additional step makes it easier for a virtual assistant to return a concise and accurate answer in response to a question that is the same or similar to its pair.
- Another feature to consider enabling is the *Emphasize the answer* beta feature. When enabled, the answers that are returned to customers who interact with the assistant show the exact answer highlighted in bold font within the search response. For more information about how the exact answer is determined, see [Answer finding](/docs/discovery-data?topic=discovery-data-query-parameters#answer-finding).

For more information about building a {{site.data.keyword.conversationshort}} search skill, see the appropriate documentation for your deployment:

- ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: [Creating a search skill](/docs/assistant-data?topic=assistant-data-skill-search-add).
- ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: [Embedding existing help content](/docs/assistant?topic=assistant-skill-search-add)

### Content Mining ![Premium plan](images/Premium.png) ![Cloud Pak for Data](images/cp4d.png)
{: #mining}

Use this project type to discover hidden insights, trends, and relationships in your data.

Only users of installed deployments ({{site.data.keyword.icp4dfull_notm}}) or Premium plan managed deployments can create this type of project.
{: note}

This project type is especially useful for analyzing structured data, such as data that you add by uploading a CSV file or by connecting to a database data source. You can add only one collection to a project of this type from the {{site.data.keyword.discoveryshort}} user interface.

Documents that you add as part of the initial collection are automatically enriched in the following way:

- Parts of speech are identified and tagged.

After you add a collection and optionally apply more enrichments to the data, a full-featured application is available for you to deploy. You can use the application to research your data in depth. For more information about using the application, see [Using the deployed Content Mining application](/docs/discovery-data?topic=discovery-data-contentminerapp). 

You can create a collection (CSV file only) from the deployed Content Mining application. The collection that you create is not added to your existing Content Mining project. A new Content Mining project is created to store the collection.
{: note}

### Custom
{: #custom}

Choose this type if you prefer not to use one of the other project types. No enrichments are applied automatically, so you can add only those enrichments that are necessary for your use case.

## Project limits
{: #projects-limits}

The number of projects you can create depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Projects per service instance |
|--------------|--------------------------------:|
| Cloud Pak for Data |                       300 |
| Premium      |                             100 |
| Plus (includes Trial) |                     20 |
{: caption="Plan details" caption-side="top"}

The Sample project is excluded from the total number of projects.
