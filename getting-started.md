---

copyright:
  years: 2019, 2021
lastupdated: "2021-08-05"

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

# Getting started with the Watson Discovery Sample Project
{: #getting-started}

In this short tutorial, we introduce the {{site.data.keyword.discoveryshort}} Sample Project. The Sample Project is a great way to tour and try out {{site.data.keyword.discoveryshort}} features.
{: shortdesc}

This information applies to {{site.data.keyword.discovery-data_short}}, Plus plan instances, and Premium plan instances that were created on {{site.data.keyword.cloud_notm}} after 16 July 2020. For Premium instances that were created before that date and for all Lite and Advanced plans, see [Getting started with Discovery](/docs/discovery?topic=discovery-getting-started){: external}.
{: important}

## Before you begin
{: #before-you-begin-tool}
{: hide-dashboard}

Choose the appropriate step to complete for your deployment:

- ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: Install {{site.data.keyword.discoveryshort}}. See [Installing Discovery for Cloud Pak for Data](/docs/discovery-data?topic=discovery-data-install).
- ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Complete the following steps:

  - Sign up for a {{site.data.keyword.cloud_notm}} account or log in.
  - You can use a Plus plan for 30 days at no cost. However, to create a Plus plan instance of the service, you must have a paid account. For more information about creating a paid account, see [Upgrading your account](/docs/account?topic=account-upgrading-account){: external}. And, if you decide not to continue using the Plus plan and don't want to pay for it, delete the service instance before the 30-day trial period ends.
  - Go to the [{{site.data.keyword.discoveryshort}} resource](https://cloud.ibm.com/catalog/services/watson-discovery){: external} page in the {{site.data.keyword.cloud_notm}} catalog and create a Plus plan service instance.

## Step 1: Open Watson Discovery
{: #getting-started-launch-tool}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**

{{site.data.keyword.discoveryshort}} installed on {{site.data.keyword.icp4dfull}} 4:

1.  From the {{site.data.keyword.icp4dfull_notm}} web client main menu, expand **Services**, and then click **Instances**.
1.  Find your instance, and then click it to open its summary page.
1.  Click **Launch tool**.

{{site.data.keyword.discoveryshort}} installed on {{site.data.keyword.icp4dfull}} 3.0.1 or later:

1.  From the {{site.data.keyword.icp4dfull_notm}} web client menu, choose **My Instances**.
1.  Select your {{site.data.keyword.discoveryshort}} instance.
1.  Click **Launch tool**.

{{site.data.keyword.discoveryshort}} installed on {{site.data.keyword.icp4dfull}} 2.5.0.0:

1.  From the {{site.data.keyword.icp4dfull_notm}} web client menu, choose **My Instances**.
1.  On the **Provisioned instances** tab, find your {{site.data.keyword.discoveryshort}} instance, and then hover over the last column to display the ellipsis icon ![Ellipsis icon](images/cp4d-sideways-kebab.png) and choose **View details**.
1.  Click **Open Watson Discovery**.


![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**

1.  {: hide-dashboard} Click the {{site.data.keyword.discoveryshort}} instance you created to go to the service dashboard.
1.  {: hide-dashboard} On the **Manage** page, click **Launch Watson Discovery**. If you're prompted to log in to the tooling, provide your {{site.data.keyword.cloud_notm}} credentials.


## Step 2: Open the Sample Project
{: #open-project-tool}

1.  Open the **Projects** page by selecting **My Projects**. 

    For more information about projects, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).
1.  Select **Sample Project**. 

    The **Improve and Customize** page opens.

If you just installed {{site.data.keyword.discoveryshort}}, the Sample Project will need time to finish processing documents. Wait until processing is complete to start experimenting. You can confirm that all 40 documents have finished processing by selecting the **Manage collections** icon on the navigation panel and checking the **Sample Collection**.
{: note}

The Sample Project is a *Document Retrieval* project. Document Retrieval projects are used to search and find the most relevant answers from your data. It includes one collection that contains 40 documents.

## Step 3: Tour the Sample Project
{: #tour-project-tool}

Now that we've opened the Sample Project and learned more about **Document Retrieval** projects, let's explore.

1.  Select the **Manage collections** icon on the navigation panel. Choose the **Sample Collection**. Several tabs display but we'll concentrate on a few.

    - The **Activity** tab displays collection details: Number of documents, Collection status, Date of last update, an abbreviated list of **Warnings and errors** (to see the full list, select **View all**).
    - The **Identify fields** tab is where you can annotate your document using [Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields). You can use the **Field labels** that are available or create your own.
    - The **Manage fields** tab gives you the option to choose the fields you want to index, turn on document splitting, and set date formats. For more information, see [Managing fields](/docs/discovery-data?topic=discovery-data-configuring-fields#field-settings).
    - The **Enrichments** tab displays the available enrichments (you can create more). By default, the enrichments already applied to this collection include **Entities** and **Parts of speech**. Click on **Fields to enrich** and you will notice that these enrichments are applied to the `text` field. To learn more about these enrichments, see [Apply prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu). You can also create enrichments that will add related terms (**Dictionary**), identify and extract values (**Regular expressions**), extract entities and relationships/apply rules to fields in your collection (**Machine Learning and Watson Explorer Content Analytics Studio models**), classify your documents into categories (**Classifier**), or use an **Advanced rule model**. See [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain).   
1.  Select the **Integrate and Deploy** icon on the navigation panel. From here, you can share your project with colleagues and deploy. For more information, see [Building and deploying components](/docs/discovery-data?topic=discovery-data-deploy).

    - The **Share preview** link tab makes it easy to share your project with others. Follow the instructions to add a user, then send those login credentials and the provided link to your colleague.
    - The **Explore UI components** tab includes several componets: **Search bar**, **Search results**, **Facets**, and **Document preview**. The code for the {{site.data.keyword.discoveryshort}} components can be found on [GitHub](https://github.com/watson-developer-cloud/discovery-components){: external}. You can learn more about the components and preview them in [Storybook](https://watson-developer-cloud.github.io/discovery-components){: external}.
1.  Select the **Improve and customize** icon on the navigation panel. The **Improve and Customize** page is where you can to try out queries, then add and test customizations to improve the query results for your project. For more information, see [Previewing the default query results](/docs/discovery-data?topic=discovery-data-query-results).

    - There are several example queries in the **Try an example to get started** section. Click the **Run search** button for`IBM`.
    - Query results are displayed.
    - From one of the query results, click **View passages in document**. A preview of the document where the result was found is shown.
    -  On the **Improvement tools** panel, select the dropdowns to learn about the different way you can customize your project. There are five categories of tools: **Customize display**, **Search results**, **Teach domain concepts**, **Define structure**, and **Improve relevance**.
    
That's the tour, stay on the **Improve and Customize** page for the next step.
    
## Step 4: Customize the Sample Project
{: #customize-project-tool}

Now, let's customize a bit. Starting on the **Improve and Customize** page, complete the following steps:

1.  Enter the natural language query `How do I install {{site.data.keyword.icp4dfull_notm}}` in the query field.
1.  Review the query results that are displayed. View the source document for each result by clicking on **View passage in document**.
1.  On the **Improvement tools** panel, choose **Customize display**, and select **Facets**. Select **New facet**, then click the **From existing fields in a collection** button. Choose `enriched_text.entities.type` from the dropdown and click **Apply**. The new facets will display. You can change the name of the facet label, and the filtering behavior.

## Step 5: Keep exploring and experimenting
{: #next-steps-tool}

Continue experimenting with the Sample Project. A few other things you might want to try:

  - Select the **Manage collections** icon on the navigation panel. Click the **New collection** button. Choose **Upload data** and create a new collection with a few of your own documents.
  - Select the **Integrate and Deploy** icon on the navigation panel. On the **Share preview link** tab, copy the link and paste it in your browser to preview your application. On the **Explore UI components** tab, click the **Try it on Storybook** link for any of the components.
  - Select the **Improve and customize** icon on the navigation panel. On the **Improvement tools** panel, select **Customize display**, then choose **Search results**. In the **Select field to display as titles**, choose `document_id` from the dropdown and click **Apply**. The document identifier in each search result will switch from the document name to the document id number.

## Bonus: Get help from anywhere
{: #handy-tools}

To open the product documentation, select the **Help** ![Help icon](images/help_icon.png) icon from the page header. The help content is customized to provide information that is related to what you're doing in the product.