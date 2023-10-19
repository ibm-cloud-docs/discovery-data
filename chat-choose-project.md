---

copyright:
  years: 2021, 2023
lastupdated: "2023-10-12"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Searching {{site.data.keyword.discoveryshort}} data from {{site.data.keyword.conversationshort}}
{: #chat-choose-project}

Your {{site.data.keyword.discoveryshort}} project can provide answers to questions that stump your assistant. Instead of answering with “I don't know”, your assistant can say, “I'm not sure, but I searched my knowledge base and found these answers which might help.” 
{: shortdesc}

For more information about how to search a {{site.data.keyword.discoveryshort}} project from an assistant, read the appropriate {{site.data.keyword.conversationshort}} documentation for your situation.

- From the new experience user interface, see [Search trigger](/docs/watson-assistant?topic=watson-assistant-search-add#search-add-trigger){: external}.
- From an actions skill in the classic user interface, see [Configuring the search for an answer](/docs/assistant?topic=assistant-actions#actions-what-next-search){: external}.
- From a dialog skill, see [Adding a search skill response type](/docs/assistant?topic=assistant-dialog-overview#dialog-overview-add-search-skill){: external}.

If you use the built-in web chat, you can use answer finding by enabling the *Emphasize the answer* feature. Answer finding highlights the word or phrase in the search result that is determined to be the exact answer to the customer's question.
{: tip}

For a more detailed look at the steps to take to connect to a {{site.data.keyword.discoveryshort}} project from {{site.data.keyword.conversationshort}}, take a tutorial that walks you through them. For more information, see [Power your assistant with answers from web resources](/docs/discovery-data?topic=discovery-data-tutorial-assistant-fred).

Alternatively, you can add a generative language service named NeuralSeek between the Watson {{site.data.keyword.discoveryshort}} and {{site.data.keyword.conversationshort}} services. For more information, see [Use NeuralSeek to return polished answers from existing help content](/docs/watson-assistant?topic=watson-assistant-tutorial-neuralseek){: external}.

## How the assistant calls Discovery
{: #chat-choose-project-api}

When a user asks your assistant a question that triggers a search, the following API request is sent to {{site.data.keyword.discoveryshort}} if *Emphasize the answer* is enabled.

The *Emphasize the answer* feature is available from instances that are managed by {{site.data.keyword.cloud_notm}} only.
{: note}

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

## Choosing a project type
{: #chat-choose-project-type}

If the *Conversational Search* project type isn't providing the best answers and you want to understand why, switch to using a *Document Retrieval* project type.

Most often, the *Conversational Search* project type is the right choice. You get great results from the start, and when you enable extra features like *Emphasize the answer*, the answers are clear and concise. However, for advanced use cases, or if you want to be able to troubleshoot issues, a *Document Retrieval* project type might be a better fit.

To help you choose the right {{site.data.keyword.discoveryshort}} project type, review the project type differences that are described in the following table.

| Function | Conversational Search | Document Retrieval |
|----------|-----------------------|--------------------|
| Enrichment support | No default enrichments are applied. | The *Entities* enrichment is applied. The Entities enrichment is helpful for identifying important information and introduces more ways to filter query results. |
| Testing queries from the *Improve and customize* page in {{site.data.keyword.discoveryshort}} | You see only one of the responses that are returned from the chatbot. You cannot see all of the available responses and cannot analyze individual query results. | You can filter query results by enrichment-based facets. You can review details about fields that are indexed in the source documents that are returned for a query. Access to more information makes it easier to troubleshoot unexpected results. |
| Search triggers | Returns answers from the `text` field automatically. If answers are stored in another field, you must change the configuration. | You can apply a Smart Document Understanding (SDU) model or enrichments to your collections and retrieve useful information from fields other than `text` when search is triggered from the assistant. |
{: caption="Project type details" caption-side="top"}

For both project types, the best way to test is to trigger search from the {{site.data.keyword.conversationshort}} preview. When you configure search support for an assistant, you can fine-tune the experience in ways that aren't available in {{site.data.keyword.discoveryshort}}. 

And settings that are available from the *Search results* tool for a *Document Retrieval* project type are replaced by configuration settings that you specify in {{site.data.keyword.conversationshort}}. For example, the query response title and body are defined in {{site.data.keyword.conversationshort}}. And a passage length of 325 characters is applied to responses regardless of what you specify in the **Max characters in a passage** field.

The way that you deploy search support in your chatbot is the same regardless of the project type. You enable search support in your assistant and then publish your assistant.

If you decide that you want to use a *Document Retrieval* project type, you must create it *before* you add the search function to your virtual assistant. Otherwise, when you add search support to your assistant, a *Conversational Search* project is created for you automatically. When you have a service instance that contains a *Document Retrieval* project already, the {{site.data.keyword.conversationshort}} user interface shows the existing instance, and you can choose to use it.
{: note}
