---

copyright:
  years: 2019
lastupdated: "2019-11-25"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Facets
{: #facets}

To help you analyze the results of linguistic processing and text analysis, {{site.data.keyword.discovery-data_short}} organizes and classifies documents that share similar patterns or content.
{: shortdesc}

## Overview
{: #facetov}

Facets represent the different aspects or dimensions of the documents in your collection. In {{site.data.keyword.discovery-data_short}}, you add facets on the "Improve and customize" page in your project. Facets are available in the "Customize display" section, as shown in Figure 1.

Facets provide a mechanism for navigating and analyzing your content and the exact functionality varies depending on the project type:

- In a content mining project, you select facets to explore content. In real time, you can search across all facets to explore analysis results, relationships, and how different facets of your content change over time.
- In a document retrieval project, you can select facets to filter the search results to find particular documents of interest.
- In a conversational search project, facets aren't applicable, so you don't see the facets option.

!["Customize display" section](images/disccustdisp.png "The customize display section that's available on the "Improve and customize" page in your project"){: caption="Figure 1. The Customize Display section showing the Facets option" caption-side="bottom"}

## Facets in content mining projects
{: #facetcm}

For content mining projects, by default, facets are extracted from your collection for the part of speech enrichment, as shown in Figure 2. You can add facets for fields from your documents. For default project details, see the content mining section of [Creating projects](/docs/services/discovery-data?topic=discovery-data-projects#mining).

For content mining projects, the **Dynamic facets** toggle at the bottom right side of the page is off by default because it does not apply to content mining projects.
{: note}

![Default facets in content mining projects](images/cmdeffacets.png "The "Improve and customize" page showing part of speech facets that are extracted by default"){: caption="Figure 2. The Improve and Customize page of a content mining project showing default extracted facets and no default metadata facets" caption-side="bottom"}

### Adding facets to a content mining project
{: #facetcma}

1. On the "Improve and customize" page, click "Customize display" and then click **Facets**.
1. Click **New facet** > **From existing fields in a collection**, and select a field from your documents that you want to use to filter results.

    As you make your selections, a preview is shown.

1. Optional. Change the default label, filtering options, and number of facet values.
1. To save the facet, click **Apply**.

    The new facet is shown in the list.

## Facets in document retrieval projects
{: #facetdr}

For document retrieval projects, by default, a facet is created for you titled, `Top Entities`, as shown in Figure 3. That facet comes from the `enriched_text.entities.text` field of the entities enrichment. For default project details, see the content mining section of [Creating projects](/docs/services/discovery-data?topic=discovery-data-projects#doc-retrieval).

For document retrieval projects, notice the **Dynamic facets** toggle at the bottom right side of the page, which is on by default. When you have over 100 documents in your collection and the **Part of Speech** enrichment is enabled (as it is by default) this feature creates facets as you test and refine searches. When dynamic facets are generated, you see a facet called **Dynamic Facets** along with **Top Entities** or any other facets you configure.
{: tip}

![Watson Discovery "Customize display" section](images/drdeffacets.png "The "Improve and customize" page showing the default Top Entities facet"){: caption="Figure 3. The Improve and Customize page of a document retrieval project showing the default Top Entities facet" caption-side="bottom"}

### Adding facets to a document retrieval project
{: #facetdra}

1. On the "Improve and customize" page, click "Customize display" and then click **Facets**.
1. Click **New facet** > **From existing fields in a collection**, and select a field from your documents that you want to use to filter results.

    As you make your selections, a preview is shown.

1. Optional. Change the default label, filtering options, and number of facet values.
1. To save the facet, click **Apply**.

    The new facet is shown in the list.

## Creating a facet by creating a dictionary
{: #facetdict}

For either project type, if you want to add a facet that doesn't exist as a field, you can create a dictionary.

1. On the "Improve and customize" page, click **Customize display** and then click **Facets**.
1. Click **New facet** > **By creating a dictionary**.
1. Enter a name for the facet, and then create a dictionary as described in the dictionary enrichments section of [Creating enrichments](/docs/services/discovery-data?topic=discovery-data-dictionary-enrichment#dictionary-enrichment).

    After you save the dictionary, the name that you used for the facet label is shown in the list of facets.

1. As you test the facet, you can add more terms to the dictionary you created by selecting **Teach domain concepts** > **Dictionaries**. The dictionary you created is shown in the list on the "Dictionaries" page.
