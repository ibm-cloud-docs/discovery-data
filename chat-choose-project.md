---

copyright:
  years: 2021
lastupdated: "2021-10-12"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Choosing the right project type for a chatbot
{: #chat-choose-project}

For a straightforward solution to deliver answers from a virtual assistant that is built with {{site.data.keyword.conversationshort}}, choose the *Conversational Search* project type. For more complex use cases, consider using the *Document Retrieval* project type.
{: shortdesc}

When you create a project to support a chatbot, you must choose the type of project to store your data collections. Most often, the *Conversational Search* project type is the right choice. You get great results from the start, and when you enable extra features like *FAQ extraction* and *Emphasize the answer*, the answers are clear and concise. For advanced use cases, where you have complex data or need to return long answers, you can evaluate whether using a *Document Retrieval* project type is a better fit.

To help you choose the right {{site.data.keyword.discoveryshort}} project type, review the project type differences that are described in the following table.

| Function | Conversational Search | Document Retrieval |
|----------|-----------------------|--------------------|
| Enrichment support | No enrichments are applied automatically. | The *Parts of Speech* and *Entities* enrichments are applied to collections that you add to this project type automatically. These enrichments are helpful for identifying important information and introduce more ways to filter query results. |
| Testing queries from the *Improve and customize* page in {{site.data.keyword.discoveryshort}} | You see only one of the responses that will be returned from the chatbot. You cannot see all of the available responses and cannot analyze individual query results. | You can filter query results by enrichment-based facets. You can review details about fields that are indexed in the source documents that are returned for a query. Access to more information makes it easier to troubleshoot unexpected results. |
| Search triggers | Returns answers from the `text` field automatically. If answers are stored in another field, you must change the configuration. | You can apply a Smart Document Understanding (SDU) model or enrichments to your collections and retrieve useful information from fields other than `text` when search is triggered from the assistant. |
{: caption="Project type details" caption-side="top"}

For both project types, the best way to test is to trigger search from the {{site.data.keyword.conversationshort}} preview. When you configure search support for an assistant, you can fine-tune the experience in ways that aren't available in {{site.data.keyword.discoveryshort}}. And settings that are available from the *Search results* tool for a *Document Retrieval* project type are replaced by configuration settings that you specify in {{site.data.keyword.conversationshort}}. For example, the query response title and body are defined in {{site.data.keyword.conversationshort}}. And a passage length of 325 characters is applied to responses regardless of what you specify in the **Max characters in a passage** field.

The way you deploy search support in your chatbot is the same regardless of the project type. You simply enable search support in your assistant and then publish your assistant.

If you decide that you want to use a *Document Retrieval* project type, you must create it *before* you add the search function to your virtual assistant. Otherwise, when you add search support to your assistant, a *Conversational Search* project is created for you automatically. When you have a service instance that contains a *Document Retrieval* project already, the {{site.data.keyword.conversationshort}} user interface shows the existing instance, and you can choose to use it.
{: note}

For more information about configuring search support from {{site.data.keyword.conversationshort}}, read the appropriate documentation for your situation.

- From an actions skill, see [Configuring the search for an answer](/docs/assistant?topic=assistant-actions#actions-what-next-search){: external}.
- From a dialog skill, see [Adding a search skill response type](/docs/assistant?topic=assistant-dialog-overview#dialog-overview-add-search-skill){: external}.
- From the new Beta user interface, see [Search trigger](/docs/watson-assistant?topic=watson-assistant-search-add#search-add-trigger){: external}.

## How the assistant calls Discovery
{: #chat-choose-project-api}

When a user asks your assistant a question that triggers search, the following API request is sent to Discovery if *Emphasize the answer* is enabled:

```json
{
    "aggregation": "",
    "sort": "",
    "count": 10,
    "return": [],
    "filter": <custom_filter_specified_in_assistant>
    "passages": {
		"enabled": "true",
      	"fields": [
        	<search_config_body_field_specified_in_assistant>
      	],
      	"characters": 325,
      	"per_document": true,
      	"max_per_document": 3,
        "find_answers": true,
        "max_answers_per_passage": 1
    },
    "highlight": false,
    "spelling_suggestions": false,
    "table_results": {
      	"enabled": false
    },
    "suggested_refinements": {
      	"enabled": false
    }
}
```
{: codeblock}

When *Emphasize the answer* is used (`"find_answers": true`), Discovery rescores and reorders the documents to ensure that documents with the highest-quality answers are returned first.
