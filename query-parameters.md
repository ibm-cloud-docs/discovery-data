---

copyright:
  years: 2019
lastupdated: "2019-11-22"

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

These parameters are used when writing queries with the {{site.data.keyword.discoveryshort}} Query Language. For more information, see the {{site.data.keyword.discovery-data_short}} [API](https://{DomainName}/apidocs/discovery-data-v2#query-a-collection-get). For an overview of query concepts, see the [Query overview](/docs/services/discovery-data?topic=discovery-data-query-concepts).
{: shortdesc}

Queries written in the {{site.data.keyword.discoveryshort}} Query Language can include both search and structure parameters.

**Search parameters**

Search parameters enable you to search your collection, identify a result set, and perform analysis on the result set.

The **results set** is the group of documents identified by the combined searches of the search parameters. The results set may be significantly larger than the returned results. If an empty query is performed, the results set is equal to all the documents in the collection.

Documents you do not have permissions for will not be returned in query results.
{: important}

## natural_language_query
{: #nlq}

A natural language query enables you to perform queries expressed in natural language, as might be received from an end user in a conversational or free-text interface - for example: "IBM Watson in healthcare". The parameter uses the entire input as the query text. It does **not** recognize operators. The `natural_language_query` parameter enables capabilities such as relevancy training. Query results will include a `confidence` score. See [confidence scores](/docs/services/discovery-data?topic=discovery-data-confidence#confidence). The maximum query string length for a natural language query is `2048`.

## query
{: #query}

A query search returns all documents in your data set with full enrichments and full text in order of relevance. A query also excludes any documents that don't mention the query content.

## aggregation
{: #aggregation}

Aggregation queries return a count of documents matching a set of data values. For the full list of aggregation options, see the [Aggregations table](/docs/services/discovery-data?topic=discovery-data-query-aggregations#query-aggregations). 


## filter
{: #filter}

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

A comma-separated list of the portion of the document hierarchy to return. Any of the document hierarchy are valid values.

## count
{: #count}

The number of documents that you want returned in the response. The default is `10`. The maximum for the `count` and `offset` values together in any one query is `10000`.

## offset
{: #offset}

For example, if the total number of results that are returned is 10, and the offset is 8, it returns the last two results. The default is `0`. The maximum for the `count` and `offset` values together in any one query is `10000`.

## spell correction
{: #spell}

In natural language queries, you can spell check the `natural_language_query` parameter. The most likely correction is returned in the `suggested_query` field of the response (if one exists).

## sort
{: #sort}

A comma-separated list of fields in the document to sort on. You can optionally specify a sort direction by prefixing the field with `-` for descending order or `+` for ascending order. Ascending order is the default sort direction.

## highlight
{: #highlight}

A boolean that specifies whether the returned output includes a `highlight` object in which the keys are field names and the values are arrays that contain segments of query-matching text highlighted by the HTML `*` tag.

The output lists the `highlight` object after the `enriched_text` object, as shown in the following example.

```bash
curl -H \"Authorization: Bearer {token}\" 'https://{hostmame}/{instance_name}/v2/projects/{project_id}/collections/{collection_id}/query?version=2019-11-29&natural_language_query=Hybrid%20cloud%20companies&highlight=true"
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

## passages
{: #passages}

A boolean that specifies whether the service returns a set of the most relevant passages from the documents returned by a query that uses the `natural_language_query` parameter. The passages are generated by sophisticated Watson algorithms to determine the best passages of text from all of the documents returned by the query. The default is `false`.

{{site.data.keyword.discovery-data_short}} attempts to return passages that start at the beginning of a sentence and stop at the end using sentence boundary detection. To do so, it first searches for passages approximately the length specified in the [`passages.characters` parameter](/docs/services/discovery-data?topic=discovery-data-query-parameters#passages_characters) (default `400`). It then expands each passage to the limit of twice the specified length in order to return full sentences. If your `passages.characters` parameter is short and/or the sentences in your documents are very long there may be no sentence boundaries close enough to return the full sentence without going over twice the requested length. In that case, {{site.data.keyword.discovery-data_short}} stays within the limit of twice the `passages.characters` parameter, so the passage returned will not include the entire sentence and omit the beginning, end, or both.

Since sentence boundary adjustments expand passage size, you will see a substantial increase in average passage length. If your application has limited screen space, you may want to set a smaller value for `passages.characters` and/or truncate the passages that are returned by {{site.data.keyword.discovery-data_short}}. Sentence boundary detection works for all supported languages and uses language-specific logic.

Passages are returned `per_document` by default. This means they will appear as a section within each document result ordered by passage relevance. Including passage retrieval in queries can increase response times as it includes additional scoring of the passages.

You can adjust the fields in the documents over which passage retrieval searches with the [`passages.fields`](/docs/services/discovery-data?topic=discovery-data-query-parameters#passages_fields) parameter.

The `passages` parameter returns matching passages (`passage_text`), as well as the `score`, `document_id`, the name of the field the passage was extracted from (`field`), and the starting and ending characters of the passage text within the field (`start_offset` and `end_offset`), as shown in the following example.

```bash
 curl -H \"Authorization: Bearer {token}\" 'https://{hostmame}/{instance_name}/v2/projects/{project_id}/collections/{collection_id}/query?version=2019-11-29&natural_language_query='Hybrid%20cloud%20companies'&passages=true"
```
{: pre}

The JSON that is returned from the query will be of the following format:

```json
 {
   "matching_results":2,
   "passages":[
     {
       "document_id":"ab7be56bcc9476493516b511169739f0",
       "passage_score":15.230205287402338,
       "passage_text":"a privately held company that provides hybrid cloud recovery, cloud migration and business continuity software for enterprise data centers and cloud infrastructure."
       "start_offset":120
       "end_offset":300
       "field":"text"       
     },
     {
       "passage_text":"Disaster Recovery Services for Hybrid Cloud</title></head>\n<body>\n\n\n<p>Published: Thu, 27 Oct 2016 07:01:21 GMT</p>\n"
       "passage_score":10.153470191601558,
       "document_id":"fbb5dcb4d8a6a29f572ebdeb6fbed20e",              
       "start_offset":70
       "end_offset":120
       "field":"html"
     },
  ...
```
{: codeblock}                        

### passages.fields
{: #passages_fields}

A comma-separated list of fields in the index that passages will be drawn from. If this parameter not specified then all top level field are included.

### passages.count
{: #passages_count}

The maximum number of passages to return. The search will return fewer passages if that is the total number found. The default is `10`. The maximum is `100`.

### passages.characters
{: #passages_characters}

The approximate number of characters that any one passage should have. The default is `400`. The minimum is `50`. The maximum is `2000`. Passages returned may be up to twice the requested length (if necessary) to get them to begin and end at sentence boundaries.

## table retrieval
{: #table_retrieval}

If [Table understanding](/docs/services/discovery-data?topic=discovery-data-understanding_tables) is enabled in your collection, a `natural_language_query` will find tables whose content or context match a search query.

Example query:

```bash
 curl -H \"Authorization: Bearer {token}\" 'https://{hostmame}/{instance_name}/v2/projects/{project_id}/collections/{collection_id}/query?version=2019-11-29&natural_language_query='interest%20appraised'&table_results=true"
```
{: pre}

The JSON that is returned from the query will be of the following format:

```json
{
  “matching_results”: 1,
  “session_token”: “1_FDjAVkn9SW6oH9y5_9Ek3KsNFG”,
  “results”: [
    {
     ...
    }
  ],
{
  "table_results": [
    {
      "table_id": "e883d3df1d45251121cd3d5aef86e4edc9658b21",
      "source_document_id": "c774c3df0c90255191cc0d4bb8b5e8edc6638d96",
      "collection_id": "collection_id",
      "table_html": "html snippet of the table info",
      "table_html_offset": 42500,
      "table": [
        {
          "location": {
            "begin": 42878,
            "end": 44757
          },
          "text": "Appraisal Premise Interest Appraised Date of Value Value Conclusion\nMarket Value \"As Is\" Fee Simple Estate January 12, 2016 $1,100,000\n",
          "section_title": {
            "location": {
              "begin": 42300,
              "end": 42323
            },
            "text": "MARKET VALUE CONCLUSION"
          },
          "title": {},
          "table_headers": [],
          "row_headers": [
            {
              "cell_id": "rowHeader-42878-42896",
              "location": {
                "begin": 42878,
                "end": 42896
              },
              "text": "Appraisal Premise",
              "text_normalized": "Appraisal Premise",
              "row_index_begin": 0,
              "row_index_end": 0,
              "column_index_begin": 0,
              "column_index_end": 0
            }
          ],
          "column_headers": [],
          "body_cells": [
            {
              "cell_id": "bodyCell-43410-43424",
              "location": {
                "begin": 43410,
                "end": 43424
              },
              "text": "Date of Value",
              "row_index_begin": 0,
              "row_index_end": 0,
              "column_index_begin": 2,
              "column_index_end": 2,
              "row_header_ids": [
                "rowHeader-42878-42896",
                "rowHeader-43145-43164"
              ],
              "row_header_texts": [
                "Appraisal Premise",
                "Interest Appraised"
              ],
              "row_header_texts_normalized": [
                "Appraisal Premise",
                "Interest Appraised"
              ],
              "column_header_ids": [],
              "column_header_texts": [],
              "column_header_texts_normalized": [],
              "attributes": []
            }
          ],
          "contexts": [
            {
              "location": {
                "begin": 44980,
                "end": 44996
              },
              "text": "Compiled by CBRE"
            }
          ],
          "key_value_pairs": []
        }
      ]
    }
  ]
}
```
{: codeblock}

### table_results.enabled
{: #table_results}

When `true`, a `table_results` array will appear in the response with a list of table objects that match the given `natural_language_query` in order of scored relevance. The default is `false`.

### table_results.count
{: #table_count}

This parameter specifies the maximum number of tables that can appear in the `table_results` array. Only returned if `table_results.enabled`=`true`. The default is `10`.

