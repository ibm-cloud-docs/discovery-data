---

copyright:
  years: 2019, 2021
lastupdated: "2021-12-21"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Split documents to make query results more succinct
{: #split-documents}

Split your documents so that the search function can find more concise information to return in query results.

For more information about the benefits of splitting documents, read the [Using IBM Watson Discovery’s New Document Segmentation Feature](https://medium.com/ibm-watson/using-ibm-watson-discoverys-new-document-segmentation-feature-7a58b44d32c2){: external} blog post on Medium.com.

When you split a document, the original document is broken into segments. Each segment contains a more uniform set of information. By splitting the content in your documents into segmented groups, you can enrich and index your data at a more granular level.

To control how your documents are split, you specify a field, such as `subtitle` or `question`, to use as the page break marker. As a document is reprocessed, it is evaluated from start to end. Whenever the page break marker field occurs, the original document is split and a new segment is created. The splitting continues at each marker field until the original document is broken into multiple segments.

Before you begin, decide which field to use as the page break marker.

- You can use any of the fields that are indexed by default. For more information, see [Fields indexed by default](/docs/discovery-data?topic=discovery-data-configuring-fields#sdu-default-fields).
- If the fields that are created by default don't meet your needs, you can use the Smart Document Understanding tool to define a custom field, and then split documents by the custom field. For more information, see [Using Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields).
- The number of segments per document is limited to `1,000`. After segment number `999` is created, any remaining document content is stored within segment `1,000`.
- Metadata from PDF and Microsoft Word documents and any custom metadata is extracted and included in the index with each segment.

To split the documents in a collection, complete the following steps:

1.  Click **Manage collections** from the navigation pane, and then click to open a collection.
1.  Open the **Manage fields** page.

    A list of the identified fields is displayed.
1.  From the *Improve query results by splitting your documents* section, click **Split document**.
1.  Choose the field that you want to use as your page break marker from the **Select field** dropdown.

    The list that you can choose from includes a subset of all the identified fields.
1.  Click **Apply changes and reprocess**.

You can check the status of the splitting process from the *Activity* page.

## Updating documents that were split
{: #split-documents-update}

If a document that was split changes and you want to upload the document again, work with a developer to replace the document by using the API. A developer can use the POST method to upload the latest version of the document to the `/environments/{environment_id}/collections/{collection_id}/documents/{document_id}` endpoint. For more information, see the [API reference](https://{DomainName}/apidocs/discovery-data#updatedocument){: external}. To provide the `{document_id}` path variable that must be sent with the request, copy the contents of the `parent_id` field of one of the document's segments.

When you replace the original document, all of the segments are overwritten, unless the updated version of the document has fewer total sections than the original. Those older segments remain in the index. A developer can delete each remaining segment separately by using the API. For more information, see the [delete document API](https://{DomainName}/apidocs/discovery-data#deletedocument){: external}.
