---

copyright:
  years: 2020, 2024
lastupdated: "2024-03-05"

keywords: projects, project types

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Creating projects
{: #projects}



A project is a convenient way to collect and manage the resources in your {{site.data.keyword.discoveryfull}} application. You can assign a *Project type* and connect your data to the project by creating a collection.
{: shortdesc}

Before you create a project, decide which project type best fits your needs.

{{site.data.content.projects-reuse}}

If you created the {{site.data.keyword.discoveryshort}} service as part of a {{site.data.keyword.icp4dfull_notm}} as a Service deployment, the {{site.data.keyword.discoveryshort}} project is separate and distinct from the deployment project that is displayed in {{site.data.keyword.cloud_notm}}.
{: note}

To create a project, complete the following steps:

1.  Open the *Projects* page by selecting **My Projects**.
1.  Click **New project**. Name your project, and then choose the project type.

    For more information about each type, see [Project types](#project-type).

1.  If you choose a *Document Retrieval* project type and your data sources are in English, decide whether to enable the Content Intelligence feature.

    If your data source contains contracts, enable the feature by selecting **Apply contracts enrichment**. Scroll to see the checkbox, if necessary.

1.  Click **Next**.
1.  Choose and configure a data source.

    For more information about supported data sources, see [Creating collections](/docs/discovery-data?topic=discovery-data-collections).

Take advantage of the following resources that are available from the page header:

- To open the product documentation, click the Help icon ![Help icon](images/help.svg).
- To see all of your projects, click **My projects**.

## Project types
{: #project-type}



Choose a project type to get the correct set of enrichments applied to your documents automatically. The improvement tools that are available differ by project type, as do the deployment methods, which are optimized for each use case.

The following project types are available:

-    [Intelligent Document Processing](#doc-idp) [IBM Cloud]{: tag-ibm-cloud}
-    [Document Retrieval](#doc-retrieval)
-    [Document Retrieval for Contracts](#doc-retrieval-contracts)
-    [Conversational Search](#conversational)
-    [Content Mining](#mining)
-    [Custom](#custom)

### Intelligent Document Processing [IBM Cloud]{: tag-ibm-cloud}
{: #doc-idp}

Use this project type to understand quickly what data {{site.data.keyword.discoveryshort}} has extracted from your documents. You can view the extracted data in a rich document preview (default view is **PDF**). If the extracted data does not meet your requirements, you can apply enrichments to improve the data.

This project type is available from IBM Cloud-managed instances only.
{: note}

Documents that you add to a project of this type are automatically enriched in the following ways:

- Entities, such as proper nouns, are identified and tagged.

### Document Retrieval
{: #doc-retrieval}

Use this project type to search and find the most relevant answers from your data. Projects of this type are typically deployed as search field components that are added to websites or other applications.

Documents that you add to a project of this type are automatically enriched in the following ways:

- Entities, such as proper nouns, are identified and tagged.

This tagged information is used later when a natural language phrase is submitted as a search query to return a smarter response.

A sample Document Retrieval project is available for you to explore. For more information, see [Getting started with Watson Discovery](/docs/discovery-data?topic=discovery-data-getting-started).
{: tip}

### Document Retrieval for Contracts
{: #doc-retrieval-contracts}

If you are working with English-language legal contracts, enable the Content Intelligence feature to apply a contracts enrichment that can recognize and tag contract-related concepts in your data. Use this project type to automate complex business processes, such as contract review and negotiation. This project type can help to increase productivity, minimize costs, and reduce your legal exposure.

Only users of installed deployments ({{site.data.keyword.icp4dfull_notm}}) or Premium or Enterprise plan managed deployments can create this type of project.
{: note}

In addition to the enrichments that are applied to a typical document retrieval project, the following enrichments are made automatically:

- Content from tables in the source document is tagged so that it can be found later.
- Contract details, such as payment terms or parties that are involved in the contract, are identified and tagged.

For any collection that you add to the project, optical character recognition (OCR) is enabled automatically so that text from scanned documents or other images is processed.

When you apply the contracts enrichment, you cannot use Smart Document Understanding to annotate documents. A pretrained SDU model that can recognize contract-related information is applied automatically. The Table understanding enrichment is automatically applied.
{: note}

For more information, see [Understanding contracts](/docs/discovery-data?topic=discovery-data-contracts-schema).

### Conversational Search
{: #conversational}

The *Conversational Search* project returns information from a connected data collection as answers to questions that customers ask a chatbot, which is also known as an *assistant*.

Use {{site.data.keyword.conversationfull}} and {{site.data.keyword.discoveryshort}} together to give your assistant access to technical content and other knowledge base resources without having to relocate or copy your corporate data. The built-in synchronization capabilities mean that your assistant can share the most up-to-date information available. Use the integrations that are provided with {{site.data.keyword.conversationshort}} to deploy an assistant that connects to this project to various platforms, including your company website, in minutes.

The documents that you add to this type of project are not enriched automatically.

If you need to perform more complex searches from your virtual assistant, you might want to create a *Document Retrieval* project instead of *Conversational Search* project. For more information, see [Choosing the right project type for a chatbot](/docs/discovery-data?topic=discovery-data-chat-choose-project).

[IBM Cloud]{: tag-ibm-cloud} Another feature to consider enabling is the *Emphasize the answer* feature. When enabled, the answers that are returned to customers who interact with the assistant show the exact answer highlighted in bold font within the search response. For more information about how the exact answer is determined, see [Answer finding](/docs/discovery-data?topic=discovery-data-query-parameters#answer-finding).

For more information about building a {{site.data.keyword.conversationshort}} search skill, see the appropriate documentation for your deployment:

-   [IBM Cloud Pak for Data]{: tag-cp4d} [Adding a search integration](/docs/watson-assistant?topic=watson-assistant-search-add){: external}.
-   [IBM Cloud]{: tag-ibm-cloud} [Embedding existing help content](/docs/assistant?topic=assistant-skill-search-add){: external}

    From the classic {{site.data.keyword.conversationshort}} experience, see [Creating a search skill](/docs/assistant-data?topic=assistant-data-skill-search-add){: external}.
    {: note}

### Content Mining
{: #mining}

Use this project type to discover hidden insights, trends, and relationships in your data.

Only users of installed deployments ({{site.data.keyword.icp4dfull_notm}}) or Premium or Enterprise plan managed deployments can create this type of project.
{: note}

This project type is especially useful for analyzing structured data, such as data that you add by uploading a CSV file or by connecting to a database data source. You can add only one collection to a project of this type from the {{site.data.keyword.discoveryshort}} user interface.

Documents that you add as part of the initial collection are automatically enriched in the following way:

- Parts of speech are identified and tagged.

After you add a collection and optionally apply more enrichments to the data, a full-featured application is available for you to deploy. You can use the application to research your data in depth. For more information about using the application, see [Analyzing your data with the deployed Content Mining application](/docs/discovery-data?topic=discovery-data-contentminerapp).

From the Content Mining application, you can create the following enrichment types which are not available in other project types:

-   [Document classifier](/docs/discovery-data?topic=discovery-data-cm-doc-classifier)
-   [Phrase sentiment](/docs/discovery-data?topic=discovery-data-cm-phrase-sentiment)

You can create a collection from the deployed Content Mining application. The collection that you create is not added to your existing Content Mining project. A new Content Mining project is created to store the collection. The collection can contain an uploaded CSV file only. The project that is generated is given the name that you specify for the collection.
{: note}

Because the data that you add to this type of project is often structured, consider using the API to submit queries in the Discovery Query Language (DQL). With DQL queries, you can get information from specific fields or find specific enrichment type mentions. You cannot apply relevancy training to a *Content Mining* project.

### Custom
{: #custom}

Choose this type if you prefer not to use one of the other project types. No enrichments are applied automatically, so you can add only those enrichments that are necessary for your use case.

{{site.data.content.project-defaults-reuse}}

## Project limits
{: #projects-limits}

The number of projects you can create depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Projects per service instance |
|--------------|---------------------------------|
| Cloud Pak for Data |                 Unlimited |
| Premium      |                             100 |
| Enterprise |                               100 |
| Plus (includes Trial) |                     20 |
{: caption="Plan details" caption-side="top"}

The Sample project is excluded from the total number of projects.

## Renaming a project
{: #projects-rename}

You cannot rename the *Sample Project*.
{: note}

To rename a project after you create it, complete the following steps:

1.  Go to the *My Projects* page.
1.  Find the project that you want to rename, click the *Project actions* icon ![Overflow menu](images/overflow-menu-vertical.png), and then choose **Rename**.
1.  Edit the project name, and then click **Apply**.

## Deleting a project
{: #projects-delete}

If you want to delete a project, but keep a collection from the project, share the collection with another project before you complete these steps. From another project (a type that allows multiple collections), open the *Manage collections* tab. Click **New collection**, and then click **Reuse data from an existing collection**. Select the collection that you want to keep, and then click **Finish**.

You cannot delete the *Sample Project*.
{: note}

To delete a project, complete the following steps:

1.  Go to the *My Projects* page.
1.  Find the project that you want to delete, click the *Project actions* icon ![Overflow menu](images/overflow-menu-vertical.png), and then choose **Delete**.
1.  Click **Delete**.
