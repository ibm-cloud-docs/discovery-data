---

copyright:
  years: 2019, 2022
lastupdated: "2022-08-17"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Query aggregations
{: #query-aggregations}

You can use aggregations when you write queries with the {{site.data.keyword.discoveryshort}} Query Language. For more information, see the {{site.data.keyword.discoveryshort}} [API reference](https://{DomainName}/apidocs/discovery-data#query){: external}. For an overview of query concepts, see the [Query overview](/docs/discovery-data?topic=discovery-data-query-concepts).
{: shortdesc}

Aggregations return a set of data values. A maximum of 50,000 values can be returned for a single query. If more than 50,000 values are returned, then an error is displayed.

For the complete list of available aggregations, see the [Query reference](/docs/discovery-data?topic=discovery-data-query-reference#aggregations).

## `average`
{: #average}

Returns the mean of values of the specified field across all matching documents.

For example:

```json
average(product_price)
```
{: codeblock}

## `filter`
{: #aggfilter}

A modifier that narrows down the document set of the aggregation query it precedes. This example filters the set to include only documents that mention `IBM`.

For example:

```json
filter(enriched_text.entities.text:"IBM")
```
{: codeblock}

## `histogram`
{: #histogram}

Creates numeric interval segments to categorize documents. Uses field values from a single numeric field to describe the category. The field used to create the histogram must be of number (`integer`, `float`, `double`, or `date`) type. Non-number types such as `string` are not supported. For example, `"price": 1.30` is a number value that works, and `"price": "1.30"` is a string, so it wouldn’t work. Use the `interval` argument to define the size of the sections the results are split into. Interval values must be whole, non-negative numbers, and are set to make sense for segmenting your possible field values.

For example, if your data set includes the price of several items, like: `“price”: 1.30`, `“price”: 1.99`, and `“price”: 2.99`, you might use intervals of `1`, so that you see everything that is grouped in the range `1 - 2`, and `2` and `3`. You would probably not use an interval of `100`, because then all the data would end up in the same segment. Histograms can process decimal values, but intervals must be whole numbers. The syntax is `histogram(<field>,<interval>)`, as shown in the following example.

For example:

```json
histogram(product_price,interval:1)
```
{: codeblock}

## `max`
{: #max}

Returns the highest value in the specified field across all matching documents.

For example:

```json
max(product_price)
```
{: codeblock}

## `min`
{: #min}

Returns the lowest value in the specified field across all matching documents.

For example:

```json
min(product_price)
```
{: codeblock}

## `nested`
{: #nested}

Applying `nested` before an aggregation query restricts the aggregation to the area of the results that are specified. For example, `nested(enriched_text.entities)` means that only the `enriched_text.entities` components of any result are used to aggregate against.

For example:

```json
nested(enriched_text.entities)
```
{: codeblock}

## `sum`
{: #sum}

Adds the values of the specified field across all matching documents.

For example:

```json
sum(product_price)
```
{: codeblock}

## `term`
{: #term}

Returns the top values (by score and by frequency) for the selected enrichments. All enrichments are valid values. You can optionally use `count` to specify the number of terms to return. This example returns the full text and enrichments of the top values with the Entities enrichment, and specifies to return 10 terms.

For example:

```json
term(enriched_text.entities.text,count:10)
```
{: codeblock}

## `timeslice`
{: #timeslice}

A specialized histogram that uses dates to create interval segments. Valid date interval values are `second/seconds` `minute/minutes`, `hour/hours`, `day/days`, `week/weeks`, `month/months`, and `year/years`. The syntax is `timeslice(<field>,<interval>,<time_zone>)`. To use `timeslice`, the time fields in your documents must be of the `date` data type and in [UNIX time](https://en.wikipedia.org/wiki/Unix_time){: external} format. Unless both of these requirements are met, the `timeslice` parameter does not work correctly. You can create a timeslice if your documents contain `date` fields with values such as `1496228512`. The value must be in a numeric format (for example, `float` or `double`) and not enclosed in quotation marks. The service treats dates in text and dates in ISO 8601 format as data type `string`, not as data type `date`.

## `top_hits`
{: #top_hits}

Returns the documents ranked by the score of the query or enrichment. Can be used with any query parameter or aggregation. This example returns the 10 top hits for a term aggregation.

For example:

```json
term(enriched_text.entities.text).top_hits(10)
```
{: codeblock}

## `unique_count`
{: #unique_count}

Returns a count of the unique instances of the specified field in the collection.

Examples:

```json
unique_count(enriched_text.keyword.text)
```
{: codeblock}

```json
nested(enriched_text.entities).term(enriched_text.entities.text,count:3).unique_count(enriched_text.entities.type)
```
{: codeblock}
