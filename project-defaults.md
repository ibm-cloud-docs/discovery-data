---

copyright:
  years: 2020, 2021
lastupdated: "2021-04-08"

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

| Project type | Default enrichments | Default query result settings | Default CSV settings |
|--------------|---------------------|-------------------------------|----------------------|
| Document Retrieval | Entities, Parts of Speech | Facets (by Entity), Dynamic Facets, Passages | NA |
| Document Retrieval for Contracts | Entities, Parts of speech, Table Understanding, and Contracts | Facets (by Category, Nature, Contract Term, Contract Payment Term, Contract Type, Contract Currency, Invoice Buyer, Invoice supplier, Invoice Currency, Purchase Order Buyer, Purchase Order Supplier, Purchase Order Payment Term) and Table Retrieval | NA |
| Conversational Search | None | Passages | NA |
| Content Mining | Parts of Speech | None | No header, selected delimiters are comma and semicolon |
| Custom | None | Passages | NA |
{: caption="Basic project defaults" caption-side="top"}

NA indicates that a setting is not applicable to the project type.

For more information about default query result settings, see [Default query settings](/docs/discovery-data?topic=discovery-data-query-defaults).