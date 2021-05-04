---

copyright:
  years: 2019, 2021
lastupdated: "2021-05-03"

keywords: preview link, share link

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

# Testing your project
{: #test}

As you improve your project, periodically test how enrichments and search setting changes impact the query results.
{: shortdesc}

For all project types except Conversational Search, you can see the fields that are associated with an indexed document by looking at the JSON view of a document that is returned by a query. Checking the JSON structure of a document can be useful if you want to check whether certain types of information are being captured.

After you enrich your collection, you can use the JSON view of a query result to check whether your enrichments are being applied and retrieved properly. For example, you can check the JSON to confirm that a synonym that you defined in a dictionary is being tagged as an occurrence of the corresponding dictionary term.

To test your project, complete the following steps:

1.  From the navigation pane, open the **Improve and customize** page.
1.  Retrieve query results by doing one of the following things:

    - *Content Mining* project: Choose or add a facet to apply to the documents, and then click **View filtered documents**.
    - Other project types: Enter a test query to submit or leave the field empty and press Enter to submit an empty query.
1.  From the query result list, click the link to view the document.
1.  Click **JSON** to view the query result in JSON format.
