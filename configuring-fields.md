---

copyright:
  years: 2019, 2025
lastupdated: "2025-01-20"

keywords: smart document understanding,sdu

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Define a user-trained SDU model
{: #configuring-fields}

Create a Smart Document Understanding (SDU) model that learns about the content of a document based on the document's structure.
{: shortdesc}

Use the Smart Document Understanding tool to add custom fields to a collection so you can do the following things:

-   Target prebuilt or custom enrichments at specific sections of a document.
-   Break large documents into smaller documents.

For help with deciding whether SDU can help your use case, read [When to use Smart Document Understanding](#sdu-when).

If capturing information from tables is critical to your use case, consider using a pretrained model. For more information about creating a pretrained SDU model, see [Apply a pretrained SDU model](/docs/discovery-data?topic=discovery-data-sdu-pretrained).

## When to use Smart Document Understanding
{: #sdu-when}

The Smart Document Understanding (SDU) tool works better with some project types.

-   The tool is most beneficial when used with *Document Retrieval* projects. Use the tool to break your documents into smaller, more consumable chunks of information. When you help {{site.data.keyword.discoveryshort}} index the correct set of information in your documents, you improve the answers that your application can find and return.

    For example, your documents might contain tips that are shown in sections with an H4 heading. If you want to extract the information from these tips separately, you can add a field that is named `tips`, and teach the model to recognize it. After you apply the model to your collection, you can apply an enrichment to the `tips` field only. Later, you can limit the search to return content from only the `tips` field.
  
    Or maybe you have extra large documents that contain subsections. You can teach the SDU model to recognize these subsections, and then split the large document into multiple, smaller, and easier-to-manage documents that begin with one of these subsections.

-   The best way to prepare a collection for use in *Conversational Search* projects is to identify discrete question-and-answer pairs. You can use the SDU tool to find and annotate them. If you configure the project to contain answers in an answer field, you must update the search configuration in {{site.data.keyword.conversationshort}} to get the body of the response from the custom answer field.

-   A pretrained SDU model is applied to *Document Retrieval for Contracts* projects automatically. The pretrained SDU model knows how to recognize terms and concepts that are significant to contracts. As a result, you cannot apply a user-trained SDU model to this project type, but you also don't need to.
-   The SDU tool is rarely used with *Content Mining* projects.

You can use the SDU tool to annotate the following file types only:

-   Image files (PNG, TIFF, JPG)
-   Microsoft PowerPoint
-   Microsoft Word
-   PDF

For a complete list of file types that {{site.data.keyword.discoveryshort}} supports, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).

The Smart Document Understanding tool uses optical character recognition (OCR) to extract text from images in the files that it analyzes. Images must meet the minimum quality requirements that are supported by OCR. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).

The tool cannot read documents with the following characteristics; remove them from your collection before you begin:

-   Documents that appear to have text that overlays other text are considered *double overlaid* and cannot be annotated.
-   Documents that contain multiple columns of text on a single page cannot be annotated.

When you build a custom Smart Document Understanding model, the conversion time for your collection can increase due to the resources that are required to apply the AI model to your documents.
{: note}

### Start with representative documents
{: #sdu-prereq}

Documents come in all shapes and sizes. Your collection might have a mix of different document structures. Smart Document Understanding works best when the documents in a single collection have similar style characteristics. For example, the documents use consistent font sizes and colors for titles and headers, and tables in the document have similar layouts. To create the best model for your collection, take this prerequisite step:

1.  Review your documents to look for style and layout patterns, and then separate the documents into groups based on their style.

    For example, if your data contains documents that follow four different formatting styles, break the documents into four separate collections, one for each style. Add documents with a uniform layout and style to each collection. A good target size per collection is 40 documents.
1.  Use the SDU tool to annotate this representative set of documents and train Watson to recognize custom content in your data.
1.  Apply the custom SDU model to the full collection. For more information, see [Reusing SDU models](#import).

## Creating the model
{: #sdu-task}

To apply a user-trained Smart Document Understanding model to your collection, complete the following steps:

1.  Open the **Manage collections** page from the navigation panel.
1.  If your project has more than one collection, select the collection with documents that you want to annotate.
1.  Open the *Identify fields* page.
1.  Choose **User-trained models**.

    The **Text extraction only** option is used by default. With this model, any text that is recognized in the source documents is indexed in the `text` field.
1.  Click **Submit**, and then click **Apply changes and reprocess**.

A subset of documents is available for you to annotate. A set of 20 - 50 documents is displayed in a list. The number of documents that are available differs based on several factors, including the overall number of documents in your collection and how many of them are supported file types.

If any training documents, which are used to train an SDU model, undergoes layout or structure changes in {{site.data.keyword.discoveryshort}}, the previous annotations are no longer valid. To update the SDU model, you must annotate the updated documents again after ingesting them. Otherwise, the previous annotations are incorrectly mapped with the text content, and the corresponding annotation pages in the UI become confusing.


## Labeling video
{: #sdu-label}

The following video shows you how to select a label, and then apply it to a representation of the text in your document. 

In the video, the user clicks the `title` field label, and then clicks the text block that represents the *Table of Contents* page title to label the text as a title. Next, the user clicks the `table_of_contents` field label and selects the table of contents text block to label it. Then, the user clicks the `footer` field label and clicks the text block that represents the page footer. After the text is labeled, the user clicks the *Submit page* button.

![Labeling a title, table of contents, and footer with SDU](images/sdu-snip.mp4){: video controls loop height="500"}

## Labeling the documents
{: #sdu-label-task}

Before you begin, get a feel for the structure of the document you plan to annotate. Are there subtitled sections that you want Discovery to return per answer? If so, identify all subtitles. Later you can split the document into discrete subdocuments, each starting with a subtitle. For more information, see [When to use Smart Document Understanding](#sdu-when).

To label documents, complete the following steps:

1.  Review the document preview.

    A view of the original document is displayed along with a representation of the document, where the text is replaced by blocks.

    The blocks are all the color of the `text` field label because all of the current text is considered to be standard text and will be indexed in the `text` field.

    Label blocks that represent specific types of information, such as titles or page footers, with other field labels. For example, when you apply the title field label to a document title that would otherwise be indexed as text, you are defining a more precise representation of the document content.
    
    The process of using labels to identify different parts of the document's structure is called *annotating* the document.

1.  Review the field labels that you can use to annotate the document. They are displayed in the *Field labels* panel.

    See the [Default field labels](#sdu-default-fields) table for a list of the fields and their descriptions.
1.  To create a custom field label, click **Create new**.

    -   Specify a field label with no spaces. For example, `complex_task` is a valid field label.

        Avoid using a field label name or including characters, such as a number sign (#) or period (.), in the name that have special meaning for {{site.data.keyword.discoveryshort}}. For more information, see [How fields are handled](/docs/discovery-data?topic=discovery-data-index-overview#field-name-limits).
        {: note}

    -   If you want to change the color that is used to represent the field, repeatedly click the color block ![Square block of color with two arrows that point in a circle](images/sdu-label-color.png) until it is displayed in the color that you want to use.

        You cannot change the field label color later.
        {: important}

    -   Click **Create**.
1.  First, click a field label to activate it.
1.  Next, click the block that represents the content that you want to label as the field type.

    The block changes to the color of the field label. You successfully labeled the field!
1.  Repeat this process to annotate more fields in the document.

    Don't worry. You don't need to label every page. As you apply labels and submit pages, Watson learns from what you annotate and starts to predict annotations.

    Follow these guidelines:

    -   If there's nothing special about a section, leave it labeled as `text`, which is applied by default.
    -   A label cannot span multiple pages.
    -   Do not treat **bold**, *italic*, or underlined text differently. Label based on the context, not the style.
    -   Use consistent labeling on all documents.
    -   Work from the first page of a multipage document to the last.
    -   To remove a single annotation, choose another label (such as `text`) and apply it to the item to overwrite the previous annotation.
    -   To remove annotations that you added to an entire page, click the **Clear changes** icon in the toolbar.
    -   To annotate a table, click the text at the start of the table and then drag to select the text in the entire table.
    -   When you label one or more tables, the *Table Understanding* enrichment is enabled for the entire collection automatically. For more information, see [Understanding tables](/docs/discovery-data?topic=discovery-data-understanding_tables).
    -   Images from the source documents are not rendered in the preview. If Optical Character Recognition (OCR) is enabled, any text from the image or diagram is extracted and rendered in the preview.
    -   Do not label white space.

1.  When everything that you want to label is labeled, submit the page. Click **Submit page**.

    Continue annotating documents until Watson can correctly and consistently map different types of content to the appropriate fields for you.
    {: note}

1.  After you teach Watson to identify fields, click **Apply changes and reprocess**.

Custom fields that you define by using the SDU tool are indexed as root-level fields.

### What to do next
{: #sdu-postreq}

When you build a user-trained model, you change where information is stored in your documents. Next, change how the search results are configured. By default, search results are retrieved from passages or the text field. You might have a better field to use as the source of the result body. For more information, see [Changing the result content](/docs/discovery-data?topic=discovery-data-query-results#query-results-content).

If your project is being used by a virtual assistant, update the search skill configuration to pull the answer body from a different field. For more information, see [Configure the search](/docs/assistant?topic=assistant-skill-search-add#skill-search-add-configure){: external}.

You can apply enrichments, either custom or prebuilt enrichments, to the new root fields that are generated by the SDU model.

If you want to return shorter text snippet with a search result, you can split your documents based on one of the new fields that you defined, such as chapter or section.

### Available fields
{: #sdu-default-fields}

The following fields are available for you to apply to documents by using the Smart Document Understanding tool.

The fields are arbitrary. You can apply the `image` field to every title in the document if you want. Although, it might be difficult to know which field to search later for information that you need if the field names don't match the content. The default set are representative field types that are meant to help you get started. Only the `text` and `table` fields have special significance. Do not use them to identify anything other than text and tables.

| Field      | Definition |
|------------|------------|
| `answer`   | In a question-and-answer pair (often in an FAQ), the answer to the question. |
| `author`   | Name of author or authors. |
| `footer`   | Use this tag to denote meta-information about the document (such as the page number or references), that appear at the end of the page. |
| `header`   | Use this tag to denote meta-information about the document that appears at the start of the page. |
| `question` | In a question-and-answer pair (often in an FAQ), the question. |
| `subtitle` | The secondary title of the document. |
| `table_of_contents` | Use this tag on lists in the document table of contents. |
| `text`     | By default, every block of text in the document is labeled as text. Apply different labels only to blocks of text with special meaning. |
| `title`    | The main title of the document. |
| `table`    | Use this tag to annotate tables in your document. |
| `image`    | Images are not shown in the document preview. If you enable OCR, text from an image or diagram is displayed in the preview instead. If you want to prevent text from some images from being included in search results, tag the image text as an image. You can exclude the image field from the index later. |
{: caption="Default field labels" caption-side="top"}

### Reusing SDU models
{: #import}

After you define a model with the SDU tool, you can save it and reuse it in other collections by exporting it from one collection and importing it to another.

Importing a new model overwrites the existing model in a collection. If the existing model is already trained such as through custom field labels and annotations, then importing a new model affects the collection and can result in data loss.
{: note}

To reuse a model, complete the following steps:

1.  Export the model that you want to reuse. From the SDU toolbar menu, select **Export model**.

    ![Import and export menu](images/sdu-import-export.png){: caption="Import and export menu" caption-side="bottom"}

1.  Create the collection where you want to reuse the model. Add only one document to the collection at first.
1.  Import the model from the SDU toolbar. The exported model has a file extension of `.sdumodel`.
1.  Add the rest of the documents to the collection. Open the **Activity** tab of the *Manage collections* page, and then click **Upload data** to add more files to the collection.

Use the imported model as-is. Do not make any more annotations. If you make annotations after you import the `.sdumodel` file, the imported model will be overwritten.

## Smart Document Understanding limits
{: #sdu-limits}

The number of custom fields that you can create per Smart Document Understanding model depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Custom fields per SDU model |
|--------------|---------------------|
| Cloud Pak for Data |                 Unlimited |
| Premium      |                             100 |
| Enterprise |                               100 |
| Plus (includes Trial)  |                    40 |
{: caption="Custom field limits" caption-side="top"}

The maximum number of documents that you can annotate to train an SDU model per collection depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Documents per collection |
|--------------|------------------|
| Cloud Pak for Data |                        40 |
| Premium      |                              40 |
| Enterprise |                                40 |
| Plus (includes Trial)  |                    40 |
{: caption="Training set limits" caption-side="top"}

## Managing fields
{: #field-settings}



The **Manage fields** tab contains several options:

Identify fields to index
:   For more information, see [Excluding content from query results](/docs/discovery-data?topic=discovery-data-hide-data).

Improve query results by splitting your documents
:   For more information, see [Split documents to make query results more succinct](/docs/discovery-data?topic=discovery-data-split-documents).

Date format settings
:   For more information, see [Date format settings](/docs/discovery-data?topic=discovery-data-index-overview#field-date-settings).

To access the **Manage fields** page, click the **Manage collections** icon on the navigation panel and open a collection. Click the **Manage fields** tab. For more information about collections, see [Creating collections](/docs/discovery-data?topic=discovery-data-collections).
