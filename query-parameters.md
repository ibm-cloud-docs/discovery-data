---

copyright:
  years: 2019
lastupdated: "2019-06-24"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Query parameters
{: #query-parameters}

{{site.data.keyword.discovery-data_long}} queries can include both search and structure parameters.
{: shortdesc}

{{site.data.keyword.discovery-data_short}} includes the following parameters. Most are available on the **Query** screen, though a few are only available when using the API. To access the **Query** screen, [create a new collection (or open an existing one)](/docs/services/discovery-data?topic=discovery-data-collections#collections), and click the **Query** tab. 

See [Query concepts](/docs/services/discovery-data?topic=discovery-data-query-concepts#query-concepts) for more on querying. 

**Search parameters**

Search parameters enable you to search your collection, identify a result set, and perform analysis on the result set.

The **results set** is the group of documents identified by the combined searches of the search parameters. The results set may be significantly larger than the returned results. If an empty query is performed, the results set is equal to all the documents in the collection.

Documents you do not have permissions for will not be returned in query results.
{: important}

## natural_language_query
{: #nlq}

Field on the **Query** screen: **Use natural language**

A natural language query enables you to perform queries expressed in natural language, as might be received from an end user in a conversational or free-text interface - for example: "IBM Watson in healthcare". The parameter uses the entire input as the query text. It does **not** recognize operators. The `natural_language_query` parameter enables capabilities such as relevancy training. Query results will include a `confidence` score. See [confidence scores](/docs/services/discovery-data?topic=discovery-data-confidence#confidence). The maximum query string length for a natural language query is `2048`.

## query
{: #query}

Field on the **Query** screen: **Use the {{site.data.keyword.discoveryshort}} Query Language** 

A query search returns all documents in your data set with full enrichments and full text in order of relevance. A query also excludes any documents that don't mention the query content. These queries are written using the [{{site.data.keyword.discoveryshort}} Query Language](/docs/services/discovery-data?topic=discovery-data-query-operators#query-operators).

## aggregation
{: #aggregation}

Field on the **Query** screen: **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** 

Aggregation queries return a count of documents matching a set of data values. For the full list of aggregation options, see the [Aggregations table](/docs/services/discovery-data?topic=discovery-data-query-aggregations#query-aggregations). 


## filter
{: #filter}

Field on the **Query** screen: **Write a filter to narrow down the document set using the Discovery Query Language** 

A cacheable query that excludes any documents that don't mention the query content. Filter search results are **not** returned in order of relevance. 

### Differences between the filter and query parameters
{: #filtervquery}

If you test the same search term on a small data set, you might find that the `filter` and `query` parameters return very similar (if not identical) results. However, there is a difference between the two parameters.

- Using a filter parameter alone will return search results in no specific order.
- Using a query parameter alone will return search results in order of relevance.

In large data sets, if you need results returned in order of relevance, you should combine the `filter` and `query` parameters, because using them together will improve performance. This is because the `filter` parameter will run first and cache results, then the `query` parameter will rank them. For an example of using filters and queries together, see [Building combined queries](/docs/services/discovery-data?topic=discovery-data-query-concepts#building-combined-queries). Filters can also be used in aggregations.

When you write a query that includes both a `filter`, and an `aggregation`, `query`, or `natural_language_query` parameter; the `filter` parameters run first, after which any `aggregation`, `query`, or `natural_language_query` parameters run in parallel.

With a simple query, especially on a small data set, `filter` and `query` often return the exact same (or similar) results. If a `filter` and `query` call return similar results, and getting a response in order of relevance does not matter, it is better to use filter because filter calls are faster and are cached. Caching means that the next time you make that call, you get a much quicker response, particularly in a big data set.


**Structure parameters**

Structure parameters define the content and organization of the documents in the returned JSON. This includes the number of results retuned, where in the results set to start returning documents, how the result set is sorted, which fields to return for each documents, if duplicate documents should be removed, and if relevant passages should be extracted from the results set. Structure parameters don't affect which documents are part of the entire results set.

## return
{: #return}

Field on the **Query** screen: **Fields to return** 

A comma-separated list of the portion of the document hierarchy to return. Any of the document hierarchy are valid values.

## count
{: #count}

Field on the **Query** screen: **Number of documents to return** 

The number of documents that you want returned in the response. The default is `10`. The maximum for the `count` and `offset` values together in any one query is `10000`.

## offset
{: #offset}

Field on the **Query** screen: **Number of query results to skip at the beginning** 

For example, if the total number of results that are returned is 10, and the offset is 8, it returns the last two results. The default is `0`. The maximum for the `count` and `offset` values together in any one query is `10000`.

## spell correction
{: #spell}

In natural language queries, you can spell check the `natural_language_query` parameter. The most likely correction is returned in the `suggested_query` field of the response (if one exists).

## sort
{: #sort}

The `sort` parameter is currently available for use only with the API.
{: note}

A comma-separated list of fields in the document to sort on. You can optionally specify a sort direction by prefixing the field with `-` for descending order or `+` for ascending order. Ascending order is the default sort direction.

## highlight
{: #highlight}

The `highlight` parameter is currently available for use only with the API.
{: note}

A boolean that specifies whether the returned output includes a `highlight` object in which the keys are field names and the values are arrays that contain segments of query-matching text highlighted by the HTML `*` tag.

The output lists the `highlight` object after the `enriched_text` object, as shown in the following example.

```bash
curl -u "apikey":"{apikey_value}" "https://gateway.watsonplatform.net/discovery/api/v1/environments/{environment_id}/collections/{collection_id}/query?version=2017-06-25&natural_language_query=Hybrid%20cloud%20companies&highlight=true"
```
{: pre}

The JSON that is returned will be of the following format:

```json
{
  "highlight": {
    "extracted_metadata.title": [
      "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>"
    ],
    "enriched_text.concepts.text": [
      "Privately held <em>company</em>",
      "<em>Cloud</em> computing"
    ],
    "text": [
      " Sanovi Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em> recovery, <em>cloud</em> migration",
      "IBM to Acquire Sanovi Technologies to Expand Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em>\n\nPublished",
      " undergoing digital and <em>hybrid</em> <em>cloud</em> transformation.\n\nURL: http://www.ibm.com/press/us/en/pressrelease/50837.wss",
      " and business continuity software for enterprise data centers and <em>cloud</em> infrastructure. Adding"
    ],
    "enriched_text.categories.label": [
      "/business and industrial/<em>company</em>/bankruptcy"
    ],
    "enriched_text.entities.type": [
      "<em>Company</em>"
    ],
    "html": [
      " Technologies, a privately held <em>company</em> that provides <em>hybrid</em> <em>cloud</em>\n recovery, <em>cloud</em> migration and business",
      " Disaster Recovery Services for <em>Hybrid</em> <em>Cloud</em></title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01",
      " digital and <em>hybrid</em> <em>cloud</em> transformation.</p>\n<p>URL: http://www.ibm.com/press/us/en/pressrelease/50837.wss</p>\n\n\n\n</body></html>",
      " continuity software for \nenterprise data centers and <em>cloud</em> infrastructure. Adding these \ncapabilities"
    ]
  }
}
```
{: codeblock}
