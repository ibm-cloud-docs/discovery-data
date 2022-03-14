---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-14"

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

   To delete a document, complete the following steps:

   1. From the navigation pane, open the **Manage collections** page, and then click a collection to open it.
   1. Click the **Manage data** tab.

      A list of information from each document in the collection is displayed. If the information that is displayed doesn't help you identify the document that you want to delete, you can change what is displayed.

      -   Click the *Settings* icon in the table header.
      -   Choose a field from which you want to fetch data to display in the first and second columns. You can choose fields such as `extracted_metadata.filename` to show the document file name, or `document_id`, for example.

      Remember that you can page through the documents in the collection by using the controls in the table footer.

   1. After you identify the document that you want to delete, select the document, and then click **Delete**. Confirm the deletion.
