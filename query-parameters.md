---

copyright:
  years: 2019, 2021
lastupdated: "2021-07-19"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:beta: .beta}
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
{:beta: .beta}

# Query parameters
{: #query-parameters}

You can use these parameters when you write queries with the {{site.data.keyword.discoveryshort}} Query Language. For more information, see the {{site.data.keyword.discoveryshort}} [API reference](https://{DomainName}/apidocs/discovery-data#query){: external}. For an overview of query concepts, see the [Query overview](/docs/discovery-data?topic=discovery-data-query-concepts).
{: shortdesc}

Queries that are written in the {{site.data.keyword.discoveryshort}} Query Language can include both search and structure parameters.

## Search parameters
{: #query-parameters-search}

Use search parameters to search your collection, identify a result set, and analyze the result set.

The **results set** is the group of documents that are identified by the combined searches of the search parameters. The results set might be significantly larger than the returned results. If an empty query is submitted, the results set is equal to all the documents in the collection.

Documents that you do not have permissions to access are not returned in query results.
{: important}

## Answer finding ![IBM Cloud only](images/ibm-cloud.png)
{: #answer-finding}

Answer finding is a beta feature. Do not enable the feature in production environments. This feature is available in managed deployments only.
{: beta}

By default, {{site.data.keyword.discoveryshort}} provides answers by returning the entire [passage](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-query-parameters#passages) that contains the answer to a natural language query. When Answer finding is enabled, {{site.data.keyword.discoveryshort}} also provides a "short answer" within the passage, and a confidence score to show whether the "short answer" answers the question that is explicit or implicit in the user query. Applications that use Answer finding can display this short answer alone or can display the short answer emphasized in the context of the full passage. For most applications, the option that displays the short answer emphasized within the full passage might be preferable, because answers generally make more sense in context.

Notes about Answer finding:

  -  It finds answers. It doesn’t create answers. The answer must be part of the text; it can't be inferred.
     -  “What was IBM’s revenue in 2017?” can get a correct answer if you have a document that states what was IBM’s revenue was in 2017. However, if you have a document that lists what IBM’s revenue was in each quarter of 2017, it doesn't add them up and give you a total.
  -  If the answer is available, it can handle synonyms and lexical variations.
     -  Example question: “When did IBM purchase Red Hat?” – Passage ("short answer" is in **bold**.): “IBM closed its $34 billion acquisition of Red Hat in **July of 2019**."
  -  It can combine information across multiple sentences if they are close together (within approximately 2,000 characters)
     -  Example question: “When did IBM purchase Red Hat?” – Passage: “IBM acquired Red Hat for $34 billion. The deal closed in **July of 2019**."
  -  It handles implicit questions similar to the way it would handle the equivalent explicit question.
     - Example questions: 

        - `company that developed the AS/400`
        - `What company developed the AS/400?`
  - Works well with questions with longer phrase or clause answers.
    - Example question: How do I flip a pancake?
    - Passage: The key to getting a world-class pancake is flipping it properly. The best way to flip a pancake is to **stick a spatula under it, lift it at least 4 inches in the air, and quickly rotate the spatula 180 degrees.**
  - Many how or why questions are only fully answered by much longer spans of text. Answer finding does not return a whole document as the answer (and it doesn't summarize a document length answer).
  - Handles yes or no questions that are factual and have a concise answer in the text.
     - Example question: Is there a library in Timbuktu
     - Passage: Timbuktu's **main library, officially called the Ahmed Baba Institute of Higher Islamic Studies and Research**, is a treasure house that contains more than 20,000 manuscripts that cover centuries of Mali's history. 
  - Handles questions with very short answers, such as names and dates, especially when the type of answer that is required is explicit in the text.
  - Handles opinion questions, but only for finding a statement of that opinion, not for assessing the validity of the opinion.
     - Example question: Should I try blue eyeshadow?
     - Passage: We think **blue eye shadow is trending** this year.

The Answer finding API beta adds two new parameters within the `passage` block of the query API. for more information about these parameters, see the {{site.data.keyword.discoveryshort}} [API reference](https://{DomainName}/apidocs/discovery-data#query){: external}.

-  `find_answers` is optional and defaults to `false`. If it is set to `true` (and the `natural_language_query` parameter is set to a query string), Answer finding is enabled.
-  `max_answers_per_passage` is optional and defaults to `1`. In this case, Answer finding finds the number of answers that are specified at most from any one passage.

A block is also added to the `return` value within each `passage` object. That block is called `answers`, and it is a list of answer objects. The list can be up to `max_answers_per_passage`in length. Each answer object contains the following fields:

-  `answer_text`is the text of the concise answer to the query.
-  `confidence` is a number between `0` and `1` that is an estimate of the probability that the answer is correct. Some answers have low confidence and are unlikely to be correct. Be selective about what you do with answers based on this value. The confidence and order of documents in the search results are adjusted based on this combination if the `per_document` parameter of passage retrieval is set to `true` (which is the default).
-  `start_offset` is the start character offset (the index of the first character) of the answer within the field that the passage came from. It is greater than or equal to the start offset of the passage (since the answer must be within the passage).
-  `end_offset` is the end character offset (the index of the last character, plus one) of the answer within the field that the passage came from. It is less than or equal to the end offset of the passage.

To find answers across your whole collection:
Set `passages/enabled` to `true`
Set `passages/find_answers` to `true`

To find answers within a single known document (for example, a document review application with long, complex documents):
Set `passages/enabled` to `true`
Set `passages/find_answers` to `true`
Set `filter` to select the `document_id` for the document 

The following example shows a query that uses this API:

```bash
POST /v2/projects/{project_id}/query{"natural_language_query": "Why did Nixon resign?",
  "passages": {"enabled": true, "find_answers":true} }
```
{: codeblock}

Example response

```json
{
  "matching_results": 74, "retrieval_details": { "document_retrieval_strategy": "untrained"},
  "results": [
     {"document_id": "63919442-7d5b-4cae-ab7e-56f58b1390fe",
     "result_metadata":{"collection_id": "collection_id1234","document_retrieval_source":"search","confidence": 0.78214},
     "metadata": {"parent_document_id": "63919442-7d5b-4cae-ab7e-56f58b1390fg"},
     "title": "Watergate scandal",
     "document_passages": [
      {"passage_text": "With his complicity in the cover-up made public and his political support completely eroded, Nixon resigned from office on August 9, 1974. It is believed that, had he not done so, he would have been impeached by the House and removed from office by a trial in the Senate.",
         "field": "text",
         "start_offset": 281,
         "end_offset": 553,
         "answers": [
            {"answer_text": "his complicity in the cover-up made public and his political support completely eroded",
            "start_offset": 286, "end_offset": 373, "confidence": 0.78214}
            ]
  ... 
}     
```
{: codeblock}

Because Answer finding is enabled on only the documents and passages that are requested, consider requesting more documents and more passages per document than are needed. By doing so, the Answer finding model can be combined with more candidate documents and passages. For example, if you want to show `10` documents and `1` passage from each document, consider asking for `20` documents and up to `3` passages from each document with Answer finding. Answer finding searches for answers in up to `20*3` = `60` passages. If it's confident that an answer was found in one of the passages, the confidence score is combined with the document and passage scores to produce a final ranking, which can promote a document or passage that might otherwise be missed.

## `natural_language_query`
{: #nlq}

Use a natural language query to enter queries that are expressed in natural language, as might be received from a user in a conversational or free-text interface, such as IBM Watson Assistant. The parameter uses the entire input as the query text. It does **not** recognize operators. The `natural_language_query` parameter enables capabilities such as relevancy training. Query results include a `confidence` score. See [confidence scores](/docs/discovery-data?topic=discovery-data-train#confidence). The maximum query string length for a natural language query is `2048`.

## `query`
{: #query}

A query search returns all documents in your data set with full enrichments and full text in order of relevance. A query also excludes any documents that don't mention the query content.

## `aggregation`
{: #aggregation}

Aggregation queries return a count of documents that match a set of data values. For the full list of aggregation options, see the [Aggregations table](/docs/discovery-data?topic=discovery-data-query-aggregations). 


## `filter`
{: #filter}

A cacheable query that excludes any documents that don't mention the query content. Filter search results are **not** returned in order of relevance. 

### Differences between the filter and query parameters
{: #filtervquery}

If you test the same search term on a small data set, you might find that the `filter` and `query` parameters return very similar (if not identical) results. However, the two parameters differ.

- Using a filter parameter alone returns search results in no specific order.
- Using a query parameter alone returns search results in order of relevance.

In large data sets, if you need results to be returned in order of relevance, combine the `filter` and `query` parameters. Using the parameters together improves performance. The `filter` parameter is applied first. It filters the documents, and then caches the results. Then, the `query` parameter ranks the cached results. For an example of using filters and queries together, see [Building combined queries](/docs/discovery-data?topic=discovery-data-query-concepts#building-combined-queries). You can use filters in aggregations also.

When you write a query that includes both a `filter`, and an `aggregation`, `query`, or `natural_language_query` parameter, the `filter` parameter runs first, and then any `aggregation`, `query`, or `natural_language_query` parameters run in parallel.

With a simple query, especially on a small data set, the `filter` and `query` parameters often return the exact same (or similar) results. If the `filter` and `query` calls return similar results, and you don't need the responses to be returned in order of relevance, use the `filter` parameter. Filter calls are faster and are cached. Caching means that the next time you make the same call, you get a much quicker response, particularly in a big data set.


## Structure parameters
{: #query-parameters-structure}

Structure parameters define the content and organization of the documents in the returned JSON. They determine the following things:

- the number of results to return
- where in the results set to start returning documents
- how the result set is sorted
- which fields to return for each document
- whether to remove duplicate documents
- whether to remove extracted relevant passages from the results set. 

Structure parameters don't affect which documents are part of the entire results set.

## `return`
{: #return}

A comma-separated list of the portion of the document hierarchy to return. Any of the document hierarchies are valid values. If this parameter is an empty list, then all fields are returned.

## `count`
{: #count}

The number of documents that you want to return in the response. The default is `10`. The maximum for the `count` and `offset` values together in any one query is `10000`.

## `offset`
{: #offset}

Index value of the position of the search result where the set of results to return begins. For example, if the total number of results that are returned is 10, and the offset is 8, it returns the last two results. The default is `0`. The maximum allowed value for the `count` and `offset` together in any one query is `10000`.

## `spell correction`
{: #spell}

In natural language queries, you can check and correct the spelling of terms in the `natural_language_query` parameter. The most likely correction is returned in the `suggested_query` field of the response (if one exists).

## `sort`
{: #sort}

A comma-separated list of fields in the document to sort by. You can optionally specify a sort direction by prefixing the field with `-` for descending order or `+` for ascending order. Ascending order is the default sort direction.

## `highlight`
{: #highlight}

A Boolean that specifies whether to include a `highlight` object in the returned output. When included, the highlight returns keys that are field names and values that are arrays. The arrays contain segments of query-matching text that is highlighted by using the HTML emphasis (`<em>`) tag.

The output lists the `highlight` object after the `enriched_text` object, as shown in the following example.

```bash
curl -H "Authorization: Bearer {token}" 'https://{hostname}/{instance_name}/v2/projects/{project_id}/collections/{collection_id}/query?version=2019-11-29&natural_language_query=Hybrid%20cloud%20companies&highlight=true'
```
{: pre}

The JSON that is returned has the following format:

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

## `suggested_refinements` ![Premium plan](images/premium.png)
{: #suggested_refinements}

The `suggested_refinements` parameter enables dynamic facets for a natural language query. Dynamic facets use unsupervised machine learning models to automatically select terms that are semantically similar to the terms in the query and terms in the resulting documents. For example, you can select dynamic facets to enhance an existing query by filtering on a unique term to improve your results. Dynamic facets are trained as documents are added to a collection. It might take several minutes until dynamic facets appear, after you add documents to a collection. To enable dynamic facets, you must first enable the **Parts of Speech** enrichment in your collection. For more information, see [Applying prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu#pos).

Only users of Premium plan managed deployments and installed Cloud Pak for Data 2.x deployments can use this parameter.
{: note}

The JSON that is returned is of the following format:

```json
{
  "matching_results": 40,
  "retrieval_details": {
  "document_retrieval_strategy": "untrained"
  },
  "suggested_refinements": [
     {
       "text": "spss"
     },
     {
       "text": "environment"
     },
     {
       "text": "DataEnterprise Edition"
     },
     {
       "text": "InstallPackage"
     },
     {
       "text": "modules"
     },
     {
       "text": "refinery"
     },
     {
       "text": "store"
     },
     {
       "text": "iira"
     },
     {
       "text": "registration"
     },
     {
       "text": "put"
     }
  ],
```
{: codeblock}

### `suggested_refinements.count`
{: #suggested_refinements_count}

The maximum number of suggested refinements to return. The default is `10`. The minimum is `1`. The maximum is `100`.

## `passages`
{: #passages}

A Boolean that specifies whether the service returns a set of the most relevant passages from the documents that are returned by a query that uses the `natural_language_query` parameter. The passages are generated by sophisticated Watson algorithms that determine the best passages of text from all of the documents returned by the query. The default is `false`.

{{site.data.keyword.discoveryshort}} attempts to return passages that start at the beginning of a sentence and stop at the end by using sentence boundary detection. To do so, it first searches for passages approximately the length specified in the [`passages.characters` parameter](/docs/discovery-data?topic=discovery-data-query-parameters#passages_characters) (default `400`). It then expands each passage to the limit of twice the specified length so as to return full sentences. If your `passages.characters` parameter is short or the sentences in your documents are long there might be no sentence boundaries close enough to return the full sentence without going over twice the requested length. In that case, {{site.data.keyword.discoveryshort}} stays within the limit of twice the `passages.characters` parameter, so the passages that are returned might not include the entire sentence and can omit the beginning, end, or both.

Since sentence boundary adjustments expand passage size, the average passage length can increase. If your application has limited screen space, you might want to set a smaller value for `passages.characters` or truncate the passages that are returned by {{site.data.keyword.discoveryshort}}. Sentence boundary detection works for all supported languages and uses language-specific logic.

Passages are returned `per_document` by default. Passages are grouped with each document result and are ordered by passage relevance. Including passage retrieval in queries increases the response time because it takes to score the passages. Search results are displayed in a preview of your document for the following document types: PDF, Word, PowerPoint, Excel, and all image files. See [supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes) for the list of supported image files.

You can adjust the fields in the documents for passage retrieval to search with the [`passages.fields`](/docs/discovery-data?topic=discovery-data-query-parameters#passages_fields) parameter.

The `passages` parameter returns matching passages (`passage_text`), and the `score`, `document_id`, the name of the field that the passage was extracted from (`field`), and the starting and ending characters of the passage text within the field (`start_offset` and `end_offset`), as shown in the following example.

```bash
 curl -H "Authorization: Bearer {token}" 'https://{hostname}/{instance_name}/v2/projects/{project_id}/collections/{collection_id}/query?version=2019-11-29&natural_language_query=Hybrid%20cloud%20companies&passages=true&passages.per_document=false'
```
{: pre}

The JSON that is returned from the query has the following format:

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

### `passages.fields`
{: #passages_fields}

A comma-separated list of fields in the index that passages are drawn from. If this parameter is not specified, then passages from all root-level fields are included.

You can specify fields in both the `return` and `passages.fields` parameters. When you specify both parameters, each with different values, they are treated separately. 

For example, the request might include the parameters `"return": ["docno"]` and `"passages":{"fields": ["body"]`. The `body` field is specified in `passages.fields`, but not in `return`. In the result, passages from the document body are returned, but the contents of the body field itself is not returned.

### `passages.count`
{: #passages_count}

The maximum number of passages to return. The search returns fewer passages if the specified count is the total number found. The default is `10`. The maximum is `100`.

### `passages.characters`
{: #passages_characters}

The approximate number of characters that any one passage can have. The default is `400`. The minimum is `50`. The maximum is `2,000`. Passages that are returned can contain up to twice the requested length (if necessary) to get them to begin and end at sentence boundaries.

## `table retrieval`
{: #table_retrieval}

If [Table understanding](/docs/discovery-data?topic=discovery-data-understanding_tables) is enabled in your collection, a `natural_language_query` finds tables with content or context that match a search query.

Example query:

```bash
 curl -H "Authorization: Bearer {token}" 'https://{hostname}/{instance_name}/v2/projects/{project_id}/collections/{collection_id}/query?version=2019-11-29&natural_language_query=interest%20appraised&table_results=true'
```
{: pre}

The JSON that is returned from the query has the following format:

```json
{
  “matching_results”: 1,
  “session_token”: “1_FDjAVkn9SW6oH9y5_9Ek3KsNFG”,
  “results”: [
    {
     ...
    }
  ]
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

### `table_results.enabled`
{: #table_results}

When `true`, a `table_results` array is included in the response with a list of table objects that match the `natural_language_query` value in order of scored relevance. The default is `false`.

### `table_results.count`
{: #table_count}

This parameter specifies the maximum number of tables that can be included in the `table_results` array. Only returned if `table_results.enabled`=`true`. The default is `10`.

