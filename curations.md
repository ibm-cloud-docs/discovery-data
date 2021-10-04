---

copyright:
  years: 2019, 2021
lastupdated: "2021-06-16"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Curations
{: #curations}

The Curations feature is beta functionality.
{: beta}

Use curations to specify the exact document to return in response to a specific query. Curations can guarantee that frequent or important questions always return the most valuable document. The `confidence_score` for a curated query will always be `1.00000`.

This beta feature is only available when using the API and can be used to specify up to 1,000 curations. For details, see [Create curation](https://{DomainName}/apidocs/discovery-data#createcuration){: external} in the API reference.

This example shows how a curation is added with the API. When querying with the same or similar `natural_language_query` the document with the `document_id` of `document_id1234` is returned.

```JSON
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
