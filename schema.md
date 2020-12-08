---

copyright:
  years: 2018, 2020
lastupdated: "2020-12-04"


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

![Cloud Pak for Data only](images/cpdonly.png) The {{site.data.keyword.discoveryshort}} for Content Intelligence enrichments (`Contracts`, `Invoices`, and `Purchase orders`) are available only if you install {{site.data.keyword.discoveryshort}} for Content Intelligence and choose the **Project type** of **Document retrieval**.

![IBM Cloud only](images/cloudonly.png) On {{site.data.keyword.cloud_notm}} Premium plans, the {{site.data.keyword.discoveryshort}} for Content Intelligence `Contracts` enrichment is available if you choose the **Project type** of **Document retrieval**, then select the **Apply contracts enrichment** checkbox.

{{site.data.keyword.discoveryshort}} for Content Intelligence enables understanding of governing business documents with pre-trained models so enterprises can start analyzing complex documents in minutes. The enrichments enable automation of complex business processes, such as contract review and negotiation, and more. Such automation of processes result in increased productivity, minimization of costs, and reduced exposure.
{: shortdesc}

{{site.data.keyword.discoveryshort}} for Content Intelligence includes pre-trained models that identify lists, sections, tables, headers, footers, and other structures in your documents. These models cannot be modified, so you cannot annotate fields with [Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields) to train custom conversion models when using {{site.data.keyword.discoveryshort}} for Content Intelligence. The [Table understanding](/docs/discovery-data?topic=discovery-data-understanding_tables) enrichment is automatically applied.

Discovery for Content Intelligence supports English language documents only. The pre-trained models cannot be modified.
{: important}

## Getting started
{: #content-intelligence-gs}

To use {{site.data.keyword.discoveryshort}} for Content Intelligence, start by creating a **Document Retrieval** project. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).

![Cloud Pak for Data only](images/cpdonly.png) The `Contracts` enrichment and all {{site.data.keyword.discoveryshort}} for Content Intelligence defaults will be automatically applied to your **Document retrieval** project.

![IBM Cloud only](images/cloudonly.png) On {{site.data.keyword.cloud_notm}} Premium plans, {{site.data.keyword.discoveryshort}} for Content Intelligence is enabled when you choose the **Project type** of **Document retrieval**, then select the **Apply contracts enrichment** checkbox.

A Discovery for Content Intelligence project has the following default settings:
  
- **Settings**: Optical Character Reader Advanced `on`
- **Enrichments applied**: Entities, Parts of speech, Table Understanding, and Contracts
- **Improvement tools enabled**: Facets (by Category, Nature, Contract Term, Contract Payment Term, Contract Type, Contract Currency, Invoice Buyer, Invoice supplier, Invoice Currency, Purchase Order Buyer, Purchase Order Supplier, Purchase Order Payment Term) and Table Retrieval

For additional default settings, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults).

## Understanding Discovery for Content Intelligence enrichments
{: #understand-ci-enrichments}

{{site.data.keyword.discoveryshort}} for Content Intelligence provides a set of analysis models that are pre-trained for use with the following business documents:

- **Contracts** For more information, see [Understanding the Contracts enrichment](/docs/discovery-data?topic=discovery-data-contracts-schema)
- ![Cloud Pak for Data only](images/cpdonly.png) **Invoices** For more information, see [Understanding the Invoices enrichment](/docs/discovery-data?topic=discovery-data-invoices)
- ![Cloud Pak for Data only](images/cpdonly.png) **Purchase orders** For more imformation, see [Understanding the Purchase orders enrichment](/docs/discovery-data?topic=discovery-data-purchase_orders).


### Changing the default enrichment
{: #changing-enrichment}

![Cloud Pak for Data only](images/cpdonly.png)</br>

Unless you specify the `Invoices` or `Purchase orders` enrichment, {{site.data.keyword.discoveryshort}} for Content Intelligence processes all collections with the `Contracts` enrichment. The [Invoices](/docs/discovery-data?topic=discovery-data-invoices) and [Purchase Orders](/docs/discovery-data?topic=discovery-data-purchase_orders) enrichments enable automation of complex business processes, such as invoice reconciliation, software entitlement verification, and more. 
{: shortdesc}

To specify the `Invoices` or `Purchase orders` enrichment, complete the following steps:

1. After you create a collection in the {{site.data.keyword.discoveryshort}} tooling, select it on the **Projects** page.
1. On the **Improve and customize** page, select **I want to...** **=>** **Extract meaning**.
1. Select **Entities**.
1. On the **Available enrichments** page, unselect **Contracts**, and select either **Invoices** or **Purchase Orders**. Only one of **Contracts**, **Invoices**, and **Purchase Orders** can be applied to a given collection.
1. Click **Apply changes and reprocess**.
