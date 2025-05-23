---

copyright:
  years: 2020, 2025
lastupdated: "2025-02-13"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Excluding content from query results
{: #hide-data}

Prevent content that you don't want customers to see from being included in query results.
{: shortdesc}

You can prevent content from being included in query results in the following ways:

- Delete an entire collection.

   For more information, see [Deleting collections](/docs/discovery-data?topic=discovery-data-manage-collections#collection-delete).

- Remove a field from the index that contains data that you don't want to share with customers.

   You can control which fields are indexed. If you want to prevent a field from being indexed, you can set it to be excluded. For example, if your PDF files contain a running header or footer that does not contain useful information, you can exclude the `header` and `footer` fields from the index.

   To manage the fields to index, complete the following steps:

   1. From the navigation pane, open the **Manage collections** page, and then click a collection to open it.
   1. Click the **Manage fields** tab.

      A list of the identified fields is displayed. You can see which fields are included in the index and which are not.

   1. To remove a field from the index, set the **Include** switch to off.

- Delete a single document.

   If you use the Smart Document Understanding tool to annotate a document, and then decide that you want to delete the document and its associated SDU annotations, you must remove the annotations before you delete the document. To remove the annotations, annotate the document again. This time, label all of the content as `text`.
   {: note}

   To delete a document, complete the following steps:

   1. From the navigation pane, open the **Manage collections** page, and then click a collection to open it.
   1. Click the **Manage data** tab.

      A list of information from each document in the collection is displayed. If the information that is displayed doesn't help you identify the document that you want to delete, you can change what is displayed.

      -   Click the *Settings* icon in the table header.
      -   Choose fields from which you want to fetch data to display in the first and second columns. You can choose fields such as `extracted_metadata.filename` to show the document file name, or `document_id`, for example.

      You can page through the documents in the collection by using the controls in the table footer.
      {: tip}

   1. After you identify the document that you want to delete, select the checkbox that is associated with the document, and then click **Delete**. Confirm the deletion.

      Documents that are added to a collection from an external data source will be added back to the collection with the next scheduled crawl of the data source. The delete function removes the document from the index of the collection, not from the external data source.

      Some file types, such as CSV or JSON files, generate subdocuments when they are added to a collection. Splitting a document turns one document into multiple document segments. If you delete one of these generated documents, and then repeat the action that created it, the deleted document is added back in to your collection. To completely delete the original document, you must delete the parent document by using the [Delete document](/apidocs/discovery-data#deletedocument) API and remove the original document from the crawled data source.
      {: note}

   [IBM Cloud Pak for Data]{: tag-cp4d} **{{site.data.keyword.icp4dfull_notm}} releases before 4.6.5**

   The *Manage data* page is not available in installed deployments before the 4.6.5 release. You must use the [Discovery API](/apidocs/discovery-data#deletedocument) to delete a document. And you must know the document ID of the document that you want to delete. To get the document ID, use the [List documents](/apidocs/discovery-data#listdocuments) API method.

   If the document is a subdocument of another document and you want to remove it, its parent, and any other subdocuments that are associated with the parent, delete the parent document. To get the document ID of the parent document, look for the `metadata.parent_document_id` field for the document. It is specified in the JSON representation of the document when it is returned as a response in the *Improve and customize* page of the product user interface.
