---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-09"

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

Learn about the enrichments and query result settings that are applied to each project type by default.
{: shortdesc}

To learn more about project types, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).

## Basic project defaults
{: #basic-defaults}

| Project type | Default enrichments | Default query result settings |
|--------------|---------------------|-------------------------------|
| Document Retrieval | Entities, Parts of Speech | Facets (by Entity), Passages, Dynamic Facets (Premium plans only) |
| Document Retrieval for Contracts | Entities, Parts of speech, Table Understanding, and Contracts | Facets (by Category, Nature, Contract Term, Contract Payment Term, Contract Type, Contract Currency, Invoice Buyer, Invoice supplier, Invoice Currency, Purchase Order Buyer, Purchase Order Supplier, Purchase Order Payment Term) and Table Retrieval |
| Conversational Search | None | Passages |
| Content Mining | Parts of Speech | None |
| Custom | None | Passages |
{: caption="Basic project defaults" caption-side="top"}
