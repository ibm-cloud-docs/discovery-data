---

copyright:
  years: 2020, 2021
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

# Default query settings
{: #query-defaults}

Learn about how the search query is configured for each project type by default.
{: shortdesc}

When you submit a search from the product user interface, your text is passed as a natural language query value to the Query API. Other parameters that you can define when you use the API are assigned default values for queries made from the user interface. The following tables explain which values are specified by default for each project type. For more information about the Query API, see [Query reference](/docs/discovery-data?topic=discovery-data-query-reference).

You can override some of the default values by using improvement tools in the user interface. For example, you can use the *Search results* tool to change parameters such as `passages.enabled` or `passages.fields`. For more information, see [Changing the result content](/docs/discovery-data?topic=discovery-data-query-results#query-results-content).

## Default query settings
{: #query-defaults-table1}

| Query default | Document Retrieval | Document Retrieval for Contracts |
| --- | --- | --- |
| `aggregation` | "term(enriched_text.entities.text, name:entities)"  | "[term (enriched_html.contract. elements.categories.label, count:25,name:categories)" |
| `count` | 10  | 10  |
| `highlight` | false | false |
| `passages.characters` | 200 | 200 |
| `passages.count` | 10 | 10 |
| `passages.enabled` | true | true |
| `passages.fields` | ["text", "title"] | ["text", "title"] |
| `passages.find_answers` | false | false |
| `passages.max_answers_per_passage` | 1 | 1 |
| `passages.max_per_document` | 1 | 1 |
| `passages.per_document` | true | true |
| `return` | [] | [] |
| `spelling_suggestions` | true | true |
| `sort` | "" | "" |
| *Premium plans only*: `suggested_refinements.count` | 10 | 10 |
| *Premium plans only*: `suggested_refinements.enabled` | false | false |
| `table_results.count` | 10 | 10 |
| `table_results.enabled` | false | true |
| `table_results.per_document` | 0 | 0 |
{: caption="Default query settings" caption-side="top"}

## Default query settings continued
{: #query-defaults-table-cont}

| Query default | Conversational Search | Content Mining | Custom |
| --- | --- | --- | --- |
| `aggregation` | "" | "" | "" |
| `count` | 10  | 10 |  10 |
| `highlight` | false | false | false |
| `passages.characters` | 200  | 200 | 200 |
| `passages.count` | 10 | 10 | 10 |
| `passages.enabled` | true | false | true |
| `passages.fields` | ["text", "title"] | ["text", "title"] | ["text", "title"] |
| `passages.find_answers` | false | false | false |
| `passages.max_answers_per_passage` | 1 | 1 | 1 |
| `passages.max_per_document` | 1 | 1 | 1 |
| `passages.per_document` | true | true | true |
| `return` | [] | [] | [] |
| `spelling_suggestions` | false | true | true |
| `sort` | "" | "" | "" |
| *Premium plans only*: `suggested_refinements.count` | 10 | 10 | 10 |
| *Premium plans only*: `suggested_refinements.enabled` | false | false | false |
| `table_results.count` | 10 | 10 | 10 |
| `table_results.enabled` | false | false | false |
| `table_results.per_document` | 0 | 0 | 0 |
{: caption="Default query settings continued" caption-side="top"}

## Project component settings
{: #component-defaults-dr}

| Default | Document Retrieval | Document Retrieval for Contracts |
| --- | --- | --- |
| Aggregations | See [table](#aggregations-dr) | See [table](#aggregations-dr-contracts) |
| Autocomplete (`autocomplete`) | true | true |
| Fields shown Body field  (`fields_shown.body.field`)| "" |  "" |
| Fields shown Body Use passage  (`fields_shown.body.use_passage`) | true  | true |
| Fields shown Title/field  (`fields_shown.title.field`) | "title" | "title" |
| Results per page  (`results_per_page`) | 5  | 5 |
| Structured search (`structured_search`) | false  | false |
{: caption="Project component settings" caption-side="top"}

## Project component settings continued
{: #component-defaults-cont}

The Custom project type has no project component default settings.
{: note}

| Default | Conversational search | Content Mining |
| --- | --- | --- |
| Aggregations | [] | [] |
| Autocomplete (`autocomplete`) | false | true |
| Fields shown Body field  (`fields_shown.body.field`)| "" | text |
| Fields shown Body Use passage  (`fields_shown.body.use_passage`) | true | false |
| Fields shown Title/field  (`fields_shown.title.field`) | "title" | "document_id" |
| Results per page  (`results_per_page`) | 0 | 0 |
| Structured search (`structured_search`) | false | false |
{: caption="Project component settings continued" caption-side="top"}

## Document Retrieval project aggregations
{: #aggregations-dr}

| `aggregations.name` | `aggregations.label` | `aggregations.multiple_selections_allowed` |
|---|---|---|
| "name": "entities" | "label": "Top Entities"  | "multiple_selections_allowed": false |
| *Premium plans only*: "name": "_system_suggested_refinements" | "label": "Dynamic Facets" | "multiple_selections_allowed": true |
| "name": "_system_collections" | "label": "Collections" | "multiple_selections_allowed": true |
{: caption="Document Retrieval project aggregations" caption-side="top"}

## Document Retrieval for Contracts project aggregations
{: #aggregations-dr-contracts}

| `aggregations.name` | `aggregations.label` | `aggregations.multiple_selections_allowed` |
|---|---|---|
| "name": "categories" | "label": "Category" | "multiple_selections_allowed": true |
| "name": "natures" | "label": "Nature" | "multiple_selections_allowed": false |
| "name": "contract_terms" | "label": "Contract Term" | "multiple_selections_allowed": false |
| "name": "contract_payment_terms" | "label": "Contract Payment Term" | "multiple_selections_allowed": false |
| "name": "contract_types" | "label": "Contract Type" | "multiple_selections_allowed": false |
| "name": "contract_currencies" | "label": "Contract Currency" | "multiple_selections_allowed": false |
| "name": "invoice_buyers" | "label": "Invoice Buyer" | "multiple_selections_allowed": false |
| "name": "invoice_suppliers" | "label": "Invoice Supplier" | "multiple_selections_allowed": false |
| "name": "invoice_currencies" | "label": "Invoice Currency" | "multiple_selections_allowed": false |
| "name": "po_payment_terms" | "label": "Purchase Order Payment Term" | "multiple_selections_allowed": false |
| "name": "po_buyers" | "label": "Purchase Order Buyer" | "multiple_selections_allowed": false |
| "name": "po_suppliers" | "label": "Purchase Order Supplier" | "multiple_selections_allowed": false |
| "name": "po_currencies" | "label": "Purchase Order Currency" | "multiple_selections_allowed": false |
{: caption="Document Retrieval for Contracts project aggregations" caption-side="top"}
