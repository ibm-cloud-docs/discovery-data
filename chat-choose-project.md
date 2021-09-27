---

copyright:
  years: 2021
lastupdated: "2021-09-27"

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

# Choosing the right project type for a chatbot
{: #chat-choose-project}

For a straightforward solution to deliver answers from a virtual assistant that is built with {{site.data.keyword.conversationshort}}, choose the *Conversational Search* project type. For more complex use cases, consider using the *Document Retrieval* project type.
{: shortdesc}

When you create a project to support a chatbot, you must choose the type of project to store your data collections. To help you make the decision, review the differences in the {{site.data.keyword.discoveryshort}} project types that are described in the following table.

| Function | Conversational Search | Document Retrieval |
|----------|-----------------------|--------------------|
| Enrichment support | No enrichments are applied automatically. | The *Parts of Speech* and *Entities* enrichments are applied to collections that you add to this project type automatically. These enrichments are helpful for identifying important information and introduce more ways to filter query results. |
| Testing queries from the *Improve and customize* page in {{site.data.keyword.discoveryshort}} | You see only the response that the chatbot will return. You cannot analyze individual query results. | You can filter query results by enrichment-based facets. You can review details about fields that are indexed in the source documents that are returned for a query. Access to more information makes it easier to troubleshoot unexpected results. |
| Search triggers | Returns answers from the `text` field only. | You can apply a Smart Document Understanding (SDU) model or enrichments to your collections and retrieve useful information from fields other than `text` when search is triggered from the assistant. |
{: caption="Project type details" caption-side="top"}

The way you deploy search support in your chatbot is the same regardless of the project type. You simply enable search support in your assistant and then publish your assistant.

If you decide that you want to use a *Document Retrieval* project type, you must create it *before* you add the search function to your virtual assistant. Otherwise, when you add search support to your assistant, a *Conversational Search* project is created for you automatically. When you have a service instance that contains a *Document Retrieval* project already, the {{site.data.keyword.conversationshort}} user interface shows the existing instance, and you can choose to use it.
{: note}

For more information about configuring search support from {{site.data.keyword.conversationshort}}, read the appropriate documentation for your situation.

- From an actions skill, see [Configuring the search for an answer](/docs/assistant?topic=assistant-actions#actions-what-next-search){: external}.
- From a dialog skill, see [Adding a search skill response type](/docs/assistant?topic=assistant-dialog-overview#dialog-overview-add-search-skill){: external}.
<!-- From the new Beta user interface, see [Search trigger](/docs/watson-assistant?topic=watson-assistant-search-add#search-add-trigger){: external}.-->

If you choose to use a *Document Retrieval* project type with your virtual assistant, filter the query results to show matches from a single collection at a time. Although you can add up to 5 collections to both project types in {{site.data.keyword.discoveryshort}}, you can choose only one collection to connect to from {{site.data.keyword.conversationshort}}. To ensure that your tests reflect how the search will function in reality, limit the search to one collection. You can test more than one collection to find the one that returns the best answers, and then connect to that collection from your assistant.
{: tip}
