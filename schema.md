---

copyright:
  years: 2018, 2020
lastupdated: "2020-03-31"


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

# Using Discovery for Content Intelligence
{: #output_schema}

The Discovery for Content Intelligence enrichments (`Contracts`, `Invoices`, and `Purchase orders`) are available only if you purchase and install Discovery for Content Intelligence and choose the **Project type** of **Document retrieval**.
{: note}

Discovery for Content Intelligence enables understanding of governing business documents with pre-trained models so enterprises can start analyzing complex documents in minutes. The `Contracts`, `Invoices`, and `Purchase Orders` enrichments enable automation of complex business processes, such as contract review and negotiation, invoice reconciliation, software entitlement verification, and more. Such automation of processes result in increased productivity, minimization of costs, and reduced exposure.
{: shortdesc}

Discovery for Content Intelligence includes pre-trained models that identify lists, sections, tables, headers, footers, and other structures in your documents. These models cannot be modified, so you cannot annotate fields with [Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields) to train custom conversion models when using Discovery for Content Intelligence enrichments.

## Getting started
{: #content-intelligence-gs}

To use Discovery for Content Intelligence, start by creating a document retrieval project. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).

Discovery for Content Intelligence only works on collections that contain documents in English. A Discovery for Content Intelligence project has the following default settings:
  
- The setting **Optical Character Reader Advanced** is set to `on`.
- The enrichments applied include `Entities`, `Parts of speech`, `Table Understanding`, and `Contracts`.
- The improvement tools enabled include Facets (by Category, Nature, Contract Term, Contract Payment Term, Contract Type, Contract Currency, Invoice Buyer, Invoice supplier, Invoice Currency, Purchase Order Buyer, Purchase Order Supplier, Purchase Order Payment Term) and Table Retrieval.


## Understanding Discovery for Content Intelligence enrichments
{: #understand-ci-enrichments}

Discovery for Content Intelligence provides a set of analysis models that are pre-trained for use with the following business documents:

- Contracts
- Invoices
- Purchase orders

For information about each Discovery for Content Intelligence enrichment, see the following sections:

  - [Understanding the Contracts enrichment](/docs/discovery-data?topic=discovery-data-contracts-schema)
  - [Understanding the Invoices enrichment](/docs/discovery-data?topic=discovery-data-invoices)
  - [Understanding the Purchase orders enrichment](/docs/discovery-data?topic=discovery-data-purchase_orders)


### Changing the default enrichment
{: #changing-enrichment}

Unless you specify the `Invoices` or `Purchase orders` enrichment, Discovery for Content Intelligence processes all collections with the `Contracts` enrichment.
{: shortdesc}

To specify a different enrichment other than `Contracts`, complete the following steps:

1. After you create a collection in the {{site.data.keyword.discovery-data_short}} tooling, select it on the **Projects** page.
1. On the **Improve and customize** page, select **I want to...** **=>** **Extract meaning**.
1. Select **Entities**.
1. On the **Available enrichments** page, unselect **Contracts**, and select either **Invoices** or **Purchase Orders**. Only one of **Contracts**, **Invoices**, and **Purchase Orders** can be applied to a given collection.
1. Click **Apply changes and reprocess**.
