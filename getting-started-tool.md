---

copyright:
  years: 2019
lastupdated: "2019-08-30"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Getting started with Watson Discovery for IBM Cloud Pak for Data
{: #getting-started}

In this short tutorial, we introduce {{site.data.keyword.discovery-data_short}} and go through the process of creating a data collection and searching it.
{: shortdesc}

## Before you begin
{: #before-you-begin-tool}
{: hide-dashboard}

Install {{site.data.keyword.discovery-data_short}}. See [Installing Discovery for Cloud Pak for Data](/docs/services/discovery-data?topic=discovery-data-install#install).

## Step 1: Create a collection
{: #create-a-collection-tool}

Your first step with {{site.data.keyword.discovery-data_short}} is to create a data collection.

A collection is a set of your documents. *Why would I want more than one collection?* There are a few reasons:

-  You might want multiple collections in order to separate results for different audiences.
-  You have a number of different data sources.
-  The data might be so different that it doesn't make sense for it all to be queried at the same time.

To create a collection:

1.  From the instance details page in {{site.data.keyword.icp4dfull}}, click **Launch Tool**.
1.  Click **Create new collection**.
1.  Click **Upload data**. In this tutorial, we are manually uploading files from a local machine, the other options on this page allow you to configure the automatic collection of data from supported applications.
1.  Enter `example collection` into the **Collection name** field and leave the **Collection language** as `English`. By selecting a language at this point you define which built-in processors will be used when ingesting your documents. If the documents you upload are written in more than one language, select the language of the majority of documents.
1.  Click **Create collection**. Once the collection has been initialized, the **Upload data to get started** page is displayed.

## Step 2: Download the sample document and upload to your collection
{: create-custom-configuration}

1.  Download this sample PDF document: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/watsonexplorerinstall.pdf" download>Watson Explorer Installation Guide <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. See [Configuring collection types](/docs/services/discovery-data?topic=discovery-data-collections#collection-types) for the full list of document types that are supported in {{site.data.keyword.discovery-data_short}}.

    In some browsers, the link opens in a new window instead of saving locally. If this occurs, select **Save As** in your browser's **File** menu to save a copy of the file.
    {: tip}

1.  Upload the document to your collection. To upload documents, either drag and drop it into your collection, or click **Select documents**. After the upload is complete and the document has been processed, the following information displays:
    -  The number of documents (1).
    -  The fields identified from your document. You should see one field identified, `text`. We will identify additional fields in a bit.
1.  Let's try a quick natural language query to level set. Click **Build your own query** on the lower right.
1.  On the **Query** page, enter `What are the minimum hardware requirements` in the **Use natural language** field, and click **Run query**. The result is not as precise as it could be, so let's improve it with Smart Document Understanding.
1.  Click the **Data settings** link on the upper right. The **Data settings** page opens.

## Step 3: Annotate your document
{: #upload-your-documents}

For more information about annotating documents, see [Configuring your collection with Smart Document Understanding](/docs/services/discovery-data?topic=discovery-data-configuring-fields).
{: tip}

1.  On the **Data settings** page, there are three tabs: **Identify fields**, **Manage fields**, and **Enrich fields**.
1.  The `Watson Explorer Installation Guide` is displayed and ready for annotation on the **Identify fields** tab. All available fields (`answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text`, and `title`) are displayed in the **Field labels** list on the right.

    Since the entire document is currently identified as `text`, the markers on the right side of the PDF are indicated as the `text` field label, which is yellow in color. As you annotate (and the system starts predicting), the colors update.
    {: tip}

1.  Click the **Single page view** icon so that the highlighting overlays the page text.
1.  Click the **title** field label, select the `Installation and Integration Guide` text, and then click the **Submit page** button.
1.  In the page preview on the left, click page 3. Note that the `title` has already been predicted for this page and click the **Submit page** button.
1.  On page 4, select the **footer** field label, select the footer text, and then click the **Submit page** button.
1.  On pages 5 and 6, annotate the footer text with the **footer** field label. Submit each page. Click through a few more pages and note that the footer was predicted properly by {{site.data.keyword.discovery-data_short}}.
1. On pages 7, 9, and 10, annotate the `title`s (flush left) and `subtitle`s (indented). Submit each page individually.
1.  Click through a few more pages and check the predicted titles and subtitles. If any text needs to be changed, annotate those pages and click the **Submit page** button.
1.  Now, click the **Manage fields** tab.
1.  In the **Improve query results by splitting your documents** section, click **Split document** and select `subtitle`.
1.  Click **Apply changes**.
1.  Click on the name of your collection to return to the **Overview** page.
1.  Click **Reprocess collection**. This action takes the documents that are in the collection and applies all the changes that you made to the configuration.

After {{site.data.keyword.discovery-data_short}} finishes processing and indexing, the **Overview** page is refreshed. You should now see 30+ documents, and 4 fields identified from your data: `footer`, `subtitle`, `text`, and `title`. If the changes don't display within a few minutes, refresh the browser window.

  You can exclude fields such as `footer` from being indexed by selecting **Data settings** > **Manage fields** and toggling the field name to `off`.
  {: tip}

## Step 4: Let's query
{: #build-a-query}

1.  Click **Build your own query** on the bottom right.
1.  On the **Query** page, enter `What are the minimum hardware requirements` in the **Use natural language** field and click **Run query**.
1.  In the output, look at the `text` field under the `results` section. The answers that are returned from the query are much more precise.

Additional resources:
-  To learn more about the data schema of your documents, see the [Discovery data schema](/docs/services/discovery-data?topic=discovery-data-query-concepts#discovery-data-schema) for details.

## Next steps
{: #next-steps-tool}

Now you have a functioning and populated {{site.data.keyword.discovery-data_short}} instance. You can customize your collection by adding more documents and enrichments, and by labeling fields. For more information, see [Configuring your collection with Smart Document Understanding](/docs/services/discovery-data?topic=discovery-data-configuring-fields).
