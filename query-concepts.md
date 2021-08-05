---

copyright:
  years: 2019, 2021
lastupdated: "2021-08-05"

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

{{site.data.keyword.discoveryfull}} offers powerful content search capabilities through queries. After your content is uploaded and customized by {{site.data.keyword.discoveryshort}}, you can build queries, integrate {{site.data.keyword.discoveryshort}} into your own projects, or create a custom application. For more information, see [Building and deploying components](/docs/discovery-data?topic=discovery-data-deploy).
{: shortdesc}

In {{site.data.keyword.discoveryshort}}, you can write and test [natural language queries](/docs/discovery-data?topic=discovery-data-query-parameters#nlq) on the *Improve and customize* page.
{: tip}

When querying using the API, the entire {{site.data.keyword.discoveryshort}} Query Language is supported. For more information, see the {{site.data.keyword.discoveryshort}} [API](https://{DomainName}/apidocs/discovery-data#query){: external}.
{: important}

For more information about the {{site.data.keyword.discoveryshort}} Query Language, see:

-  [Query operators](/docs/discovery-data?topic=discovery-data-query-operators)
-  [Query aggregations](/docs/discovery-data?topic=discovery-data-query-aggregations)
-  [Query reference](/docs/discovery-data?topic=discovery-data-query-reference)

Also, see:

-  **Use the {{site.data.keyword.discoveryshort}} Query Language** - see [query](/docs/discovery-data?topic=discovery-data-query-parameters#query).
-  **Write an aggregation query by using the {{site.data.keyword.discoveryshort}} Query Language** - see [aggregation](/docs/discovery-data?topic=discovery-data-query-parameters#aggregation).
-  **Write a filter to narrow down the documentation set by using the {{site.data.keyword.discoveryshort}} Query Language** - see [filter](/docs/discovery-data?topic=discovery-data-query-parameters#filter).
-  **Fields to return** - see [return](/docs/discovery-data?topic=discovery-data-query-parameters#return).
-  **Number of documents to return** - see [count](/docs/discovery-data?topic=discovery-data-query-parameters#count).
-  **Number of query results to skip at the beginning** - see [offset](/docs/discovery-data?topic=discovery-data-query-parameters#offset).

When you create a query or filter, {{site.data.keyword.discoveryshort}} looks at each result and tries to match the paths that you define. When matches occur, they are added to the results set. When you create a query, you can be as vague or as specific as you want. The more specific the query, the more targeted the results.

Documents that you do not have permissions to access are not returned in query results.
{: important}

The queries that you write might vary by collection and project because all collections and projects contain unique content.
{: tip}

## How to structure a basic query
{: #structure-basic-query}

JSON is hierarchical, so {{site.data.keyword.discoveryshort}} Query Language queries need to be written by using that same hierarchy. So if your JSON looks like this:

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

  Operators that evaluate a field (`<=` , `>=`, `<`, `>`) require a `number` or `date` as the value. Using quotations around a value always makes it a `string`. Therefore, `score>=0.5` is a valid query and `score>="0.5"` is not. See [Query operators](/docs/discovery-data?topic=discovery-data-query-operators) for a complete list of operators.
  {: tip}

## Building combined queries
{: #building-combined-queries}

You can combine query parameters together to build more targeted queries. For example, you can use both the `filter` and `query` parameters together. For more information about filtering versus querying, see [Differences between the filter and query parameters](/docs/discovery-data?topic=discovery-data-query-parameters#filtervquery).

## How to structure an aggregation
{: #structure-aggregation}

Aggregations return a set of data values. For the full list of aggregation options, see [Aggregations](/docs/discovery-data?topic=discovery-data-query-reference#aggregations).

![Example aggregation query structure](images/aggregation_structure.png)

This example aggregation finds all of the `concepts` in your collection.
The delimiter in this query is `.` and the operator is `()`, see [Query operators](/docs/discovery-data?topic=discovery-data-query-operators) to learn about other operators available in the {{site.data.keyword.discoveryshort}} Query Language.

### Example aggregation queries
{: #example-aggregations}

You can aggregate results with {{site.data.keyword.discoveryshort}} in many ways, including `top` values, `sum`, `min`, `max`, `average`, `timeslice`, and `histogram`. You can also add filters and nest aggregations.

#### Filter aggregations
{: #filter-aggregations}

This example aggregation returns the number of articles that are found in a collection of articles about Pittsburgh and how many of those results have a `positive`, `negative`, or `neutral` sentiment.

- `filter(enriched_text.entities.text:"Pittsburgh").term(enriched_text.sentiment.document.label,count:3)`


#### Nested aggregations
{: #nested-aggregations}

Adding `nested` before an aggregation restricts the aggregation to the area of the results specified. For example, `nested(enriched_text.entities)` means that only the `enriched_text.entities` components of any result are used to aggregate against.

For example, look at the differences between the following two queries:

-  `filter(enriched_text.entities.disambiguation.subtype::City)` - the aggregation counts the number of *Results* that contain one or more `entity` with the type `City`
-  `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` - the aggregation counts the number of instances of an `entity` with the type `City` in the results.  

Additionally, any subsequent operation restricts the result set that can be aggregated against. For example:

-  `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City)` means that only entities of `subtype::City` are aggregated.
-  `nested(enriched_text.entities).filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` aggregates the top three entities of subtype `City`
-  `filter(enriched_text.entities.disambiguation.subtype::City).term(enriched_text.entities.text,count:3)` returns the top three entities where the result contains at least one entity of subtype `City`.

## Querying with document level security enabled
{: #querydls}

If you enabled document level security on a collection, you can control search results at query time at the user level. See [Configuring document level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls) for information about using the security settings of your source documents.

To return search results that restrict query results to the security settings of authorized users, those users: 
-  Must be associated with your {{site.data.keyword.discoveryshort}} instance. See [Creating users for document level security](/docs/discovery-data?topic=discovery-data-collection-types#createusersdls) for instructions.
-  Must be present in the source system (Box, SharePoint OnPrem, or SharePoint Online).
If both criteria are not met, no results are returned.

The username that is associated with your {{site.data.keyword.discoveryshort}} instance is used to generate an authorization token. That token is used in your {{site.data.keyword.discoveryshort}} queries.

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

For more information about how to write queries by using the {{site.data.keyword.discoveryshort}} API, see the [API Reference](https://{DomainName}/apidocs/discovery-data#query){: external}.
{: tip}    

Each user's query results are restricted to their document permissions.

## Query limits
{: #query-limits}

A query is any operation that submits a POST request to the `/query` endpoint of the API. Such operations include queries that are submitted from the search bar on the *Improve and customize* page and by using the API. A query is counted only if the request is successful, meaning it returns a response (with message code 200).

The number of search queries that you can submit per month per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Queries per month per service instance |
|--------------|--------------------------------:|
| Cloud Pak for Data |                 Unlimited |
| Premium      |                       Unlimited |
| Plus (includes Trial)         |        500,000 |
{: caption="Number of queries per month" caption-side="top"}

The number of queries that can be processed per second per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Concurrent queries per service instance |
|--------------|--------------------------------:|
| Cloud Pak for Data |                 Unlimited |
| Premium      |                              50 |
| Plus (includes Trial) |                      5 |
{: caption="Number of concurrent queries" caption-side="top"}

For more information about the supported number of queries for Lite and Advanced plan instances, see [Discovery pricing plans](/docs/discovery?topic=discovery-discovery-pricing-plans#advanced){: external} in the earlier version of the product documentation.

## Estimating query usage
{: #query-estimate}

How to estimate the number of queries your application will use per month depends on your use case. 

- For use cases that focus more on data enrichment and analysis or where the output from the document processing is not heavily searched, you can estimate query numbers based on the total number of documents.
- For use cases where many users interact with the application that leverages Discovery, you can estimate by calculating the number of searches per user times the number of expected users. For example, 50% of the questions that are submitted by users to a virtual assistant are likely to be answered by Discovery. With 100,000 users per month and an average of 3 questions per user, you can expect 15,000 queries per month. (10,000 users/mo * 3 queries/user * 50% to Discovery = 15,000)

