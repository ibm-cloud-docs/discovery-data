---

copyright:
  years: 2019
lastupdated: "2019-07-12"

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

# Query overview
{: #query-concepts}

<!-- Help for the Query screen in WD ICP4D -->

{{site.data.keyword.discovery-data_long}} offers powerful content search capabilities through queries. After your content is uploaded and enriched by {{site.data.keyword.discovery-data_short}}, you can build queries, integrate {{site.data.keyword.discovery-data_short}} into your own projects, or create a custom applications. 
{: shortdesc}

To access the **Query** screen, [create a new collection (or open an existing one)](/docs/services/discovery-data?topic=discovery-data-collections#collections), and click the **Query** tab.

For information on writing queries using the {{site.data.keyword.discovery-data_short}} API, see the [API Reference](https://{DomainName}/apidocs/discovery-data#query-a-collection-get).

You can write natural language queries, or structured queries using the {{site.data.keyword.discoveryshort}} Query Language. 

-  **Use natural language** - see [natural_language_query](/docs/services/discovery-data?topic=discovery-data-query-parameters#nlq). 
-  **Use the {{site.data.keyword.discoveryshort}} Query Language** - see [query](/docs/services/discovery-data?topic=discovery-data-query-parameters#query).
-  **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** - see [aggregation](/docs/services/discovery-data?topic=discovery-data-query-parameters#aggregation).
-  **Write a filter to narow down the documentation set using the {{site.data.keyword.discoveryshort}} Query Language** - see [filter](/docs/services/discovery-data?topic=discovery-data-query-parameters#filter).
-  **Fields to return** - see [return](/docs/services/discovery-data?topic=discovery-data-query-parameters#return).
-  **Number of documents to return** - see [count](/docs/services/discovery-data?topic=discovery-data-query-parameters#count).
-  **Number of query results to skip at the beginning** - see [offset](/docs/services/discovery-data?topic=discovery-data-query-parameters#offset).

Also see

-  [Query operators](/docs/services/discovery-data?topic=discovery-data-query-operators#query-operators)
-  [Query aggregations](/docs/services/discovery-data?topic=discovery-data-query-aggregations#query-aggregations)
-  [Query reference](/docs/services/discovery-data?topic=discovery-data-query-reference#query-reference)
-  [Getting started with {{site.data.keyword.discovery-data_short}}](/docs/services/discovery-data?topic=discovery-data-getting-started#getting-started)

The queries you write will vary by collection, because all collections contain unique content.
{: tip}

When you create a query or filter, ({site.data.keyword.discovery-data_short}} looks at each result and tries to match the paths you have defined. When matches occur, they are added to the results set. When creating a query, you can be as vague or as specific as you want. The more specific the query, the more targeted the results.

## The Discovery data schema
{: #discovery-schema}

To understand how to build a query using the {{site.data.keyword.discoveryshort}} Query Language, you need to be familiar with the JSON produced by {{site.data.keyword.discovery-data_short}} after it enriches the documents in your collection. Once you are familiar with the data schema of your documents, it will be easier to write queries in the {{site.data.keyword.discoveryshort}} Query Language. 

The best way to do this is to run an "empty" query to view the JSON. Open an existing collection. On the **Query** screen, click the **Run query** button. The results display on the right.

-  Each document will be preceded by an `id` number.
-  Scroll down to the `enriched_text` field. Examine each enrichment to learn about the JSON fields you can query on.
    
### How to structure a basic query
{: #structure-basic-query}

As you have noticed, the JSON is hierarchical, so {{site.data.keyword.discoveryshort}} Query Language queries need to be written using that same hierarchy. So if your JSON looks like this:

```json
"enriched_text": {
  "concepts": [
    {
      "text": "Cloud computing",
      "relevance": 0.610029
    }
  ]
}
```
{: codeblock}

Your query would be structured like this:

![Example query structure](images/query_structure2.png)

  Operators that evaluate a field (`<=` , `>=`, `<`, `>`) require a `number` or `date` as the value. Using quotations around a value always makes it a `string`. Therefore `score>=0.5` is a valid query and `score>="0.5"` is not. See [Query operators](/docs/services/discovery-data?topic=discovery-data-query-operators#query-operators) for a complete list of operators.
  {: tip}

## Building combined queries
{: #building-combined-queries}

You can combine query parameters together to build more targeted queries. For example, you can use the both the `filter` and `query` parameters together. For more information about filtering vs. querying, see [Differences between the filter and query parameters](/docs/services/discovery-data?topic=discovery-data-query-parameters#filtervquery).

## How to structure an aggregation
{: #structure-aggregation}

Aggregations return a set of data values. For the full list of aggregation options, see [Aggregations](/docs/services/discovery-data?topic=discovery-data-query-reference#aggregations).

![Example aggregation query structure](images/aggregation_structure.png)

This example aggregation will find all of the `concepts` in your collection.
The delimiter in this query is `.` and the operator is `()`, see [Query operators](/docs/services/discovery-data?topic=discovery-data-query-operators#query-operators) to learn about other operators available in the {{site.data.keyword.discoveryshort}} Query Language.

### Example aggregation queries
{: #example-aggregations}

There are several types of ways you can aggregate results with {{site.data.keyword.discovery-data_short}}, including top values, sum, min, max, average, timeslice, and histogram. You can also add filters and nest aggregations.

#### Filter aggregations
{: #filter-aggregations}

This example aggregation returns the number of articles found in collection of articles about Pittsburgh and how many of those results have a `positive`, `negative`, or `neutral` sentiment.

- `filter(enriched_text.entities.text:"Pittsburgh").term(enriched_text.sentiment.document.label,count:3)`


#### Nested aggregations
{: #nested-aggregations}

Adding `nested` before an aggregation restricts the aggregation to the area of the results specified. For example: `nested(enriched_text.entities)` means that only the `enriched_text.entities` components of any result are used to aggregate against.

This can be seen easily by looking at the differences between the following two queries:
-  `filter(enriched_text.entities.disambiguation.subtype::City)` - the aggregation counts the number of *Results* that contain one or more `entity` with the type `City`
-  `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` - the aggregation counts the number of instances of an `entity` with the type `City` in the results.  

Additionally, any subsequent operation will further restrict the result set that can be aggregated against. For example:

-  `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` means that only entities of `subtype::City` will be aggregated.
-  `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` will aggregate the top 3 entities of subtype `City`
-  `filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` will return the top 3 entities where the result contains at least one entity of subtype `City`.

## Querying with document level security enabled
{: #querydls}

If you have enabled document level security on a collection, you can control search results at query time at the user level. See [Configuring document level security](/docs/services/discovery-data?topic=discovery-data-configuredls#configuredls) for information about leveraging the security settings of your source documents.

To return search results that restrict query results to the security settings of authorized users, those users: 
-  Must be associated with your {{site.data.keyword.discovery-data_short}} instance. See [Creating users for document level security](/docs/services/discovery-data?topic=discovery-data-createusersdls#createusersdls) for instructions.
-  Must be present in the source system (Box, SharePoint OnPrem, or SharePoint Online).
If both criteria are not met, no results will be returned.

The username associated with your {{site.data.keyword.discovery-data_short}} instance is used to generate an authorization token. That token is used in your {{site.data.keyword.discovery-data_short}} queries.

To generate each access token, run the following command:
 
```bash
curl -u "<username>:<password>" "https://<icp4d_cluster_host><:port>/v1/preauth/validateAuth"
```
   
Replace `<username>` and `<password>` with the user's {{site.data.keyword.discovery-data_short}} credentials, and replace `<icp4d_cluster_host>` and `<port>` with the details for your instance.

To use the token in a {{site.data.keyword.discovery-data_short}} query, run the following command for each user added:

```bash
curl -k -H "Authorization: Bearer <User Access Token>" https://<Cluster_IP>:31843/discovery/wd/instances/<Instance_ID>/api/v1/environments/default/collections/<Collection_ID>/query\?version\=2019-06-07
```

Replace `<User Access Token>`, `<Cluster_IP>`, `<Instance_ID>`, and `<Collection_ID>` with the details for your instance.

For information on writing queries using the {{site.data.keyword.discovery-data_short}} API, see the [API Reference](https://{DomainName}/apidocs/discovery-data#query-a-collection-get){: external}.
{: tip}    

Each user's query results will be restricted to their document permissions.


