---

copyright:
  years: 2020, 2021
lastupdated: "2021-04-06"

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

The bulk of content from documents that you add to a collection is stored in a single `text` field. When a customer searches a collection at run time, you don't want every word in a 10,000-word document to be returned as the query result. Instead, you want to return a subsection of the text from the original document that contains only information that is relevant to the query. {{site.data.keyword.discoveryshort}} achieves this goal by returning *passages* from the `text` field in all project types except Content Mining and Document Retrieval with Content Intelligence. For more information about passages, see [How passages are derived](#query-results-passages).

Preview the default query results.

- For a Document Retrieval project:

  - Click **Run search** for one of the keywords that {{site.data.keyword.discoveryshort}} calculated to have special meaning in your collection.
  - Submit your own phrase or keyword from the search bar.

  You can see that the query results that are returned consist of passages. Entities that are recognized in your documents (based on the Entities enrichment that is applied to the project by default) are displayed as facets by which you can filter the query results.

- For Document Retrieval with Content Intelligence projects, contract-related elements that are recognized in your collection are displayed. You can filter the documents by one of the highlighted elements or by entities that are recognized in your documents (based on the Entities enrichment that is applied to the project by default).
- For Conversational Search projects, a single search field is displayed that mimics the user interface of an assistant.
- For Content Mining projects, choose a facet by which to filter the documents. Facets based on the Parts of Speech enrichment that is applied to the project by default are shown.
- Even Custom project types show query results as passages by default.

The following optional project configuration settings impact how the query results are formatted:

- ![IBM Cloud only](images/ibm-cloud.png): If you enable FAQ extraction, any question-and-answer pairs that are found in the original document are added to a new, separate document. By separating the pairs into independent documents, the right answer can be returned quickly when a phrase that is the same or similar to the associated question is submitted as the query.

- When you split documents, you break up text from the original single document into multiple smaller documents or *segments* of the original document. Each document segment contains a smaller chunk of the original text. The content <!--in the `text` field--> of each document segment is then broken up into passages.

## Improving your query results
{: #query-results-improve}

Use the tools built in to {{site.data.keyword.discoveryshort}} to make the following types of improvements:

- Use Watson NLP to find and tag terms that are generally understood to have special meaning. For more information, see [Enrich your data with Watson NLP](/docs/discovery-data?topic=discovery-data-nlp).
- Teach {{site.data.keyword.discoveryshort}} about terms and patterns that have special meaning to your use case. For more information, see [EAdding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain).
- Help {{site.data.keyword.discoveryshort}} to interpret meaning based on the format of the source documents. For example, extract information that is displayed in tables or use Smart Document Understanding to illustrate that in a PDF, phrases in 36 pt font represent titles and in 28 pt font represent subtitles.
- For a Content Mining project, you might want to add facets based on enrichments other than the Parts of Speech enrichment that is applied by default. For more information, see [Facets](/docs/discovery-data?topic=discovery-data-facets).

If the right type of information is being identified and tagged in your documents already, learn about steps you can take to tweak query results that are returned to improve their relevancy. For more information, see [Search settings](/docs/discovery-data?topic=discovery-data-search-settings).

### How passages are derived
{: #query-results-passages}

{{site.data.keyword.discoveryshort}} uses sophisticated algorithms to determine the best passages of text from all of the documents that are returned by a query. Passages are returned per document by default. They are displayed as a section within each document query result and are ordered by passage relevance.

{{site.data.keyword.discoveryshort}} uses sentence boundary detection to pick a passage that includes a full sentence. It searches for passages that have an approximate length of 400 characters, then looks at chunks of content that are twice that length to find passages that contain full sentences. If the sentences in your documents are extra long, the query might not be able to capture a full sentence. As a result, some passage that are returned might not include an entire sentence or might omit the beginning or ending of a sentence. Sentence boundary detection works for all supported languages and uses language-specific logic.

You can change the default character length and make other customizations by using the API. For example, if your application has limited screen space, you might want to search for passages that are shorter than 400 characters. 

When you deploy your project, you can use the APIs to define more complex queries that can take advantage of the enrichments in a collection. For more information, see [Query overview](/docs/discovery-data?topic=discovery-data-query-concepts).
