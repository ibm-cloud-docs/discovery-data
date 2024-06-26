---

copyright:
  years: 2020, 2023
lastupdated: "2022-08-01"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Default project settings
{: #project-defaults}

Learn about the enrichments and query result settings that are applied to each project type by default.
{: shortdesc}

To learn more about project types, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).

## Basic project defaults
{: #basic-defaults}

| Project type | Default enrichments | Default query result settings |
|--------------|---------------------|-------------------------------|
| Document Retrieval | Entities, Part of Speech | Facets (by Entity), Passages |
| Document Retrieval for Contracts | Entities, Parts of speech, Table Understanding, and Contracts | Facets (by Category, Nature, Contract Term, Contract Payment Term, Contract Type, Contract Currency, Invoice Buyer, Invoice supplier, Invoice Currency, Purchase Order Buyer, Purchase Order Supplier, Purchase Order Payment Term) and Table Retrieval |
| Conversational Search | None | Passages |
| Content Mining | Part of Speech | None |
| Custom | None | Passages |
{: caption="Basic project defaults" caption-side="top"}

When you enter a query from the product user interface, a natural language query is submitted. The default values for the supported query parameters differ by project type. For more information, see [Default query settings](/docs/discovery-data?topic=discovery-data-query-defaults).