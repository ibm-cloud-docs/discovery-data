---

copyright:
  years: 2020, 2022
lastupdated: "2022-05-13"

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

The fields that are shown can differ based on your data. However, one subset of fields are always listed. These fields, with names such as `footer` and `header`, are derived from the Smart Document Understanding (SDU) tool, and are listed even when you don't explicitly apply an SDU model to the collection. (For the full list of SDU-generated fields, see [Available fields](/docs/discovery-data?topic=discovery-data-configuring-fields#sdu-default-fields).) Only the fields with a data type specified are stored in the collection's index.

One of the SDU-generated fields that is stored in the index is the `text` field. The `text` field typically contains the main body of text from the original document. Most of the content that is returned in search results originates from this one field. How to parse and return only relevant chunks of information from this field is determined by the query result configuration that is used by the project. For more information, see [Previewing the default query results](/docs/discovery-data?topic=discovery-data-query-results).

More processing adds more fields. And more processing is applied automatically depending on the project type. When processes run on documents in a collection, extra fields are added to store information that is associated with the process. For example, when the built-in Entities enrichment is applied to a collection, it starts a process that adds fields with names that begin with `enriched_{field_name}.entities` to the documents in the collection.

- For more information about fields that are added to your collection, see [Interpreting the results](/docs/discovery-data?topic=discovery-data-test#test-json).
- For more information about the enrichments that are applied by default, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults).

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
-   If the CSV file has headers, the header names are used to name the fields in which the content from the corresponding column is stored. Avoid using names that have special meaning in {{site.data.keyword.discoveryshort}}. For more information, see [How fields are handled](#field-name-limits). For example, rename `start date` to `start_date` and `label1` to `label-one`.
-   When a CSV file header name contains restricted characters, the document converter automatically removes the restricted characters from the field name when it adds the resulting field to the index. 

Enrichment notes:

-   You cannot apply prebuilt or user-trained Smart Document Understanding models to CSV files.

### JSON files
{: #file-type-json}

Ingestion notes:

-   Each object that is defined in an array in a JSON file is added to the index as a separate document.
-   Object names from the source JSON file are used to name the fields in which the content is stored. Avoid using names that have special meaning in {{site.data.keyword.discoveryshort}}. For more information, see [How fields are handled](#field-name-limits). For example, rename `updated on` to `updated_on` and `answer2` to `answer-two`.
-   If a root-level field is an array but contains no items, the field is omitted from the index.
-   If a root-level field is an array and contains only one item, the array is indexed as the data type of the one item. For example, a string array with one string is indexed as a string.
-   If a nested field contains an array, even if the array has only one value, it is indexed as an array.
-   If a root-level field is an array and contains more than one item, the data is indexed as an array.
-   If you copy JSON that is generated by {{site.data.keyword.discoveryshort}} and then upload it as a JSON file, remove these system-generated fields from the file first: `document_id`, `parent_document_id`, `filename`, and `title`.
-   You cannot enable the Optical Character Recognition (OCR) feature for JSON files.

Enrichment notes:

-   You cannot apply prebuilt or user-trained Smart Document Understanding models to JSON files.
-   When you apply an enrichment to a field from the JSON file, the field data type is converted to an array. The field is converted to an array even if it contains a single value. For example, "field1": "Discovery" becomes "field1": ["Discovery"]. 
-   Only the first 50,000 characters of a custom field from a JSON file are enriched.
-   If you want to apply an enrichment to a nested field, you must create a Content Mining project, and then apply the enrichment to the field. If you want to use a different project type, you can reuse the collection that you created with the Content Mining project type elsewhere. For more information, see [Applying enrichments](/docs/discovery-data?topic=discovery-data-connector-database-cp4d#connector-database-cp4d-enrich-db).
