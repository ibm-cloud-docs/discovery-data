---

copyright:
  years: 2018, 2021
lastupdated: "2021-03-12"


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

{{site.data.keyword.discoveryshort}} for Content Intelligence enables understanding of governing business documents with pre-trained models so enterprises can start analyzing complex documents in minutes. You can use the enrichments to automate complex business processes, such as contract review and negotiation and more. Such process automation results in increased productivity, minimization of costs, and reduced exposure.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: You must first install {{site.data.keyword.discoveryshort}} for Content Intelligence before you can access the `Contracts` enrichment.

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: In {{site.data.keyword.cloud_notm}} Premium plans and in {{site.data.keyword.discoveryfull}}, the {{site.data.keyword.discoveryshort}} for Content Intelligence `Contracts` enrichment is available if you choose the **Project type** of **Document retrieval** and then select the **Apply contracts enrichment** checkbox.

{{site.data.keyword.discoveryshort}} for Content Intelligence includes pre-trained models that identify lists, sections, tables, headers, footers, and other structures in your documents. These models cannot be modified, so you cannot annotate fields with [Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields) to train custom conversion models when using {{site.data.keyword.discoveryshort}} for Content Intelligence. The [Table understanding](/docs/discovery-data?topic=discovery-data-understanding_tables) enrichment is automatically applied.

Discovery for Content Intelligence supports English language documents only. By default, pre-trained models are used during document conversion.
{: important}

## Getting started
{: #content-intelligence-gs}

To use {{site.data.keyword.discoveryshort}} for Content Intelligence, start by creating a **Document Retrieval** project. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).

In {{site.data.keyword.cloud_notm}} Premium plans and in {{site.data.keyword.discoveryfull}}, {{site.data.keyword.discoveryshort}} for Content Intelligence defaults, including the `Contracts` enrichment, are automatically applied to your **Document retrieval** project when you choose the **Project type** of **Document retrieval** and then select the **Apply contracts enrichment** checkbox.

A Discovery for Content Intelligence project has the following default settings:
  
- **Settings**: Optical Character Reader Advanced `on`
- **Enrichments applied**: Entities, Parts of speech, Table Understanding, and Contracts
- **Improvement tools enabled**: Facets (by Category, Nature, Contract Term, Contract Payment Term, Contract Type, Contract Currency) and Table Retrieval

For additional default settings, see [Default project settings](/docs/discovery-data?topic=discovery-data-project-defaults). {{site.data.keyword.discoveryshort}} for Content Intelligence provides a set of analysis models that are pre-trained for use with **Contracts**. For more information, see [Understanding the Contracts enrichment](/docs/discovery-data?topic=discovery-data-contracts-schema).
