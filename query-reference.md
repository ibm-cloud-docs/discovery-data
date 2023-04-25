---

copyright:
  years: 2019, 2023
lastupdated: "2021-10-03"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Query reference
{: #query-reference}

The full list of {{site.data.keyword.discoveryshort}} query parameters, operators, and aggregations. You can refer to this information for help when you write queries with the {{site.data.keyword.discoveryshort}} Query Language.

- For more information, see the {{site.data.keyword.discoveryshort}} [API reference](https://{DomainName}/apidocs/discovery-data#query){: external}.
- For an overview of query concepts, see the [Query overview](/docs/discovery-data?topic=discovery-data-query-concepts).
{: shortdesc}

In the {{site.data.keyword.discoveryshort}} user interface, you can write and test [natural language queries](/docs/discovery-data?topic=discovery-data-query-parameters#nlq) on the *Improve and customize* page.
{: tip}

## Parameters descriptions
{: #parameter-descriptions}

Use query parameters to search your collection, identify a result set, and analyze result sets.

| Parameter | Description | Example |
|-----------|-------------|---------|
| [`aggregation`](#aggregations) | A statistical query of the results set | `aggregation=term(enriched_text.entities.type)` |
| [`filter`](/docs/discovery-data?topic=discovery-data-query-parameters#filter) | An unranked query language search for matching documents. | `filter=bees` |
| [`natural_language_query`](/docs/discovery-data?topic=discovery-data-query-parameters#nlq) | A ranked natural language search for matching documents | `natural_language_query="How do bees fly"` |
| [`query`](/docs/discovery-data?topic=discovery-data-query-parameters#query) | A ranked query language search for matching documents. | `query=bees` |
{: caption="Search parameters" caption-side="top"}

| Parameter | Description | Example |
|-----------|-------------|---------|
| [`count`](/docs/discovery-data?topic=discovery-data-query-parameters#count) | The number of `result` documents to return. | `count=15` |
| [`highlight`](/docs/discovery-data?topic=discovery-data-query-parameters#highlight) | Highlight query matches | `highlight=true` |
| [`offset`](/docs/discovery-data?topic=discovery-data-query-parameters#offset) | The number of results to ignore before returning `result` documents from the results set | `offset=100` |
| [`return`](/docs/discovery-data?topic=discovery-data-query-parameters#return) | List of fields to return | `return=title,url` |
| [`sort`](/docs/discovery-data?topic=discovery-data-query-parameters#sort) | Field to sort results set by | `sort=enriched_text.sentiment.document.score` |
| [`spelling suggestions`](/docs/discovery-data?topic=discovery-data-query-parameters#spell) | Spelling suggestions returned for natural language queries | `spelling_suggestions=true` |
{: caption="Structure parameters" caption-side="top"}

### Query limitations
{: #query-limitations}

You cannot query on field names that contain the following characters:

- Numbers (`0 - 9`) in the suffix of the field name. For example, `extracted-content2`.
- The characters `_`, `+`, and `-` in the prefix of the `field_name`. For example, `+extracted-content`.
- The characters `.`, `,`, and `:` in the `field_name`. For example, `new:extracted-content`.

## Operators
{: #operators}

Operators are the separators between different parts of a query. The following table lists the available operators.

| Operator | Description | Example |
|----------|-------------|---------|
| [`.`](/docs/discovery-data?topic=discovery-data-query-operators#delimiter) | JSON delimiter | `enriched_text.concepts.text` |
| [`:`](/docs/discovery-data?topic=discovery-data-query-operators#includes) | Includes | `text:computer` |
| [`::`](/docs/discovery-data?topic=discovery-data-query-operators#match) | Exact match | `title::"Query building"` |
| [`:!`](/docs/discovery-data?topic=discovery-data-query-operators#notinclude) | Does not include | `text:!computer` |
| [`::!`](/docs/discovery-data?topic=discovery-data-query-operators#notamatch) | Not an exact match | `text::!winter` |
| [`\\`](/docs/discovery-data?topic=discovery-data-query-operators#escape) | Escape character | `title::"Dorothy said: \\"There's no place like home.\\""` |
| [`""`](/docs/discovery-data?topic=discovery-data-query-operators#phrase) | Phrase query | `enriched_text.concepts.text:"IBM Watson"` |
| [`()`, `[]`](/docs/discovery-data?topic=discovery-data-query-operators#nestedquery) | Nested groups | `filter-entities:(text:Turkey,type:Location)` |
| [\|](/docs/discovery-data?topic=discovery-data-query-operators#or) | or | `query-enriched.entities.text:Google\|IBM` |
| [`,`](/docs/discovery-data?topic=discovery-data-query-operators#and) | and | `query-enriched.entities.text:Google,IBM` |
| [`<=`, `>=`, `>`, `<`](/docs/discovery-data?topic=discovery-data-query-operators#comparisons) | Numerical comparisons |  `enriched_text.sentiment.document.score>0.679`     |
| [`^x`](/docs/discovery-data?topic=discovery-data-query-operators#multiplier) | Score multiplier | `text:IBM^3` |
| [`*`](/docs/discovery-data?topic=discovery-data-query-operators#wildcard) | Wildcard | `query-enriched_text.concepts.text:pre*` |
| [`~n`](/docs/discovery-data?topic=discovery-data-query-operators#variation) | String variation | `query-enriched_text.entities.text:cat~1` |
| [`:*`](/docs/discovery-data?topic=discovery-data-query-operators#exists) | Exists | `title:*` |
| [`!*`](/docs/discovery-data?topic=discovery-data-query-operators#dnexist) | Does not exist | `title!*` |
{: caption="Query operators" caption-side="top"}

## Aggregations
{: #aggregations}

Aggregations return a set of data values. The following table lists the available aggregations.

| Aggregation | Description | Example |
|-------------|-------------|---------|
| [`average`](/docs/discovery-data?topic=discovery-data-query-aggregations#average) | Mean value for the specified field in the results set. | `average(product.price)` |
| [`filter`](/docs/discovery-data?topic=discovery-data-query-aggregations#aggfilter) | Filter results based on the specified pattern | `filter(enriched_text.concepts.text:cloud computing)` |
| [`histogram`](/docs/discovery-data?topic=discovery-data-query-aggregations#histogram) | Interval-based distribution | `histogram(product.price,interval:1)` |
| [`max`](/docs/discovery-data?topic=discovery-data-query-aggregations#max) | Maximum value for the specified field in the results set. | `max(product.price)` |
| [`min`](/docs/discovery-data?topic=discovery-data-query-aggregations#min) | Minimum value for the specified field in the results set. | `min(product.price)` |
| [`nested`](/docs/discovery-data?topic=discovery-data-query-aggregations#nested) | Restrict aggregation | `nested(enriched_text.entities)` |
| [`sum`](/docs/discovery-data?topic=discovery-data-query-aggregations#sum) | Sum of all fields in the results set. | `sum(product.price)` |
| [`term`](/docs/discovery-data?topic=discovery-data-query-aggregations#term) | Count of identical values | `term(enriched_text.concepts.text,count:10)` |
| [`timeslice`](/docs/discovery-data?topic=discovery-data-query-aggregations#timeslice) | Time-based distribution | `timeslice(last_modified,2day,America/New York)` |
| [`top_hits`](/docs/discovery-data?topic=discovery-data-query-aggregations#top_hits) | Top-ranked result documents for the current aggregation | `term(enriched_text.concepts.text).top_hits(10)` |
| [`unique_count`](/docs/discovery-data?topic=discovery-data-query-aggregations#unique_count) | Count of unique values for a field within an aggregation | `unique_count(enriched_text.entities.type)` |
{: caption="Query aggregations" caption-side="top"}
