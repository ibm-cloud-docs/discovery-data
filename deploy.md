---

copyright:
  years: 2019, 2021
lastupdated: "2021-11-03"

keywords: ui components, launch application, deploy, publish

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Deploying your project
{: #deploy}

<!-- c/s help for the *Integrate and deploy* page. Do not delete. -->

Deploy your project to start gaining new insights from your data.
{: shortdesc}

The method that you use to deploy your project differs by project type.

- [Document Retrieval and Custom projects](#dr-deploy)
- [Conversational Search projects](#cs-deploy)
- [Content Mining projects](#cm-deploy)

## Deploying a Document Retrieval project
{: #dr-deploy}

Work with a developer to build a custom search application or use the pre-built UI components that are provided by IBM.

For more information about building your own, see the [Building custom applications with the API](/docs/discovery-data?topic=discovery-data-api-use).

For Document Retrieval and Custom (the type assigned to projects when you do not apply a specific project type) projects, a set of user interface components are available for your use. The following table describes them.

| UI component | Illustration | Description | Storybook link |
|--------------|--------------|-------------|----------------|
| Search bar | ![Search bar type ahead](images/search-bar-example.png) | A search box that uses a natural language understanding query to fetch the most relevant results. | [Try it](https://watson-developer-cloud.github.io/discovery-components/storybook/?path=/story/searchinput--default){: external} |
| Search results | ![Search results list](images/search-results-example.png) | A set of results that rank the most relevant passages and tables to a query. | [Try it](https://watson-developer-cloud.github.io/discovery-components/storybook/?path=/story/searchresults--default){: external} |
| Facets | ![Facets](images/search-facets-example.png) | Refine your results with facets that help users filter the search results by specific categories and domains. | [Try it](https://watson-developer-cloud.github.io/discovery-components/storybook/?path=/story/searchfacets--default){: external} |
| Document preview | ![Document preview](images/search-doc-preview-example.png) | Displays your results in a document preview. This view helps you to see search results by highlighting passages within the text of the original document, which makes the context clearer. The preview is available for the following types of source documents: Excel, PDF, PowerPoint, Word, and all image files. (For more information about the supported image files, see [supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).) | [Try it](https://watson-developer-cloud.github.io/discovery-components/storybook/?path=/story/documentpreview--default){: external} |
{: caption="Available UI components" caption-side="top"}

To deploy your project, complete the following steps:

1.  To use the API, you need to know the project ID for your project. Go to the **Integrate and Deploy** > **API Information** page.
1.  From the **Integrate and Deploy** > **UI Components** page, find links to resources that a developer can use to get started.

    - [GitHub](https://github.com/watson-developer-cloud/discovery-components#using-discovery-components){: external}
    - [Storybook](https://watson-developer-cloud.github.io/discovery-components/storybook/){: external}

## Deploying a Document Retrieval for Contracts project
{: #dr-contracts-deploy}

The original documents are displayed in a browser, regardless of the source format. In addition, key elements of the documents are recognized and you can navigate to them quickly. For example, if you are searching for the `payment terms` clauses in a contract, the preview detects those clauses and highlights the passages. For more information, see [Understanding contracts](/docs/discovery-data?topic=discovery-data-contracts-schema).

## Deploying a Conversational Search project
{: #cs-deploy}

To deploy your project, connect this project to an assistant that is built with {{site.data.keyword.conversationshort}}. The general steps to follow include:

1.  Create an assistant.

    You can use a {{site.data.keyword.conversationshort}} Trial plan for testing purposes.
1.  Add a search skill to your assistant, and then connect it to this project.
1.  Deploy your assistant.

    For more information about building a {{site.data.keyword.conversationshort}} search skill, see the appropriate documentation for your deployment:

    -   ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: [Creating a search skill](/docs/assistant-data?topic=assistant-data-skill-search-add).
    -   ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: [Embedding existing help content](/docs/assistant?topic=assistant-skill-search-add){: external}

        From the {{site.data.keyword.conversationshort}} new experience, see [Adding a search integration](/docs/watson-assistant?topic=watson-assistant-search-add){: external}
        {: beta}

## Deploying a Content Mining project
{: #cm-deploy}

For content mining use cases, deploying the project is just the beginning. Use the deployed application to analyze your documents and find patterns and anomalies in your data. {{site.data.keyword.discoveryshort}} provides a full-featured application for you to use for this purpose. The Content Mining application is a web application that is hosted on an IBM site.

To deploy your project, complete the following steps:

1.  Go to the **Integrate and Deploy** > **Launch application** page.
1.  Click **Launch**.

For more information about how to use the application, see [Using the Content Mining application](/docs/discovery-data?topic=discovery-data-contentminerapp).
