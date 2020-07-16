---

copyright:
  years: 2020
lastupdated: "2020-07-15"

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

To learn more about projects, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects) and the [Create a project](https://{DomainName}/apidocs/discovery-data#create-a-project){: external} method in the API reference.

**Basic project defaults**

| Default | Document Retrieval | Document Retrieval (Discovery for Content Intelligence) | Conversational search | Content Mining | 
| --- | --- | --- | --- | --- |
| OCR |  off |  on | off | off |
| Enrichments | Entities, Parts of speech  | Entities, Parts of speech, Table Understanding, and Contracts | None | Parts of speech |
| Improvement tools | Facets (by Entity), Dynamic Facets, Passages | Facets (by Category, Nature, Contract Term, Contract Payment Term, Contract Type, Contract Currency, Invoice Buyer, Invoice supplier, Invoice Currency, Purchase Order Buyer, Purchase Order Supplier, Purchase Order Payment Term) and Table Retrieval | Passages | None |
| CSV settings | NA  | NA  | NA | No header, selected delimiters are comma and semicolon |

## Default query parameters
{: #query-defaults}

| Query default | Document Retrieval | Document Retrieval (Discovery for Content Intelligence) | Conversational search | Content Mining | 
| --- | --- | --- | --- | --- |
| Passages [Enabled/Count] | true/10 | true/10  | true/10 | false/10 |
| Fields | ["text", "title"] | ["text", "title"]  | ["text", "title"] | ["text", "title"] |
| Characters  | 200  | 200  | 200  | 200 |
| Per document | true  | true  | true | true |
| Max per document | 2 | 2  | 2 | 2 |
| - | - | - | - | - |
| Table results [Enabled/Count] | false/10 | true/10  | false/10 | false/10 |
| Per document | false  | false  | false | false |
| - | - | - | - | - |
| Aggregation | "term(enriched_text.entities.text,name:entities)"  | "[term(enriched_html.contract.elements.categories.label,count:25,name:categories)"  | "" | "" |
| Suggested refinements [Enabled/Count] | true/10  | false/10 | false/10 | false/10 |
| Spelling suggestions | true  | true  | false | true |
| Highlight | false   | false  | false | false |
| Count  | 10  | 10  | 10  | 10 |
| Sort | ""  | ""   | ""  | "" |
| Return | []  | []  | []  | [] |

## Project component settings
{: #component-defaults}

See the [Configuration settings for components](https://{DomainName}/apidocs/discovery-data#configuration-settings-for-components){: external} method in the API reference for more information.

**Document Retrieval** 

```json
{
  "fields_shown": {
    "body": {
      "use_passage": true,
      "field": ""
    },
    "title": {
      "field": "title"
    }
  },
  "autocomplete": true,
  "structured_search": false,
  "results_per_page": 5,
  "aggregations": [{
		"name": "entities",
		"label": "Top Entities",
		"multiple_selections_allowed": false
  },{
    "name": "_system_suggested_refinements",
    "label": "Dynamic Facets",
    "multiple_selections_allowed": true
  },
  {
    "name": "_system_collections",
    "label": "Collections",
    "multiple_selections_allowed": true
  }]
}
```
{: codeblock}


**Document Retrieval (Discovery for Content Intelligence)** 

```json
{
  "fields_shown": {
    "body": {
      "use_passage": true,
      "field": ""
    },
    "title": {
      "field": "title"
    }
  },
  "autocomplete": true,
  "structured_search": false,
  "results_per_page": 5,
  "aggregations": [{
         "name": "categories",
         "label": "Category",
         "multiple_selections_allowed": true
       },
       {
         "name": "natures",
         "label": "Nature",
         "multiple_selections_allowed": false
       },
       {
         "name": "contract_terms",
         "label": "Contract Term",
         "multiple_selections_allowed": false
       },
       {
         "name": "contract_payment_terms",
         "label": "Contract Payment Term",
         "multiple_selections_allowed": false
       },
       {
         "name": "contract_types",
         "label": "Contract Type",
         "multiple_selections_allowed": false
       },
       {
         "name": "contract_currencies",
         "label": "Contract Currency",
         "multiple_selections_allowed": false
       },
       {
         "name": "invoice_buyers",
         "label": "Invoice Buyer",
         "multiple_selections_allowed": false
       },
       {
         "name": "invoice_suppliers",
         "label": "Invoice Supplier",
         "multiple_selections_allowed": false
       },
       {
         "name": "invoice_currencies",
         "label": "Invoice Currency",
         "multiple_selections_allowed": false
       },
       {
         "name": "po_payment_terms",
         "label": "Purchase Order Payment Term",
         "multiple_selections_allowed": false
       },
       {
         "name": "po_buyers",
         "label": "Purchase Order Buyer",
         "multiple_selections_allowed": false
       },
       {
         "name": "po_suppliers",
         "label": "Purchase Order Supplier",
         "multiple_selections_allowed": false
       },
       {
         "name": "po_currencies",
         "label": "Purchase Order Currency",
         "multiple_selections_allowed": false
       }
     ]
}
```
{: codeblock}

**Conversational search** 

```json
{
  "fields_shown": {
    "body": {
      "use_passage": true,
      "field": ""
    },
    "title": {
      "field": "title"
    }
  },
  "autocomplete": false,
  "structured_search": false,
  "results_per_page": 0,
  "aggregations": []
}
```
{: codeblock}

**Content Mining**

```json
{
  "fields_shown": {
    "body": {
      "use_passage": false,
      "field": "text"
    },
    "title": {
      "field": "document_id"
    }
  },
  "autocomplete": true,
  "structured_search": false,
  "results_per_page": 0,
  "aggregations": []
}
```
{: codeblock}
