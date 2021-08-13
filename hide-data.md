---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-13"

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

# Preventing content from being returned
{: #hide-data}

Prevent content that you don't want customers to see from being included in query results.
{: shortdesc}

You can prevent content from being included in query results in the following ways:

- Delete an entire collection. 

  For more information, see [Deleting collections](/docs/discovery-data?topic=discovery-data-manage-collections#collection-delete).
- Remove a field from the index that contains data that you don't want to share with customers.

  You can control which fields are indexed. If you want to prevent a field from being indexed, you can set it to be excluded. For example, if your PDF files contain a running header or footer that does not contain useful information, you can exclude the `header` and `footer` fields from the index.

  To manage the fields to index, complete the following steps:

  1.  From the navigation pane, open the **Manage collections** page, and then click a collection to open it.
  1.  Click the **Manage fields** tab.

      A list of the identified fields is displayed. You can see which fields are included in the index and which are not.
  1.  To remove a field from the index, set the **Include** switch to off.

- Delete a single document by completing the following steps:

  1.  Get the document ID, which is shown in the JSON view of a query response.

      To list all documents, you can submit an empty query from the *Improve and customize* page.
      {: tip}
  1.  A developer can use the [Delete a document](https://cloud.ibm.com/apidocs/discovery-data#deletedocument){: external} method of the API. The document ID is a required parameter.