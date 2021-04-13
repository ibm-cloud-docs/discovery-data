---

copyright:
  years: 2019, 2021
lastupdated: "2021-04-13"

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

# Query overview
{: #query-concepts}

{{site.data.keyword.discoveryfull}} offers powerful content search capabilities through queries. After your content is uploaded and customized by {{site.data.keyword.discoveryshort}}, you can build queries, integrate {{site.data.keyword.discoveryshort}} into your own projects, or create a custom applications. For more information, see [Building and deploying components](/docs/discovery-data?topic=discovery-data-deploy).
{: shortdesc}

In the {{site.data.keyword.discoveryshort}} tooling, you can write and test [natural language queries](/docs/discovery-data?topic=discovery-data-query-parameters#nlq) on the *Improve and customize* page.
{: tip}

When querying using the API, the entire {{site.data.keyword.discoveryshort}} Query Language is supported. For more information, see the {{site.data.keyword.discoveryshort}} [API](https://{DomainName}/apidocs/discovery-data#query){: external}.
{: important}

For more information about the {{site.data.keyword.discoveryshort}} Query Language, see:

-  [Query operators](/docs/discovery-data?topic=discovery-data-query-operators)
-  [Query aggregations](/docs/discovery-data?topic=discovery-data-query-aggregations)
-  [Query reference](/docs/discovery-data?topic=discovery-data-query-reference)

Also see:

-  **Use the {{site.data.keyword.discoveryshort}} Query Language** - see [query](/docs/discovery-data?topic=discovery-data-query-parameters#query).
-  **Write an aggregation query using the {{site.data.keyword.discoveryshort}} Query Language** - see [aggregation](/docs/discovery-data?topic=discovery-data-query-parameters#aggregation).
-  **Write a filter to narrow down the documentation set using the {{site.data.keyword.discoveryshort}} Query Language** - see [filter](/docs/discovery-data?topic=discovery-data-query-parameters#filter).
-  **Fields to return** - see [return](/docs/discovery-data?topic=discovery-data-query-parameters#return).
-  **Number of documents to return** - see [count](/docs/discovery-data?topic=discovery-data-query-parameters#count).
-  **Number of query results to skip at the beginning** - see [offset](/docs/discovery-data?topic=discovery-data-query-parameters#offset).

When you create a query or filter, {{site.data.keyword.discoveryshort}} looks at each result and tries to match the paths you have defined. When matches occur, they are added to the results set. When creating a query, you can be as vague or as specific as you want. The more specific the query, the more targeted the results.

Documents you do not have permissions for will not be returned in query results.
{: important}

The queries you write will vary by collection/project, because all collections/projects contain unique content.
{: tip}

## How to structure a basic query
{: #structure-basic-query}

JSON is hierarchical, so {{site.data.keyword.discoveryshort}} Query Language queries need to be written using that same hierarchy. So if your JSON looks like this:

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

  Operators that evaluate a field (`<=` , `>=`, `<`, `>`) require a `number` or `date` as the value. Using quotations around a value always makes it a `string`. Therefore `score>=0.5` is a valid query and `score>="0.5"` is not. See [Query operators](/docs/discovery-data?topic=discovery-data-query-operators) for a complete list of operators.
  {: tip}

## Building combined queries
{: #building-combined-queries}

You can combine query parameters together to build more targeted queries. For example, you can use the both the `filter` and `query` parameters together. For more information about filtering vs. querying, see [Differences between the filter and query parameters](/docs/discovery-data?topic=discovery-data-query-parameters#filtervquery).

## How to structure an aggregation
{: #structure-aggregation}

Aggregations return a set of data values. For the full list of aggregation options, see [Aggregations](/docs/discovery-data?topic=discovery-data-query-reference#aggregations).

![Example aggregation query structure](images/aggregation_structure.png)

This example aggregation will find all of the `concepts` in your collection.
The delimiter in this query is `.` and the operator is `()`, see [Query operators](/docs/discovery-data?topic=discovery-data-query-operators) to learn about other operators available in the {{site.data.keyword.discoveryshort}} Query Language.

### Example aggregation queries
{: #example-aggregations}

There are several types of ways you can aggregate results with {{site.data.keyword.discoveryshort}}, including top values, sum, min, max, average, timeslice, and histogram. You can also add filters and nest aggregations.

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

If you have enabled document level security on a collection, you can control search results at query time at the user level. See [Configuring document level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls) for information about leveraging the security settings of your source documents.

To return search results that restrict query results to the security settings of authorized users, those users: 
-  Must be associated with your {{site.data.keyword.discoveryshort}} instance. See [Creating users for document level security](/docs/discovery-data?topic=discovery-data-collection-types#createusersdls) for instructions.
-  Must be present in the source system (Box, SharePoint OnPrem, or SharePoint Online).
If both criteria are not met, no results will be returned.

The username associated with your {{site.data.keyword.discoveryshort}} instance is used to generate an authorization token. That token is used in your {{site.data.keyword.discoveryshort}} queries.

To generate each access token, run the following command:
 
```bash
curl -u "{username}:{password}" "https://{hostname}:{port}/v1/preauth/validateAuth"
```
{: pre}
   
Replace `{username}` and `{password}` with the user's {{site.data.keyword.discoveryshort}} credentials, and replace `{hostname}` and `{port}` with the details for your instance.

To use the token in a {{site.data.keyword.discoveryshort}} query, run the following command for each user added:

```bash
curl -H "Authorization: Bearer {token}" 'https://{hostname}/{instance_name}/v2/projects/{project_id}/collections/{Collection_ID}/query\?version\=2019-11-29'
```
{: pre}

Replace `{hostname}` and other fields with the details for your instance.

For information on writing queries using the {{site.data.keyword.discoveryshort}} API, see the [API Reference](https://{DomainName}/apidocs/discovery-data#query){: external}.
{: tip}    

Each user's query results will be restricted to their document permissions.


