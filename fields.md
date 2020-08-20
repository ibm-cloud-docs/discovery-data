---

copyright:
  years: 2019, 2020
lastupdated: "2020-08-19"

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


# Configuring your collection with Smart Document Understanding
{: #configuring-fields}

You can use Smart Document Understanding (SDU) to quickly train {{site.data.keyword.discoveryfull}} to extract fields in your documents, which will improve the answers that your application returns. The specified fields can also be enriched.

With SDU, you can annotate fields within your documents to train custom conversion models. As you annotate, Watson is learning and will start predicting annotations. After an SDU model is created, it can be [exported](/docs/discovery-data?topic=discovery-data-configuring-fields#import) and used on other collections.

This video provides a quick overview of Smart Document Understanding:

<iframe class="embed-responsive-item" id="youtubeplayer" title="Watson Discovery - Extract Answers From Large Document in 5 Minutes" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/Jpr3wVH3FVA" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

PDF, Microsoft Word, Microsoft PowerPoint, Microsoft Excel, and image files (PNG, TIFF, JPG) can be annotated in the SDU editor. For the complete list of file types that {{site.data.keyword.discoveryshort}} supports, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).

To access the Smart Document Understanding editor:

- Open your project and select the **Improve and customize** icon on the navigation panel. On the **Improvement tools** panel, select **Define structure** and choose **New fields**. If your project contains more than 1 collection, you can then choose the collection.
or
- Select the **Manage collections** icon on the navigation panel and open a collection. For more information on collections, see [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections).

When you build a custom Smart Document Understanding model, the conversion time for your collection may increase due to the resources required to apply the AI model to your documents. The resource requirements will result in a significant decrease in throughput speed.
{: note}

To navigate the Smart Document Understanding editor, view the following information:

1. On the **Manage collection** page, there are three tabs that are needed to use Smart Document Understanding: **Identify fields**, **Manage fields**, and **Enrichments**.

   - **Identify fields** - the SDU editor
   - **Manage fields** - see [Managing fields](/docs/discovery-data?topic=discovery-data-configuring-fields#field-settings)
   - **Enrichments** - see [Managing enrichments](/docs/discovery-data?topic=discovery-data-configuring-fields#enrich-fields).

1. Open the **Identify fields** tab. A subset of documents will be available for annotation purposes. Between 20 - 50 documents will appear in the dropdown list. The number will depend on several factors, including the number of documents in your collection in the supported file formats. 

Use the SDU toolbar to perform the following tasks:
- Choose a document to annotate
- Navigate the document displayed
- Adjust the page view (`single page view`, `zoom in`, `zoom out`), `clear changes`, and `export/import models`. Click on `single page view` to toggle the display. You can view your annotations and document separately or together.

Also see [Getting started with {{site.data.keyword.discoveryshort}}](/docs/discovery-data?topic=discovery-data-getting-started).

## Identifying fields
{: #identify-fields}

<!-- c/s help for the **Identify fields** tab. Do not delete.  -->

See [Best practices for annotating documents](/docs/discovery-data?topic=discovery-data-configuring-fields#bestpractices) before you begin annotating.

1. A default set of fields is displayed next to your document. The available fields are `answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text`, `title`, `table`, and `image`. If you would like to create one or more new custom field labels, click **Create new** and follow the steps. Custom field labels should be lowercase, and contain no spaces.
1. To begin annotating, click on a field label to activate it.
1. Click on the content representing that field in the SDU editor. It will highlight. 
   - Alternately, you can select a field label and drag it to the content in the SDU editor. 
   - To clear a change, click the **Clear changes** button on the toolbar.
1. Click the **Submit page** button.
   
   As you annotate, Watson is learning and will start predicting annotations. Continue annotating until Watson correctly and consistently identifies fields.
   {: note}
   
1. When you have completed annotating, click the **Apply changes and reprocess** button.

Field | Definition  
------ | ------ 
`answer` | In a Q/A pair (often in an FAQ), the answer to the question.
`author` | Name of author (or authors).
`footer` | Use this tag to denote meta-information about the document (such as the page number or references), that appear at the bottom of the page.
`header` | Use this tag to denote meta-information about the document that appears at the top of the page.
`question` | In a Q/A pair (often in an FAQ), the question.
`subtitle` | The secondary title of the document being annotated. 
`table_of_contents` | Use this tag on listings in the document table of contents.
`text` | Use this tag for standard copy text, including paragraphs, definitions, or any set of words that is not a title, answer, author, subtitle, header, or a footer. 
`title` | The main title of the document being annotated.
`table` | Use this tag to annotate tables in your document. 
`image` | Use this tag to annotate images and diagrams in your document.

When you annotate one or more tables using the `table` field, you will automatically enable the **Table Understanding** enrichment for the entire collection. The **Table Understanding** enrichment is applied to the `html` field of your collection. For more information, see [Table Understanding](/docs/discovery-data?topic=discovery-data-understanding_tables).
{: #important}

### Best practices for annotating documents
{: #bestpractices}

If you want to save time reprocessing all the files in a large collection, start with a small collection of documents and build your model, then [export](/docs/discovery-data?topic=discovery-data-configuring-fields#import) it. Create a new collection that contains only 1 document, import the model, then upload the remainder of your documents.
{: tip}

- Follow all guidelines and use consistent labeling on all documents
- Do not label whitespace
- Do not treat **bold**, _italic_, or underlined text differently. Label based on the context, not the style.
- When labeling a document, work from the first page to the last.
- If you incorrectly label an item, choose another label for the item to overwrite the first.
- Pages can be submitted at any time. Ensure that all appropriate labeling is complete before submitting.
- Documents that appear to have text overlaying other text are considered “double overlaid” and cannot be annotated. Report these documents to your administrator.
- Documents that contain multiple columns of text on a single page cannot be annotated. Report these documents to your administrator.
- When annotating a table, make sure to select the entire table before applying the `table` label.

If `Run OCR` is enabled when you create your collection, text is extracted from images using Optical Character Recognition (OCR). If you do not want to apply this option for specific images or diagrams, apply the `image` label to those images.
{: important}

### Importing and exporting SDU models
{: #import}

After you define a model with the SDU editor, you can save it and reuse it on other collections.

You can import or export your completed SDU model using the toolbar at the top of the editor. Click the last icon and choose `Import model` or `Export model`.

Exported models have the file extension of `.sdumodel`.

An imported model is intended to be used without any further annotations. The model will be completely overwritten if you continue annotating after importing it.

If you plan to develop a model and import it into a new collection, it is a sound best practice to create a new collection that contains only 1 document, import the model, then upload the remainder of your documents.
{: tip}

## Managing enrichments
{: #enrich-fields}

<!-- c/s help for the **Managing enrichments** tab. Do not delete. -->

You can enrich fields (including custom fields identified with Smart Document Understanding) in your collection with cognitive metadata.

There are a number of enrichments available in {{site.data.keyword.discoveryshort}}. You must create some of the enrichments before you can apply them. For more information, see [Creating enrichments](/docs/discovery-data?topic=discovery-data-create-enrichments).

To access the **Enrichments** page, select the **Manage collections** icon on the navigation pane and open a collection. Click the **Enrichments** tab. For more information on collections, see [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections).

To apply an enrichment to a field:

1. Open the **Enrichments** page and select the enrichment.
1. Select the field or fields you want to enrich.
1. Click the **Apply** button.
1. Click the **Apply changes and reprocess** button to apply the enrichments to the collection.

## Managing fields
{: #field-settings}

<!-- c/s help for **Manage fields** page. Do not delete. -->

The **Manage fields** tab contains several options:
-  **Identify fields to index**
-  **Improve query results by splitting your documents**
-  **Date format settings**

To access the **Manage fields** page, click the **Manage collections** icon on the navigation pane and open a collection. Click the **Manage fields** tab. For more information on collections, see [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections).

**Identify fields to index** - Use this option to choose which fields should be included in the index for this collection. You can switch off any fields that you do not want to index. For example, your PDFs may contain a running header or footer that does not contain useful information, so you can exclude those fields from the index.

**Improve query results by splitting your documents**. Use this option to split your documents into segments based on a field name. After your documents are split, each segment is a separate document that will be enriched, indexed, and returned as a separate query result. Documents are split based on a single field name, for example `title`, `author`, `question`. 
  - The number of segments per document is limited to `1,000`. Any document content remaining after `999` segments are stored within segment `1,000`.
  - PDF and Word metadata, as well as any custom metadata, is extracted and included in the index with each segment. Every segment of a document includes identical metadata.
  - If a split document is updated and needs to be re-uploaded, you should replace the document using the **Update document** method in the [API reference](https://{DomainName}/apidocs/discovery-data#update-a-document){: external}. Upload the document, using the POST method of the `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}` API, specifying the contents of the `parent_id` field of one of the current segments as the {document_id} path variable. All segments will be overwritten, unless the updated version of the document has fewer total sections than the original. Those older segments remain in the index and can be individually deleted using the API. For more information, see the [API Reference](https://{DomainName}/apidocs/discovery-data#delete-a-document){: external}.

**Date format settings** - The following options are useful if you want to use time series visualization in the **Content Mining** project type or if you want to correctly parse dates from text in different languages. Use this option to add or delete date formats that are used to convert date strings to date-type data set fields. Only strings that are compatible with the Java `SimpleDateFormat` class are supported. You cannot add any documents that include alternative date formats to the index.
  - **Date formats** - Use this option to parse a string representation into the `Date` data type. For example, `Sun, 06 Nov 1994 08:49:37 GMT`, or `1994-11-06`, is parsed as the same date. This field supports the Java `SimpleDateFormat` class, so the date formats string can be in any format that the `SimpleDateFormat` class supports. If you know that your data does not match any of the predefined date formats, you can add a format that the Java `SimpleDateFormat` class supports, or you can delete any of the predefined formats. {{site.data.keyword.discoveryshort}} checks the date formats in order for each date-type data set field and uses the first format that successfully parses the field. Therefore, be sure to place the date format that you want to use at the top of the list. You must run a full crawl or a full import to apply any changes to documents that are currently in the data set.
  - **Select a time zone** - You can use this option to designate a time zone for a document that has a generated time but no time-zone information. You can use this option to store a document creation time into a date-type data set field. For example, if a document is generated on `1 January 2020 1:00 AM Eastern Standard Time (EST)`, the document metadata only stores `2020-01-01 01:00 a.m.`. In this case, {{site.data.keyword.discoveryshort}} cannot parse `2020-01-01 01:00 a.m.` because, without time-zone information that is associated with the document, `2020-01-01 01:00 a.m.` is not specific. Because `1 January 2020 1:00 AM Eastern Standard Time (EST)` and `1 January 2020 1:00 AM Pacific Standard Time (PST)` are different times, you must select **(GMT-05:00) Eastern Standard Time** as the time zone ID so that {{site.data.keyword.discoveryshort}} parses `1 January 2020 1:00 AM` with the EST time zone, as intended.
  - **Select a language** - Use this option to choose a language to parse a string value that represents the date for the date-type data set fields. You can also use this option to manage any cultural- or language-specific patterns of the dates in your documents. For example, using the `EEE, MM dd, yyyy` format, the **English (United States)** locale can parse the string value of `"Wednesday, 07 01, 2020"`, and the **Japanese (Japan)** locale can parse the same string value of `"水曜日, 07 01, 2020"`.
