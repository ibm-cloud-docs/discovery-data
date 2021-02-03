---

copyright:
  years: 2020, 2021
lastupdated: "2021-02-03"

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

# Default project settings
{: #project-defaults}

To learn more about projects, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects) and the [Create a project](https://{DomainName}/apidocs/discovery-data#createproject){: external} method in the API reference.

**Basic project defaults**

| Default | Document Retrieval | Document Retrieval (Content Intelligence) | Conversational search | Content Mining | Custom |
| --- | --- | --- | --- | --- | --- |
| OCR |  off |  on | off | off | off |
| Enrichments | Entities, Parts of speech  | Entities, Parts of speech, Table Understanding, and Contracts | None | Parts of speech | None  |
| Improvement tools | Facets (by Entity), Dynamic Facets, Passages | Facets (by Category, Nature, Contract Term, Contract Payment Term, Contract Type, Contract Currency, Invoice Buyer, Invoice supplier, Invoice Currency, Purchase Order Buyer, Purchase Order Supplier, Purchase Order Payment Term) and Table Retrieval | Passages | None | Passages |
| CSV settings | NA  | NA  | NA | No header, selected delimiters are comma and semicolon | NA |

## Default query settings
{: #query-defaults}

| Query default | Document Retrieval | Document Retrieval (Content Intelligence) | Conversational search | Content Mining | Custom |
| --- | --- | --- | --- | --- | --- |
| Passages</br>(`passages`) |  |   |  |  | |
| Enabled</br>(`passages.enabled`) | true | true  | true | false | true |
| Count</br>(`passages.count`)| 10 | 10  | 10 | 10 | 10 |
| Fields</br>(`passages.fields`)  | ["text", "title"] | ["text", "title"]  | ["text", "title"] | ["text", "title"] | ["text", "title"] |
| Characters</br>(`passages.characters`)  | 200  | 200  | 200  | 200 | 200 |
| Per document</br>(`passages.per_document`) | true  | true  | true | true | true |
| Max per document</br>(`passages.max_per_document`) | 1 | 1  | 1 | 1 | 1 |
| | | | | | |
| Table results</br>(`table_results`) | |   |  |  | |
| Enabled</br>(`table_results.enabled`)| false | true  | false | false | false |
| Count</br>(`table_results.count`)  | 10 | 10 | 10  | 10 | 10 |
| Per document</br> (`table_results.per_document`) | 0  | 0  | 0 | 0 | 0 |
| Find answers</br>(`find_answers`) |  |   |  |  | |
| Enabled</br>(`find_answers.enabled`) | false | false  | false | false | false |
| Max answers per passage</br>(`max_answers_per_passage`) | 1 | 1  | 1 | 1 | 1 |
| | | | | |
| Aggregation</br>(`aggregation`) | "term(enriched_text.entities.text,</br>name:entities)"  | "[term</br>(enriched_html.contract.elements.categories.label,</br>count:25,name:categories)"  | "" | "" | "" |
| Suggested refinements</br>(`suggested_refinements`) |   |  |  |  | |
| Enabled</br>(`suggested_refinements.enabled`) | false | false | false | false | false | 
| Count</br>(`suggested_refinements.count`) | 10 | 10  | 10 | 10 | 10 |
| | | | | | |
| Spelling suggestions</br>(`spelling_suggestions`) | true  | true  | false | true | true |
| Highlight</br>(`highlight`) | false | false  | false | false | false |
| Count</br>(`count`) | 10  | 10  | 10  | 10 |  10 |
| Sort</br>(`sort`) | ""  | ""   | ""  | "" | "" |
| Return</br>(`return`)| []  | []  | []  | [] | [] |

## Project component settings
{: #component-defaults}

For more information, see the [Configuration settings for components](https://{DomainName}/apidocs/discovery-data#getcomponentsettings){: external} method in the API reference.


| Default | Document Retrieval | Document Retrieval (Content Intelligence) | Conversational search | Content Mining | 
| --- | --- | --- | --- | --- | 
| Fields shown</br>(`fields_shown`) |   |   |  |  | 
| Title/field</br> (`fields_shown.title.field`) | "title"  | "title" | "title" | "document_id" | 
| Body</br>(`fields_shown.body`) | |  |  |  | 
| Use passage</br> (`fields_shown.body.use_passage`) | true  |  true | true  | false | 
| Field</br> (`fields_shown.body.field`)| ""  |  "" | "" | text | 
| | | | | | |
| Autocomplete</br>(`autocomplete`) | true  | true  | false | true | 
| Structured search</br>(`structured_search`) | false  |  false | false  | false  | 
| Results per page</br> (`results_per_page`) | 5  | 5  | 0 | 0 | 
| Aggregations</br>(`aggregations.name`)</br>(`aggregations.label`)</br>(`aggregations.multiple_selections_allowed`) | "name": "entities"</br> "label": "Top Entities"</br> "multiple_selections_allowed": false </br> </br>"name": "_system_suggested_refinements"</br> "label": "Dynamic Facets"</br>"multiple_selections_allowed": true </br></br>"name": "_system_collections"</br>"label": "Collections"</br>"multiple_selections_allowed": true | "name": "categories"</br> "label": "Category"</br> "multiple_selections_allowed": true</br></br> "name": "natures"</br> "label": "Nature"</br>"multiple_selections_allowed": false</br></br>"name": "contract_terms"</br> "label": "Contract Term"</br> "multiple_selections_allowed": false</br></br>"name": "contract_payment_terms"</br>"label": "Contract Payment Term"</br>"multiple_selections_allowed": false</br> </br>"name": "contract_types"</br> "label": "Contract Type"</br> "multiple_selections_allowed": false</br></br> "name": "contract_currencies"</br> "label": "Contract Currency"</br>"multiple_selections_allowed": false</br></br>"name": "invoice_buyers"</br> "label": "Invoice Buyer"</br> "multiple_selections_allowed": false</br></br>"name": "invoice_suppliers"</br> "label": "Invoice Supplier"</br> "multiple_selections_allowed": false</br></br>"name": "invoice_currencies"</br> "label": "Invoice Currency"</br> "multiple_selections_allowed": false</br></br>"name": "po_payment_terms"</br> "label": "Purchase Order Payment Term"</br> "multiple_selections_allowed": false</br></br>"name": "po_buyers"</br> "label": "Purchase Order Buyer"</br> "multiple_selections_allowed": false</br></br>"name": "po_suppliers"</br> "label": "Purchase Order Supplier"</br> "multiple_selections_allowed": false</br></br> "name": "po_currencies"</br>"label": "Purchase Order Currency"</br>"multiple_selections_allowed": false | [] | [] | 