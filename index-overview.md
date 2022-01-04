---

copyright:
  years: 2020, 2022
lastupdated: "2021-06-21"

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

The purpose of the fields is self-explanatory given their field names.

What is not obvious is the importance of the `text` field. The `text` field typically contains the main body of text from the original document. Most of the content that is returned in search results originates from this one field. How to parse and return only relevant chunks of information from this field is determined by the query result configuration that is used by the project. For more information, see [Previewing the default query results](/docs/discovery-data?topic=discovery-data-query-results).

More processing adds more fields. And more processing is applied automatically depending on the project type and on the document type. When processes run on documents in a collection, extra fields are added to store information that is associated with the process. For example, when the Entities enrichment is applied to a collection, it starts a process that adds fields with names that begin with `enriched_{field_name}.entities` to the documents in the collection.

- For more information about fields that are added to your collection, see [Interpreting the results](/docs/discovery-data?topic=discovery-data-test#test-json).
- For more information about the enrichments that are applied by default, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults).
