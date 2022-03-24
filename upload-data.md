---

copyright:
  years: 2019, 2022
lastupdated: "2022-03-24"

keywords: upload, one-time upload, field names

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Uploading data
{: #upload-data}

You can perform a one-time document upload from your local file system at any time to add data to a project.
{: shortdesc}

You can upload up to 200 files at a time.

To process document sets that are larger than 200 files, add them to an external data source and use a data source crawler to upload them. For {{site.data.keyword.icp4dfull_notm}} deployments, you can use a *Local File System* data source for this purpose.

For more information about the maximum size allowed for each file, see [Document limits](/docs/discovery-data?topic=discovery-data-collections#collections-doc-limits).

Before you upload a CSV file to a Content Mining project, decide whether you want to apply enrichments to the content. If so, consider adding headers to the source file so that any fields that are generated have meaningful names. Without headers, fields are given generic names, such as `column_0`, `column_1`, and so on.
{: tip}

To upload data, complete the following steps:

1.  Open your project, go to the **Manage collections** page, and then click **New collection**.
1.  Choose **Upload data** as your data source, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents in storage is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: If you want to look for and extract question-and-answer pairs, select **Apply FAQ extraction**.

    For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction).
1.  Optionally, click **More processing settings** to expand the menu, and then click **Apply optical character recognition (OCR)**.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Next**.
1.  Browse for the files you want to crawl.

    ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: You can drag documents that you want to add to your collection.

    For more information about supported file types, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
1.  Click **Finish**.

The file upload is completed quickly. It takes more time for the data to be processed as it is added to the collection. After the files are uploaded and processed, the *Activity* page shows the upload results.

Unlike crawled data sources, you cannot schedule regular updates for uploaded files. If you want to add a later version of a file, you must delete the earlier version and rename the file before you upload it.

## Troubleshooting ingestion issues
{: #upload-data-ts}

Find workarounds and solutions to problems that you might encounter when you upload data.

### Microsoft document troubleshooting tips
{: #upload-data-ts-ms}

Failed to prepare document for SDU processing
:    Some DOC, PPT, and XSL files that use older features which are no longer supported by Microsoft Office can cause ingestion issues. If you encounter this issue, open the file in a more recent version of Microsoft Office and convert the file to the DOCX, PPTX, or XSLX format respectively, and then upload the DOCX, PPTX, or XSLX file.

Line breaks are inserted randomly to some DOCX files
:    When some DOCX files are added to a collection, line breaks are inserted randomly to the text that is stored in the `html` index field. The unexpected line breaks can impact the efficiency of enrichments, such as custom rule recognition. If you encounter this issue, convert the DOCX file to a PDF file, and then import the PDF file.

### PDF file troubleshooting tips
{: #upload-data-ts-pdf}

Failed to parse document due to invalid encoding
:    Enable OCR for the file.

## How file types are handled
{: #file-type-notes}

When you upload a document, data in the file is indexed. Different files types are handled differently by {{site.data.keyword.discoveryshort}}.

-   [CSV files](#file-type-csv)
-   [JSON files](#file-type-json)

### CSV files
{: #file-type-csv}

Ingestion notes:

-   Each line that is defined in the CSV file is added to the index as a separate document.
-   You cannot enable the Optical Character Recognition (OCR) feature for CSV files.
-   If the CSV file has headers, the header names are used to name the fields in which the content from the corresponding column is stored. Avoid using names that have special meaning in {{site.data.keyword.discoveryshort}}. For more information, see [How fields are handled](/docs/discovery-data?topic=discovery-data-upload-data#field-name-limits).

Enrichment notes:

-   You cannot apply prebuilt or user-trained Smart Document Understanding models to CSV files.

### JSON files
{: #file-type-json}

Ingestion notes:

-   Each object that is defined in an array in a JSON file is added to the index as a separate document.
-   You cannot enable the Optical Character Recognition (OCR) feature for JSON files.
-   Object names from the source JSON file are used to name the fields in which the content is stored. Avoid using names that have special meaning in {{site.data.keyword.discoveryshort}}. For more information, see [How fields are handled](/docs/discovery-data?topic=discovery-data-upload-data#field-name-limits).
-   If a root-level field is an array but contains no items, the field is omitted from the index.
-   If a root-level field is an array and contains only one item, the array is indexed as the data type of the one item. For example, a string array with one string is indexed as a string.
-   If a nested field contains an array, even if the array has only one value, it is indexed as an array.
-   If a root-level field is an array and contains more than one item, the data is indexed as an array.
-   If you copy JSON that is generated by {{site.data.keyword.discoveryshort}} and then upload it as a JSON file, remove these system-generated fields from the file first: `document_id`, `parent_document_id`, `filename`, and `title`.

Enrichment notes:

-   You cannot apply prebuilt or user-trained Smart Document Understanding models to JSON files.
-   When you apply an enrichment to a field from the JSON file, the field data type is converted to an array. The field is converted to an array even if it contains a single value. For example, "field1": "Discovery" becomes "field1": ["Discovery"]. 
-   Only the first 50,000 characters of a custom field from a JSON file are enriched.
-   If you want to apply an enrichment to a nested field, you must create a Content Mining project, and then apply the enrichment to the field. If you want to use a different project type, you can reuse the collection that you created with the Content Mining project type elsewhere. For more information, see [Applying enrichments](/docs/discovery-data?topic=discovery-data-connector-database-cp4d#connector-database-cp4d-enrich-db).

## How fields are handled
{: #field-name-limits}

For most unstructured file types, the bulk of the content from the file is added to a field named `text`. For file types that have an inherent data structure, such JSON files, names from the source file are used to name the fields in which the content is stored. When you upload files of this type, be aware of some naming limitations that exist for fields.

The following field names have special meaning. If possible avoid using these names in your structured source files.

- id
- highlight
- html
- metadata
- result_metadata
- score
- spans

If your source document has a field with the name `document_id`, the field is skipped and not added to the index in the collection.

Avoid field names that meet the following conditions. Field names with these restricted characters are not queried.

- Start with the characters `_`, `+`, and `-`. For example, `+extracted-content`.
- Contain the characters `.`, `,`, `#`, `?`, or `:` or spaces. For example, `new:extracted-content`.
- End with numbers. For example, `extracted-content2`.

When you configure a collection to use the CSV header, the document converter automatically changes any field names that contain restricted characters to remove them from the name.
{: note}
