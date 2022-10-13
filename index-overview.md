---

copyright:
  years: 2020, 2022
lastupdated: "2022-10-12"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# How your data source is processed
{: #index-overview}

When you connect to a data source, {{site.data.keyword.discoveryshort}} *processes* the information from the data source to create a *collection*.
{: shortdesc}

The goal of processing a data source is to identify meaningful information and tag it as it is added to the collection so it is easier to find and retrieve the information later.

The processing that is applied to all data sources includes the following steps:

- Identify individual documents in the data source
- Find fields in the documents
- Index the fields

You can see a list of the fields that were indexed from the *Manage fields* page.

1.  Go to the *Manage collections* page, and then choose the collection.

    Make sure that the processing of the collection is finished first. The Activity page shows the processing status.
1.  Click the *Manage fields* tab.

The fields that are shown can differ based on your data. However, one subset of fields is always listed. These fields, with names such as `footer` and `header`, are derived from the Smart Document Understanding (SDU) tool, and are listed even when you don't explicitly apply an SDU model to the collection. (For the full list of SDU-generated fields, see [Available fields](/docs/discovery-data?topic=discovery-data-configuring-fields#sdu-default-fields).) Only the fields with a data type specified are stored in the collection's index.

One of the SDU-generated fields that is stored in the index is the `text` field. The `text` field typically contains the main body of text from the original document. Most of the content that is returned in search results originates from this one field. How to parse and return only relevant chunks of information from this field is determined by the query result configuration that is used by the project. For more information, see [Previewing the default query results](/docs/discovery-data?topic=discovery-data-query-results).

More processing adds more fields. And more processing is applied automatically depending on the project type. When processes run on documents in a collection, extra fields are added to store information that is associated with the process. For example, when the built-in Entities enrichment is applied to a collection, it starts a process that adds fields with names that begin with `enriched_{field_name}.entities` to the documents in the collection.

- For more information about fields that are added to your collection, see [Interpreting the results](/docs/discovery-data?topic=discovery-data-test#test-json).
- For more information about the enrichments that are applied by default, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults).

## How fields are handled
{: #field-name-limits}

For most unstructured file types, the bulk of the content from the file is added to a field named `text`. For file types that have an inherent data structure, such JSON files, names from the source file are used to name the fields in which the content is stored. When you upload files of this type, be aware of some naming limitations that exist for fields.

The following field names have special meaning. If possible do not use these names in your structured source files.

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
- Contain the characters `.`, `,`, `#`, `?`, or `:` or spaces. For example, `extracted content` or `new:extracted-content`.
- End with numbers. For example, `extracted-content2`.

## How dates are handled
{: #field-dates}

Dates are captured in different ways depending on the file type.

Unstructured files
:    The best way to capture date information from the body of a document with unstructured data is to use a natural language processing model enrichment. For example, the prebuilt Entities enrichment recognizes dates and annotates them in the `text` field (or other body fields with the `String` data type). In a document where the enrichment is applied, you can find dates by looking for fields that are labeled as `enriched_{fieldname}.entities.type`=`Date`.

    Dates from metadata date fields, such as `extracted_metadata.publicationdate`, are stored in the index as dates as long as the date format matches one of the supported date data type formats. You can't see nested fields from the *Manage fields* page. And when you view a search result as JSON, date field values are displayed as string values because the JSON editor shows the date as a string. However, values from date fields behave like dates. You can use greater than (`>`) or less than (`<`) operators with such fields in Discovery Query Language queries, for example.

Structured files
:    Structure files that you import, such as CSV or JSON files, might contain date fields that you want to store as date data types. {{site.data.keyword.discoveryshort}} can recognize many date formats. However, you might need to add a format to the list. For more information, see *Date format settings*.

### Date format settings
{: #field-date-settings}

If your documents have a root-level field with date information in it, you can set the field to be a `Date` data type field in the index.

{{site.data.keyword.discoveryshort}} recognizes the following date formats automatically:

```text
yyyy-MM-dd'T'HH:mm:ssZ
yyyy-MM-dd'T'HH:mm:ssXXX
yyyy-MM-dd'T'HH:mm:ss.SSSZ
yyyy-MM-dd'T'HH:mm:ss.SSSX
yyyy-MM-dd
M/d/yy
yyyyMMdd
yyyy/MM/dd
```
{: screen}

If you store dates in other formats, you can add the format to the list of supported formats. 

To add more date formats, complete the following steps:

1.  From the *Manage fields* page for the collection, add a format as a new line in the **Date formats** field. 

    Specify a date format that is supported by the Java [SimpleDateFormat](https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html){: external} class.
    
    For example, if your records store only year values for dates, add `yyyy` to the supported date formats list. You can then set the data type for the field that contains a year value to *Date*, and reprocess your collection. As a result, an occurrence of `2019` in the date field is stored as `2019-01-01T05:00:00Z` in the index.

    When you add a new date format, you must specify an associated time zone for the date.

1.  Specify a time zone.

1.  Optionally, select a date locale. 

    The locale you choose is used to parse a string value that represents the date for the date-type data set fields. For example, by using the `EEE, MM dd, yyyy` format, the **English (United States)** locale can parse the string value of `"Wednesday, 07 01, 2020"`, and the **Japanese (Japan)** locale can parse the same string value of `"水曜日, 07 01, 2020"`.

1.  If you already imported documents with dates in formats that were not recognized, reprocess the documents.

{{site.data.keyword.discoveryshort}} cannot store a date that is mentioned within a text field as a *Date* field in the index. You can, however, use an enrichment such as the *Entities* enrichment to identify dates that are mentioned in text.

## How file types are handled
{: #file-type-notes}

When you upload a document, data in the file is indexed. Different files types are handled differently by {{site.data.keyword.discoveryshort}}.

-   [CSV files](#file-type-csv)
-   [JSON files](#file-type-json)

### CSV files
{: #file-type-csv}

Notes about adding data:

-   Each line that is defined in the CSV file is added to the index as a separate document, each with the same `parent_document_id`.
-   You cannot enable the Optical Character Recognition (OCR) feature for CSV files.
-   If the CSV file has headers, the header names are used to name the fields in which the content from the corresponding column is stored. Do not use names that have special meaning in {{site.data.keyword.discoveryshort}}. Be sure that the field names conform to the naming rules, such as having no spaces and no appended numbers. For example, you can rename the `start date` header to `start_date` and `label1` to `label-one` before you add the file. For more information, see [How fields are handled](#field-name-limits).
-   When a CSV file header name contains restricted characters, the document converter automatically removes the restricted characters from the field name when it adds the resulting field to the index. 

Note about enhancing data:

-   You cannot apply prebuilt or user-trained Smart Document Understanding models to CSV files.

### JSON files
{: #file-type-json}

Notes about adding data:

-   Each object that is defined in an array in a JSON file is added to the index as a separate document, each with the same `parent_document_id`.
-   Object names from the source JSON file are used to name the fields in which the content is stored. Do not use names that have special meaning in {{site.data.keyword.discoveryshort}}. Be sure that the names conform to the naming rules, such as having no spaces and no appended numbers. For example, you can rename the `updated on` object to `updated_on` and `answer2` to `answer-two` before you add the file. For more information, see [How fields are handled](#field-name-limits).
-   If a root-level field is an array but contains no items, the field is omitted from the index.
-   If a root-level field is an array and contains only one item, the array is indexed as the data type of the one item. For example, a string array with one string is indexed as a string.
-   If a nested field contains an array, even if the array has only one value, it is indexed as an array.
-   If a root-level field is an array and contains more than one item, the data is indexed as an array.
-   If you copy JSON that is generated by {{site.data.keyword.discoveryshort}} and then upload it as a JSON file, remove these system-generated fields from the file first: `document_id`, `parent_document_id`, `filename`, and `title`.
-   You cannot enable the Optical Character Recognition (OCR) feature for JSON files.

Notes about enhancing data:

-   You cannot apply prebuilt or user-trained Smart Document Understanding models to JSON files.
-   When you apply an enrichment to a field from the JSON file, the field data type is converted to an array. The field is converted to an array even if it contains a single value. For example, "field1": "Discovery" becomes "field1": ["Discovery"]. 
-   Only the first 50,000 characters of a custom field from a JSON file are enriched.
-   In project types where the *Part of Speech* (POS) enrichment is applied automatically, the enrichment is applied to the field that contains the bulk of the file content. In JSON files, this field is determined by the following rules:

    -   If a field is named `text`, the POS enrichment is applied to it.
    -   The field with the longest string value and highest number of distinct values is chosen.
    -   If more than one field meets the previous condition, one of the fields is chosen at random.

-   If you want to apply an enrichment to a nested field, you must create a Content Mining project, and then apply the enrichment to the field. If you want to use a different project type, you can reuse the collection that you created with the Content Mining project type elsewhere. For more information, see [Applying enrichments](/docs/discovery-data?topic=discovery-data-connector-database-cp4d#connector-database-cp4d-enrich-db).

## How passages are derived
{: #query-results-passages}

{{site.data.keyword.discoveryshort}} uses sophisticated algorithms to determine the best passages of text from all of the documents that are returned by a query. Passages are returned per document by default. They are displayed as a section within each document query result and are ordered by passage relevance.

{{site.data.keyword.discoveryshort}} uses sentence boundary detection to pick a passage that includes a full sentence. It searches for passages that have an approximate length of 200 characters, then looks at chunks of content that are twice that length to find passages that contain full sentences. Sentence boundary detection works for all supported languages and uses language-specific logic.

For all project types except *Conversational Search*, you can change how the passages are displayed in the search results from the **Customize display > Search results** page. For example, you can configure the number of passages that are shown per document and the maximum character size per passage.
