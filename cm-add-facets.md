---

copyright:
  years: 2015, 2022
lastupdated: "2022-07-22"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Adding facets
{: #cm-add-facets}

Add more facets that you can use to filter your data.
{: shortdesc}

When you apply custom enrichments to your collection, annotations are added to its documents. The annotations feed into new facets that you can use to sort your data.

The following table describes the types of facets that you can create from annotations.

| Information to recognize | Annotator type |
|--------------------------|----------------|
| Commonly understood terms, such as organization or people names. | [Built-in Natural Language Processing models](/docs/discovery-data?topic=discovery-data-cm-edit-collection#cm-enrichments) |
| Phrases that express an opinion and evaluate whether the opinion is positive or negative. | [Phrase sentiment](/docs/discovery-data?topic=discovery-data-cm-phrase-sentiment) |
| Alternative words that share a meaning with terms in a finite list | [Dictionary](/docs/discovery-data?topic=discovery-data-cm-custom-annotator) |
| Terms that match a syntactical pattern | [Regular expression](/docs/discovery-data?topic=discovery-data-cm-custom-annotator) |
| Custom terms based on the context in which they’re used | [Machine learning model](/docs/discovery-data?topic=discovery-data-cm-custom-annotator) |
| Documents that fit into categories that you define | [Document classifier](/docs/discovery-data?topic=discovery-data-cm-doc-classifier) |
{: caption="Types of custom facets" caption-side="top"}
