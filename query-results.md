---

copyright:
  years: 2020, 2021
lastupdated: "2021-04-12"

keywords: passages, query results

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

# Previewing the default query results
{: #query-results}

See the types of query results that are returned automatically and learn about how they are derived. Understanding how default results are created can help you decide next steps to improve your results.
{: shortdesc}

When a document is ingested, the text is extracted and indexed in the`text` field. When a customer searches a collection at run time, you don't want every word in a 10,000-word document to be returned as the query result. Instead, you want to return a subsection of the text from the original document that contains only information that is relevant to the query. {{site.data.keyword.discoveryshort}} achieves this goal by returning *passages* from the `text` field in all project types except Content Mining. For more information about passages, see [How passages are derived](#query-results-passages).

Preview the default query results.

- For a Document Retrieval project:

  - Click **Run search** for one of the keywords that {{site.data.keyword.discoveryshort}} calculated to have special meaning in your collection.
  - Submit your own phrase or keyword from the search bar.

  You can see that the query results that are returned consist of passages. Entities that are recognized in your documents (based on the Entities enrichment that is applied to the project by default) are displayed as facets by which you can filter the query results.

- For Document Retrieval with Content Intelligence projects, contract-related elements that are recognized in your collection are displayed. You can filter the documents by one of the highlighted elements or by entities that are recognized in your documents (based on the Entities enrichment that is applied to the project by default).
- For Conversational Search projects, a single search field is displayed that mimics the user interface of an assistant.
- For Content Mining projects, choose a facet by which to filter the documents. Facets based on the Parts of Speech enrichment that is applied to the project by default are shown.
- Even Custom project types show query results as passages by default.

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: The following optional project configuration setting impacts how the query results are formatted:

- If you enable FAQ extraction, each question-and-answer pair that is found in the original document is added to a new, separate document with the question in the `title` field and answer in the `text` field. By separating the pairs into independent documents, the right answer can be returned quickly when a phrase that is the same or similar to the associated question is submitted as the query.

## Improving your query results
{: #query-results-improve}

Use the tools built in to {{site.data.keyword.discoveryshort}} to make the following types of improvements:

- Prepare your documents a bit more before you enrich them. Add to the set of fields that are indexed in your documents by default. You can use Smart Document Understanding to identify additional sections of your document that contain valuable information. You can also split large documents into more easily consumable chunks. For more information, see [Adding custom fields with Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields).
- Use Watson Natural Language Understanding to find and tag terms that are generally understood to have special meaning. For more information, see [Applying prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu).
- Teach {{site.data.keyword.discoveryshort}} about terms and patterns that have special meaning to your use case. For more information, see [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain).
- For a Content Mining project, you might want to add facets based on enrichments other than the Parts of Speech enrichment that is applied by default. For more information, see [Facets](/docs/discovery-data?topic=discovery-data-facets).

If the right type of information is being identified and tagged in your documents already, learn steps that you can take to tweak query results that are returned to improve their relevancy. For more information, see [Search settings](/docs/discovery-data?topic=discovery-data-search-settings).

### How passages are derived
{: #query-results-passages}

{{site.data.keyword.discoveryshort}} uses sophisticated algorithms to determine the best passages of text from all of the documents that are returned by a query. Passages are returned per document by default. They are displayed as a section within each document query result and are ordered by passage relevance.

{{site.data.keyword.discoveryshort}} uses sentence boundary detection to pick a passage that includes a full sentence. It searches for passages that have an approximate length of 200 characters, then looks at chunks of content that are twice that length to find passages that contain full sentences. If the sentences in your documents are extra long, the query might not be able to capture a full sentence. As a result, some passages that are returned might not include an entire sentence or might omit the beginning or ending of a sentence. Sentence boundary detection works for all supported languages and uses language-specific logic.

You can change the default character length and make other customizations by using the API. For example, if your application has limited screen space, you might want to search for passages that are shorter than 200 characters.

When you deploy your project, you can use the APIs to define more complex queries that can take advantage of the enrichments in a collection. For more information, see [Query overview](/docs/discovery-data?topic=discovery-data-query-concepts).
