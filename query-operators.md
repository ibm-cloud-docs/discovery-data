---

copyright:
  years: 2019, 2025
lastupdated: "2025-01-27"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Query operators
{: #query-operators}

You can use operators when you write queries to submit to {{site.data.keyword.discoveryshort}} by using the Query API.
{: shortdesc}

The types of operators that are supported differ by query type:

-   [Natural language queries](#nlq-operator)
-   [Discovery Query Language (DQL) queries](#dql-operators)

## Natural Language Query (NLQ) operator
{: #nlq-operator}

The `natural_language_query` parameter accepts a string value.

### `""` (Phrase query)
{: #phrase-nlq}

Use quotation marks to emphasize a single word or phrase in the query that is most important to match. For example, the following request boosts documents that contain the term “nomination” in them.

```json
{
  "natural_language_query":"What is the process for \"nomination\" of bonds?"
}
```
{: codeblock}

Specifying a quoted phrase does not prevent documents without the phrase from being returned. It merely gives more weight to documents with the phrase than those without it. For example, the query results might also contain documents that mention “bonds” or “process” and do not contain the word “nomination”.

The following request boosts the phrase “change in monetary policy” and also matches “change” or “monetary” or “policy”.

```json
{
  "natural_language_query":"\"change in monetary policy\""
}
```
{: codeblock}

Single quotation marks (') are not supported. You cannot use wildcards (*) in phrase queries.

## Discovery Query Language (DQL) operators
{: #dql-operators}

Operators are the separators between different parts of a query.

### `.` (JSON delimiter)
{: #delimiter}

This delimiter separates the levels of hierarchy in the JSON schema

For example, the following query argument identifies the section of the enriched_text object that contains entities and the text recognized as an entity.

```bash
enriched_text.entities.text
```
{: codeblock}

The JSON representation of this section looks as follows:

![JSON source that shows the enriched_text.entities.text object structure](images/api-placement.png){: caption="JSON representation of the enriched_text.entities.text field" caption-side="bottom"}

### `:` (Includes)
{: #includes}

This operator specifies inclusion of the full query term.

For example, the following query searches for documents that contain the term `cloud computing` in the `text` field:

```json
{
  "query":"enriched_text.entities.text:\"cloud computing\""
}
```
{: codeblock}

The **includes** operator does not return a partial match for the query term. If you want to find a partial match for a term, use a **wildcard** operator with the **includes** operator. For example, if you want to find any occurrences of `TP53` or `p53` in the `test_results` field, the following query will *not* find occurrences of both terms:

```json
{
  "query":"test_results:P53"
}
```
{: codeblock}

Instead, include a wildcard in the request. For example, use the following query request. Because we are using the wildcard operator, we also changed the term to lowercase.

```json
{
  "query":"test_results:*p53"
}
```
{: codeblock}

With this syntax, occurrences of `p53`, `tp53`, `P53`, or `TP53` are all returned.

### `""` (Phrase query)
{: #phrase-dql}

Phrase queries only match occurrences of the whole phrase. The order of the words in the phrase must match.

For example, the following query returns only documents that contain a field named `quotation` with the text, `There's no crying in baseball`.

```json
{
  "query":"quotation:\"There's no crying in baseball\""
}
```
{: codeblock}

A document with a `quotation` field that says `Jimmy Dugan said there's no crying in baseball` is also returned. However, documents that only mention `baseball` or `crying` without the entire phrase are not matched. Neither is a document with `In baseball, there's no crying`. Documents that contain the right text in the wrong field also are not matched. For example, a document with the text `There's no crying in baseball` in the `text` field is not returned.

Single quotation marks (') are not supported. You cannot use wildcards (*) in phrase queries.

### `::` (Exact match)
{: #match}

This operator specifies an exact match for the query term. Exact matches are case-sensitive.

For example, the following query searches for documents that contain entities of type `Organization`:

```json
{
  "query":"enriched_text.entities.type::Organization"
}
```
{: codeblock}

The entire content of the field that you specify must match the phrase you specify. For example, the following query finds documents in which only entity mentions of `IBM Cloud` are detected, not `IBM Cloud Pak for Data` or `IBM cloud` or `Cloud`.

```json
{
  "query":"enriched_text.entities.text::\"IBM Cloud\""
}
```
{: codeblock}

Cannot match document fields that are greater than 256 characters in length.
{: note}

To get the query results for a given character symbol, see the following example:

```json
curl -X POST "https://api.jp-tok.discovery.watson.cloud.ibm.com/instances/<instance-id>/v2/projects/<project-id>/query?version=2023-03-31" \
  -u "apikey:<wd-api-key>" \
  --header "Content-Type: application/json" \
  --data '{
    "query": "<field-with-symbol>::*￥*"
  }'
```
{: codeblock}

This example query is to query ￥. You can replace ￥ with the required character symbol that you want to search. The search returns the matched value provided the field's value that includes the searchable symbol has a length less than [256 chars](#match). Also, the whole document is matched regardless of which part of a document is relevant to the query.

### `:!` (Does not include)
{: #notinclude}

This operator specifies that the results do not contain a match for the query term.

For example:

```json
{
  "query":"enriched_text.entities.text:!\"cloud computing\""
}
```
{: codeblock}

### `::!` (Not an exact match)
{: #notamatch}

This operator specifies that the results do not exactly match the query term.

For example:

```json
{
  "query":"enriched_text.entities.text::!\"Cloud computing\""
}
```
{: codeblock}

Exact matches are case-sensitive.

Will retrieve document fields matching the query term if the field is over 256 characters in length.
{: note}

### `\` (Escape character)
{: #escape}

Escape character that preserves the literal value of the operator that follows it. 

The complete list of valid escape sequences within text queries (except phrase queries):

`\"`,`\\`,`\(`,`\)`,`\[`,`\]`,`\,`,`\|`,`\^`,`\~`,`\:`,`\<=`,`\>=`,`\<`,`\>`,`\:!`,`\::`,`\::!`,`\*`,`\!`

For example, `message:\>=D`,`method::foo\(String\)`.

Within a phrase query, the only valid escape sequence is `\"`.

For example, `name:"Shane \"Rapha\" Hendrixson"`, `method::"foo(String)"`.

DQL is submitted to the [Query API](https://{DomainName}/apidocs/discovery-data#query){: external} as JSON string fields, which require their own additional layer of escaping, for example:

```json
{
  "query":"name:\"Shane \\\"Rapha\\\" Hendrixson\""
}
```
{: codeblock}

### `()`,`[]` (Nested grouping)
{: #nestedquery}

Logical groupings can be formed to specify more specific information.

For example:

```json
{
  "query":"enriched_text.entities:(text:IBM,type:Company)"
}
```
{: codeblock}

### `|` (or)
{: #or}

Boolean operator for "or".

In the following example, documents in which `Google` or `IBM` are identified as entities are returned:

```json
{
  "query":"enriched_text.entities.text:Google|enriched_text.entities.text:IBM"
}
```
{: codeblock}

The includes (`:`,`:!`) and match (`::`, `::!`) operators have precedence over the `OR` operator.
{: note}

For example, the following syntax searches for documents in which `Google` is identified as an entity or the string `IBM` is present:

```json
{
  "query":"enriched_text.entities.text:Google|IBM"
}
```
{: codeblock}

It is treated as follows:

```bash
(enriched_text.entities.text:Google) OR IBM
```
{: codeblock}

### `,` (and)
{: #and}

Boolean operator for "and".

In the following example, documents in which `Google` and `IBM` both are identified as entities are returned:

```json
{
  "query":"enriched_text.entities.text:Google,enriched_text.entities.text:IBM"
}
```
{: codeblock}

The includes (`:`,`:!`) and match (`::`, `::!`) operators have precedence over the `AND` operator.
{: note}

For example, the following syntax searches for documents in which `Google` is identified as an entity and the string `IBM` is present:

```json
{
  "query":"enriched_text.entities.text:Google,IBM"
}
```
{: codeblock}

It is treated as follows:

```bash
(enriched_text.entities.text:Google) AND IBM
```
{: codeblock}

### `<=, >=, >, <` (Numerical comparisons)
{: #comparisons}

Creates numerical comparisons of `less than` or `equal to`, `greater than` or `equal to`, `greater than`, and `less than`.

Only use numerical comparison operators when the value is a `number` or `date`.

Any value that is surrounded by quotations is a String. Therefore, `score>=0.5` is a valid query and `score>="0.5"` is not.
{: tip}

For example:

```json
{
  "query":"invoice.total>100.50"
}
```
{: codeblock}

### `^x` (Score multiplier)
{: #multiplier}

Increases the score value of a search term.

For example:

```json
{
  "query":"enriched_text.entities.text:IBM^3"
}
```
{: codeblock}

### `*` (Wildcard)
{: #wildcard}

Matches unknown characters in a search expression. Do not use capital letters with wildcards.

For example:

```json
{
  "query":"enriched_text.entities.text:ib*"
}
```
{: codeblock}

### `~n` (String variation)
{: #variation}

The number of character differences that are allowed when matching a string. The maximum variation number that can be used is 2.

For example, the following query returns documents that contain `car` in the title field, as well as `cap`,`cat`,`can`, `sat`, and so on:

```json
{
  "query":"title:cat~1"
}
```
{: codeblock}

The normalized version of the word is used for matching. Therefore, if the input contains "cats", the search looks for "cat", which is the normalized form of the plural cats.

When a phrase is submitted, each term in the phrase is allowed the specified number of variations. For example, the following input matches `cat dog` and `far log` in addition to `car hog`.

For example:

```json
{
  "query":"title:\"car hog\"~1"
}
```
{: codeblock}

### `:*` (Exists)
{: #exists}

Used to return all results where the specified field exists.

For example:

```json
{
  "query":"title:*"
}
```
{: codeblock}

### `:!*` (Does not exist)
{: #dnexist}

Used to return all results that do not include the specified field.

For example:

```json
{
  "query":"title:!*"
}
```
{: codeblock}

For more information, see the {{site.data.keyword.discoveryshort}} [API reference](https://{DomainName}/apidocs/discovery-data#query){: external}. 

For an overview of query concepts, see the [Query overview](/docs/discovery-data?topic=discovery-data-query-concepts).
