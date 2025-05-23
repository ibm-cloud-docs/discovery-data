---

copyright:
  years: 2019, 2025
lastupdated: "2023-03-22"

keywords: curation,snippet,hard-coded answers

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Curations API
{: #curations}

The Curations feature is beta functionality.
{: beta}

Use curations to specify the exact document to return in response to a specific natural language query. Curations can guarantee that frequent or important questions always return the most valuable document. The `confidence_score` for a curated query is always `1.00000`.

This beta feature is only available from the API and is applied only to natural language queries, not queries that are specified by using the Discovery Query Language. Beta features are not available from the SDKs. 

You can define up to 1,000 curations. For more information, see [Create curation](https://{DomainName}/apidocs/discovery-data#createcuration){: external} in the API reference.

This example shows how a curation is added with the API. When querying with the same or similar `natural_language_query` the document with the `document_id` of `document_id1234` is returned.

```json
{
  "natural_language_query": "curations in watson discovery",
  "curated_results": [
     {
       "document_id": "document_id1234",
      "collection_id": "collection_id1234"
     }
   ]
 }
```
{: codeblock}

The natural language query that is submitted by the customer must be an exact match for the query that is specified in the curation. Both queries, the one submitted by the user at run time and the one that is submitted by the curation API and then stored in the index, undergo query analysis. The query analyzer lemmatizes text, removes stop words, and adds query expansions.

You can optionally specify a hard-coded response to the query by including a snippet. A snippet is a response that you author and that is returned when the associated document is returned for the specified natural language query.

```json
{
  "curations": [
    {
      "curation_id": "c1175536f509405bc68a9f76235fa7bbb6f9af2f",
      "natural_language_query": "What is a project",
      "curated_results": [
        {
          "collection_id": "47477591-b520-6039-0000-017ea213e837",
          "document_id": "web_crawl_123a2a56-8c26-5acb-9544-c4702ac899a4",
          "snippet": "A project is a convenient way to collect and manage the resources in your application. You can assign a project type and connect your data to the project by creating a collection."
        }
      ]
    }
  ]
}
```
{: codeblock}

If **passages.per_document** is `true`, the text snippet that you specify is returned as the top passage in the `passage_text` field instead of the original passage that is chosen by search. Only one text snippet can be specified per document. If **passages.max_per_document** is greater than `1`, the snippet is returned first, followed by the passages that are chosen by search. Query filters are applied to curation results.
