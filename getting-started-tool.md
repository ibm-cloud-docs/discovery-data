---

copyright:
  years: 2019, 2020
lastupdated: "2020-05-13"

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

# Getting started with the Watson Discovery for IBM Cloud Pak for Data Sample Project
{: #getting-started}

In this short tutorial, we introduce the {{site.data.keyword.discovery-data_short}} Sample Project. 
{: shortdesc}

The Sample Project is a great way to tour and try out {{site.data.keyword.discovery-data_short}} features. At any time, you can click **Restore project defaults** to start over.

## Before you begin
{: #before-you-begin-tool}
{: hide-dashboard}

Install {{site.data.keyword.discovery-data_short}}. See [Installing Discovery for Cloud Pak for Data](/docs/discovery-data?topic=discovery-data-install).

## Step 1: Open the Sample Project
{: #open-project-tool}

1.  Open the **Projects** page by selecting the **Projects** icon on the navigation panel. For more about projects, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).
1.  Select **Sample Project**. The **Improve and Customize** page opens. 

The [**Project type**](/docs/discovery-data?topic=discovery-data-projects#project-type) of the Sample project is **Document Retrieval**. **Document Retrieval** projects are used to search and find the most relevant answers from your data. It includes one collection that contains 40 documents.

**Document Retrieval** projects have the following defaults (we'll learn more about these later):
   -  **Settings**: Optical Character Recognition (OCR) `on` 
   -  **Enrichments applied**: Entities, Parts of speech
   -  **Improvement tools enabled**: Facets (by Entity), Dynamic Facets, Passages

A **Document Retrieval** project can contain a maximum of `5` collections.

There are three other **Project types**: **Conversational Search**, **Content Miner**, and **Custom**. 
{: tip}

## Step 2: Tour the Sample Project
{: #tour-project-tool}

Now that we've opened the Sample project and learned more about **Document Retrieval** projects, let's explore.

1.  Select the **Manage collections** icon on the navigation panel. Choose the **Sample Collection**. Several tabs display but we'll concentrate on a few.
    -  The **Activity** tab displays collection details: Number of documents, Collection status, Date of last update, an abbreviated list of **Warnings and errors** (to see the full list, select **View all**). For more information, see [Collection activity](/docs/discovery-data?topic=discovery-data-collections#collection-overview).
    -  The **Identify fields** tab is where you can annotate your document using [Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields). You can use the **Field labels** that are available or create your own.
    -  The **Manage fields** tab gives you the option to choose the fields you want to index, turn on document splitting, and set date formats. For more information, see [Managing fields](/docs/discovery-data?topic=discovery-data-configuring-fields#field-settings).
    -  The **Enrichments** tab displays the available enrichments (you can create more). By default, the enrichments already applied to this collection include **Entities** and **Parts of speech**. Click on **Fields to enrich** and you will notice that these enrichments are applied to the `text` field. To learn more about these enrichments, see [Extracting meaning](/docs/discovery-data?topic=discovery-data-create-enrichments#extract-meaning). You can also create enrichments that will add related terms (**Dictionary**), identify and extract values (**Character Pattern**), extract entities and relationships/apply rules to fields in your collection (**Machine Learning and Watson Explorer Content Analytics Studio models**), classify your documents into categories (**Classifier**), or use an **Advanced rule model**. See [Creating enrichments](/docs/discovery-data?topic=discovery-data-create-enrichments).   
1.  Select the **Integrate and Deploy** icon on the navigation panel. From here, you can share your project with colleagues and deploy. For more information, see [Building and deploying components](/docs/discovery-data?topic=discovery-data-deploy).
    -   The **Share preview** link tab makes it easy to share your project with others. Follow the instructions to add a user, then send those login credentials and the provided link to your colleague.
    -   The **Explore UI components** tab includes several componets: **Search bar**, **Search results**, **Facets**, and **Document preview**. The code for the {{site.data.keyword.discovery-data_short}} components can be found on [GitHub](https://github.com/watson-developer-cloud/discovery-components){: external}. You can learn more about the components and preview them in [Storybook](https://watson-developer-cloud.github.io/discovery-components){: external}.
1.  Select the **Improve and customize** icon on the navigation panel. The **Improve and Customize** page is where you can to try out queries, then add and test customizations to improve the query results for your project. For more information, see [Customizing and improving your project](/docs/discovery-data?topic=discovery-data-improve).
    - There are several example queries in the **Try an example to get started** section. For `Watson`, click the **Run search** button.
    - Two of the default **Improvement tools** for this project (Facets (by Entity) and Dynamic Facets) have identified facets (IBM, Watson, Kubernetes) you can filter on. Select a few and try them out. 
    - Query results display in the center pane. Another **Improvement tool**, passages, makes it possible to see the passages identified in the documents returned. Click **View passages in document** for the document preview. For more information about how passages are identified in natural language queries, see [Passages](/docs/discovery-data?topic=discovery-data-query-parameters#passages).
    -  On the **Improvement tools** panel, select the dropdowns to see what is available to further customize your project. There are five categories of tools: **Customize display**, **Search results**, **Teach domain concepts**, **Define structure**, and **Improve relevance**. For the full list of tools, see [Improvement tools](/docs/discovery-data?topic=discovery-data-improve#improvement-tools).
    
That's the tour, stay on the **Improve and Customize** page for the next step.
    
## Step 3: Customize the Sample Project
{: #customize-project-tool}

Now, let's customize a bit. Starting on the **Improve and Customize** page ...
1.  Enter the natural language query `How do I install IBM Cloud Pak for Data` in the query box.
1.  Review the query results displayed. View the source document for each result by clicking on **View* passage in document**.
1.  On the **Improvement tools** panel, choose **Customize display**, and select **Facets**. Select **New facet**, then click the **From existing fields in a collection** button. Choose `enriched_text.entities.type` from the dropdown and click **Apply**. The new facets will display. You can change the name of the facet label, and the filtering behavior.

## Step 4: Keep exploring and experimenting
{: #next-steps-tool}

Continue experimenting with the Sample project. A few other things you might want to try:
  -  Select the **Manage collections** icon on the navigation panel. Click the **New collection** button. Choose **Upload data** and create a new collection with a few of your own documents.
  -  Select the **Integrate and Deploy** icon on the navigation panel. On the **Share preview link** tab, copy the link and paste it in your browser to preview your application. On the **Explore UI components** tab, click the **Try it on Storybook** link for any of the components.
  -  Select the **Improve and customize** icon on the navigation panel. On the **Improvement tools** panel, select **Customize display**, then choose **Search results**. In the **Select field to display as titles**, choose `document_id` from the dropdown and click **Apply**. The document identifier in each search result will switch from the document name to the document id number.

When you are ready to start over, click **Restore project defaults** on the **Improve and Customize** page to restore the project defaults.
{: tip}


## Bonus: Handy tools at the top 
{: #handy-tools}

 -  To open the documentation, select the **Help** ![Help icon](images/help_icon.png) icon.
 -  To view the available storage space and the number of documents and collections in your environment, select the **Environment details** ![Environment details icon](images/env_icon.png) icon. To delete all the collections in your environment, choose **Delete environment**.
 -  To open the **IBM Cloud Pak for Data** hub, select **IBM Watson Discovery**.