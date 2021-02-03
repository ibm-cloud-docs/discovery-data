---

copyright:
  years: 2019, 2021
lastupdated: "2021-02-03"

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

These parameters are used when writing queries with the {{site.data.keyword.discoveryshort}} Query Language. For more information, see the {{site.data.keyword.discoveryshort}} [API reference](https://{DomainName}/apidocs/discovery-data#query){: external}. For an overview of query concepts, see the [Query overview](/docs/discovery-data?topic=discovery-data-query-concepts).
{: shortdesc}

Queries written in the {{site.data.keyword.discoveryshort}} Query Language can include both search and structure parameters.

**Search parameters**

Search parameters enable you to search your collection, identify a result set, and perform analysis on the result set.

The **results set** is the group of documents identified by the combined searches of the search parameters. The results set may be significantly larger than the returned results. If an empty query is performed, the results set is equal to all the documents in the collection.

Documents you do not have permissions for will not be returned in query results.
{: important}

## Answer finding ![IBM Cloud only](images/cloudonly.png)
{: #answer-finding}

The Answer finding feature is beta functionality and should not be used in production environments.
{: beta}

By default, {{site.data.keyword.discoveryshort}} provides answers by returning the entire [passage](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-query-parameters#passages) that contains the answer to a natural language query. When Answer finding is enabled, {{site.data.keyword.discoveryshort}} also provides a "short answer" within the passage, as well as a confidence score that the "short answer" answers the question that is explicit or implicit in the user query. Applications that use Answer finding can display this short answer alone or can display the short answer emphasized in the context of the full passage. For most applications, the option that displays the short answer emphasized within the full passage might be preferable, because answers generally make more sense in context.

Notes about Answer finding:
  -  It finds answers, it doesn’t create answers. The answer must be part of the text; it can't be inferred.
     -  “What was IBM’s revenue in 2017?” can get a correct answer if you have a document that states what was IBM’s revenue was in 2017. However, if you have a document that lists what IBM’s revenue was in each quarter of 2017, it will not add them up and give you a total
  -  If the answer is available, it can handle synonyms and lexical variations.
     -  Example question: “When did IBM purchase Red Hat?” – Passage ("short answer" is in **bold**.): “IBM closed its $34 billion acquisition of Red Hat in **July of 2019**."
  -  It can combine information across multiple sentences as long as they are close together (within approximately 2,000 characters)
     -  Example question: “When did IBM purchase Red Hat?” – Passage: “IBM acquired Red Hat for $34 billion. The deal closed in **July of 2019**."
  -  It handles implicit questions similar to the way it would handle the equivalent explicit question.
     - Example questions: “company that developed the AS/400”, ”What company developed the AS/400?”
  - Works well with questions with longer phrase/clause answers.
     -  Example question: “How do I flip a pancake?” - Passage: “The key to getting a world-class pancake is flipping it properly. The best way to flip a pancake is to **stick a spatula under it, lift it at least 4 inches in the air, and quickly rotate the spatula 180 degrees.**”
  - Many how or why questions are only fully answered by much longer spans of text. Answer finding will not tell you that a whole document is the answer (and it will not summarize a document length answer).
  - Handles yes/no questions that are factual and have a concise answer in the text.
     -  Example question: ”Is there a library in Timbuktu” - Passage: Timbuktu's **main library, officially called the Ahmed Baba Institute of Higher Islamic Studies and Research**, is a treasure house containing more than 20,000 manuscripts covering centuries of Mali's history. 
  - Handles questions with very short answers, such as names and dates, especially when the type of answer required is explicit in the text.
  - Handles opinion questions, but only for finding a statement of that opinion, not for assessing the validity of the opinion.
     - Example question: ”Should I try blue eyeshadow?” - Passage: “We think **blue eye shadow is trending** this year.”

The Answer finding API beta adds two new parameters within the `passage` block of the query API. for more informatation on these parameters, see the {{site.data.keyword.discoveryshort}} [API reference](https://{DomainName}/apidocs/discovery-data#query){: external}.

-  `find_answers` is optional and defaults to `false`. If it is set to `true` (and the `natural_language_query` parameter is set to a query string), Answer finding will be enabled.
-  `max_answers_per_passage` is optional and defaults to `1`. In this case, Answer finding will find the number of answers specified at most from any one passage.

A block is also added to the `return` value within each `passage` object.  That block is called `answers`, and it is a list of answer objects. The list can be up to `max_answers_per_passage`in length. Each answer object contains the following fields:

-  `answer_text`is the text of the concise answer to the query.
-  `confidence` is a number between `0` and `1` that is an estimate of the probability that the answer is correct. Note that some answers have very low confidence and are very unlikely to be correct, so you should be selective about what you do with answers based on this value. The confidence and order of documents in the search results are adjusted based on this combination if the `per_document` parameter of passage retrieval is set to `true` (which is the default).
-  `start_offset` is the start character offset (the index of the first character) of the answer within the field that the passage came from.  It is guaranteed to be greater than or equal to the start offset of the passage (since the answer must be within the passage).
-  `end_offset` is the end character offset (the index of the last character, plus one) of the answer within the field that the passage came from.  It is guaranteed to be less than or equal to the end offset of the passage.

To find answers across your whole collection:
Set `passages/enabled` to `true`
Set `passages/find_answers` to `true`

To find answers within a single known document (for example, a document review application with long, complex documents):
Set `passages/enabled` to `true`
Set `passages/find_answers` to `true`
Set `filter` to select the `document_id` for the document 

Here is an example of a query using this API:

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

Because Answer finding is enabled on only the documents and passages requested, you may want to consider requesting more documents and/or more passages per document than actually needed so the Answer finding model can be combined with more candidate documents and passages. For example, if you want to show `10` documents and `1` passage from each document, consider asking for `20` documents and up to `3` passages from each document with Answer finding. Answer finding will then search for answers in up to `20*3` = `60` passages and if confident that an answer was found in one of those passages, that confidence will be combined with the document and passage scores to produce a final ranking which can promote a document or passage that might otherwise have been missed.

## natural_language_query
{: #nlq}

A natural language query enables you to perform queries expressed in natural language, as might be received from an end user in a conversational or free-text interface - for example: "IBM Watson in healthcare". The parameter uses the entire input as the query text. It does **not** recognize operators. The `natural_language_query` parameter enables capabilities such as relevancy training. Query results will include a `confidence` score. See [confidence scores](/docs/discovery-data?topic=discovery-data-train#confidence). The maximum query string length for a natural language query is `2048`.

## query
{: #query}

A query search returns all documents in your data set with full enrichments and full text in order of relevance. A query also excludes any documents that don't mention the query content.

## aggregation
{: #aggregation}

Aggregation queries return a count of documents matching a set of data values. For the full list of aggregation options, see the [Aggregations table](/docs/discovery-data?topic=discovery-data-query-aggregations). 


## filter
{: #filter}

A cacheable query that excludes any documents that don't mention the query content. Filter search results are **not** returned in order of relevance. 

### Differences between the filter and query parameters
{: #filtervquery}

If you test the same search term on a small data set, you might find that the `filter` and `query` parameters return very similar (if not identical) results. However, there is a difference between the two parameters.

- Using a filter parameter alone will return search results in no specific order.
- Using a query parameter alone will return search results in order of relevance.

In large data sets, if you need results returned in order of relevance, you should combine the `filter` and `query` parameters, because using them together will improve performance. This is because the `filter` parameter will run first and cache results, then the `query` parameter will rank them. For an example of using filters and queries together, see [Building combined queries](/docs/discovery-data?topic=discovery-data-query-concepts#building-combined-queries). Filters can also be used in aggregations.

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
curl -H "Authorization: Bearer {token}" 'https://{hostname}/{instance_name}/v2/projects/{project_id}/collections/{collection_id}/query?version=2019-11-29&natural_language_query=Hybrid%20cloud%20companies&highlight=true'
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

## suggested_refinements
{: #suggested_refinements}

The `suggested_refinements` parameter enables dynamic facets for a natural language query. Dynamic facets use unsupervised machine learning models to automatically select terms that are semantically similar to the terms in the query and terms in the resulting documents. For example, you can select dynamic facets to enhance an existing query by filtering on a unique term to improve your results. Dynamic facets are trained as documents are added to a collection. It might take several minutes until dynamic facets appear, after you add documents to a collection. To enable dynamic facets, you must first enable the **Parts of Speech** enrichment in your collection. For more information about the **Parts of Speech** enrichment, see [Parts of speech](/docs/discovery-data?topic=discovery-data-create-enrichments#pos).

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

### suggested_refinements.count
{: #suggested_refinements_count}

The maximum number of suggested refinements returned. The default is `10`. The minimum is `1`. The maximum is `100`.

## passages
{: #passages}

A boolean that specifies whether the service returns a set of the most relevant passages from the documents returned by a query that uses the `natural_language_query` parameter. The passages are generated by sophisticated Watson algorithms to determine the best passages of text from all of the documents returned by the query. The default is `false`.

{{site.data.keyword.discoveryshort}} attempts to return passages that start at the beginning of a sentence and stop at the end using sentence boundary detection. To do so, it first searches for passages approximately the length specified in the [`passages.characters` parameter](/docs/discovery-data?topic=discovery-data-query-parameters#passages_characters) (default `400`). It then expands each passage to the limit of twice the specified length in order to return full sentences. If your `passages.characters` parameter is short and/or the sentences in your documents are very long there may be no sentence boundaries close enough to return the full sentence without going over twice the requested length. In that case, {{site.data.keyword.discoveryshort}} stays within the limit of twice the `passages.characters` parameter, so the passage returned will not include the entire sentence and omit the beginning, end, or both.

Since sentence boundary adjustments expand passage size, you will see a substantial increase in average passage length. If your application has limited screen space, you may want to set a smaller value for `passages.characters` and/or truncate the passages that are returned by {{site.data.keyword.discoveryshort}}. Sentence boundary detection works for all supported languages and uses language-specific logic.

Passages are returned `per_document` by default. This means they will appear as a section within each document result ordered by passage relevance. Including passage retrieval in queries can increase response times as it includes additional scoring of the passages. Search results display in a preview of your document for the following source documents: PDF, Word, PowerPoint, Excel, and all image files. See [supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes) for the list of image files. 

You can adjust the fields in the documents over which passage retrieval searches with the [`passages.fields`](/docs/discovery-data?topic=discovery-data-query-parameters#passages_fields) parameter.

The `passages` parameter returns matching passages (`passage_text`), as well as the `score`, `document_id`, the name of the field the passage was extracted from (`field`), and the starting and ending characters of the passage text within the field (`start_offset` and `end_offset`), as shown in the following example.

```bash
 curl -H "Authorization: Bearer {token}" 'https://{hostname}/{instance_name}/v2/projects/{project_id}/collections/{collection_id}/query?version=2019-11-29&natural_language_query=Hybrid%20cloud%20companies&passages=true&passages.per_document=false'
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

If [Table understanding](/docs/discovery-data?topic=discovery-data-understanding_tables) is enabled in your collection, a `natural_language_query` will find tables whose content or context match a search query.

Example query:

```bash
 curl -H "Authorization: Bearer {token}" 'https://{hostname}/{instance_name}/v2/projects/{project_id}/collections/{collection_id}/query?version=2019-11-29&natural_language_query=interest%20appraised&table_results=true'
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

