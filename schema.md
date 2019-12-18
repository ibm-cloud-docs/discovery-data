---

copyright:
  years: 2018, 2019
lastupdated: "2019-12-02"

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
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Understanding Discovery for Content Intelligence
{: #output_schema}

Discovery for Content Intelligence enables understanding of governing business documents with pre-trained models so enterprises can start analyzing complex documents in minutes. The `Contracts`, `Invoices`, and `Purchase Orders` enrichments enable automation of complex business processes such as contract review and negotiation, invoice reconciliation, software entitlement verification, and more. Such automation of processes result in increased productivity, minimization of costs, and reduced exposure.
{: shortdesc}

<!-- V Nov -->

The Discovery for Content Intelligence enrichments (`Contracts`, `Invoices`, and `Purchase orders`) are available only if you have purchased and installed Discovery for Content Intelligence and chosen the **Project type** of **Document retrieval**.
{: note}

<!-- Needs to be updated; check for duplicate anchors; check links-->

## Understanding Discovery for Content Intelligence enrichments
{: #understand-ci-enrichments}

Discovery for Content Intelligence provides a set of analysis models that are pre-trained for use with different types of governing business documents: contracts, invoices, and purchase orders.

For information about the Discovery for Content Intelligence enrichments, see:
  - [Understanding the `Contracts` enrichment](/docs/discovery-data?topic=discovery-data-contracts-schema)
  - [Understanding the `Invoices` enrichment](/docs/discovery-data?topic=discovery-data-invoices)
  - [Understanding the `Purchase orders` enrichment](/docs/discovery-data?topic=discovery-data-purchase_orders)

### Discovery for Content Intelligence notes
{: #ci-notes}

Note the following when using Discovery for Content Intelligence:

  - Discovery for Content Intelligence works only on collections that contain documents in English only.
  - **Document Retrieval** is the only project type available on a {{site.data.keyword.discovery-data_short}} instance on which Discovery for Content Intelligence is installed.
  - Discovery for Content Intelligence project defaults include the following:
    - The setting **Optical Character Reader Advanced** is set to `on`.
    - The enrichments applied include `Entities`, `Parts of speech`, `Table Understanding`, and `Contracts`.
    - The improvement tools enabled include Facets (by Category, Nature, Contract Term, Contract Payment Term, Contract Type, Contract Currency, Invoice Buyer, Invoice supplier, Invoice Currency, Purchase Order Buyer, Purchase Order Supplier, Purchase Order Payment Term) and Table Retrieval.
  - Discovery for Content Intelligence processes all collections with the `Contracts` enrichment unless otherwise specified. You can specify a different enrichment as follows:
    1. After you have created a collection in the {{site.data.keyword.discovery-data_short}} tooling, select it on the **Projects** page.
    1. On the **Improve and customize** page, select **I want to...** **=>** **Extract meaning**.
    1. Select **Entities**.
    1. On the **Available enrichments** page, unselect **Contracts** and select either **Invoices** or **Purchase Orders**. Only one of **Contracts**, **Invoices**, and **Purchase Orders** can be applied to a given collection.
    1. Click **Apply changes and reprocess**.
    1. Perform other steps normally.


