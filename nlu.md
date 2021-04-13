---

copyright:
  years: 2019, 2021
lastupdated: "2021-04-13"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:beta: .beta}
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

# Applying prebuilt enrichments
{: #nlu}

Take advantage of award-winning Watson Natural Language Understanding (NLU) capabilities by adding prebuilt enrichments to your documents.
{: shortdesc}

With Watson NLU, you can identify and tag meaningful information in your collections so you can understand what it all means and make more informed decisions. The following enrichments are available:

- [Entities](#entities): Recognizes proper nouns such as people, cities, and organizations that are mentioned in the content.
- [Keywords](#keywords): Recognizes significant terms in your content.
- [Parts of Speech](#pos): Identifies the parts of speech (nouns and verbs, for example) in the content.
- [Sentiment](#sentiment): Understands the overall sentiment of the content.

Some of the NLU enrichments are applied to projects automatically. You don't need to apply them yourself if you are using one of these project types.

| Enrichment that is applied automatically | Project type |
|------------------------------------------|--------------|
| Entities                                 | Document Retrieval, Document Retrieval with Content Intelligence |
| Parts of Speech                          | Content Mining, Document Retrieval, Document Retrieval with Content Intelligence |
{: caption="Default enrichments for project types" caption-side="top"}

To add an NLU enrichment, complete the following steps: 

1.  Open your project and go to the *Manage collections* page.
1.  Click to open the collection that you want to enrich.
1.  Open the **Enrichments** tab.
1.  Scroll to find the NLU enrichment that you want to apply to your documents. 
1.  Choose one or more fields to apply the enrichment to.

    You can apply the enrichments to fields with a String data type, such as the `text` and `html` fields, or other fields that you add which contain text.

## Entities
{: #entities}

Identifies entities. *Entities* are terms that typically represent proper nouns such as people, cities, and organizations that are mentioned in the data collection. {{site.data.keyword.discoveryshort}} can recognize entities that are part of an entity type system that is defined by the {{site.data.keyword.nlushort}} service.

![Managed deployments only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: For English and Korean data collections, you can choose to use the **Entities v2 trial** enrichment, which applies a newer model with updated entity types. You cannot select both **Entities** and **Entities v2 trial** for a single collection. For more information about each type system, see [Entities Version 1](/docs/natural-language-understanding?topic=natural-language-understanding-entity-types-version-1){: external} and [Entities Version 2](/docs/natural-language-understanding?topic=natural-language-understanding-entity-types-version-2){: external}. (For other languages, the Entities enrichment uses the version 2 type system by default.)
{: note}

For example:

**Input**
text: "IBM is an American multinational technology company headquartered in Armonk."

**Response**

In the JSON output:

  - `text` = string. The entity text
  - `type` = string. The entity type, including but not limited to `Organization`, `Company`, `EmailAddress`, `JobTitle`, `Location`, `Person`, `Quantity`.
  - `mentions` = array. The entity mentions and locations
  - `model_name` = string. For custom models, this field contains the user-provided model name. Otherwise, this field contains the default name of the model: `watson_knowledge_studio`, `dictionary`, `character_pattern`, or `natural_language_understanding`

```Json
 "entities": [
  {
   "model_name": "natural_language_understanding",
   "mentions": [
    {
     "location": {
      "end": 3,
      "begin": 0
     },
     "text": "IBM"
    }
   ],
   "text": "IBM",
   "type": "Company"
  },
  {
   "model_name": "natural_language_understanding",
   "mentions": [
    {
     "location": {
      "end": 75,
      "begin": 69
     },
     "text": "Armonk"
    }
   ],
   "text": "Armonk",
   "type": "Location"
  }
 ]
 ```
 {: codeblock}


## Keywords
{: #keywords}

Returns important keywords in the content.

For example:

**Input**
text: "Watson Discovery is an award-winning AI search technology."

**Response**

In the JSON output:
  - `text` = The keyword text
  - `mentions` = The entity mentions and locations

```Json
 "keywords": [
  {
   "mentions": [
    {
     "location": {
      "end": 157,
      "begin": 141
     },
     "text": "Watson Discovery"
    }
   ],
   "text": "Watson Discovery"
  },
  {
   "mentions": [
    {
     "location": {
      "end": 177,
      "begin": 164
     },
     "text": "award-winning"
    }
   ],
   "text": "award-winning"
  },
  {
   "mentions": [
    {
     "location": {
      "end": 198,
      "begin": 181
     },
     "text": "search technology"
    }
   ],
   "text": "search technology"
  }
 ]
```
{: codeblock}

## Parts of speech
{: #pos}

Recognizes and tags parts of speech, including nouns, verbs, adjectives, adverbs, conjunctions, interjections, and numerals.

## Sentiment
{: #sentiment}

Analyzes the overall sentiment of the document and returns `positive`, `neutral`, or `negative` sentiment.

For example:

**Input**
text: "It is powerful and easy to use and integrate with third party applications."

**Response**

In the JSON output:
  -  `score` = Sentiment score from `-1` (negative) to `1` (positive)
  -  `label` = `positive`, `negative`, or `neutral`
  -  `mixed` = Indicates whether the document has a mix of emotions or not

```Json
 "sentiment": {
   "score": 0.9255063900060722,
   "mixed": false,
   "label": "positive"
 }
 ```
{: codeblock}

You can apply the Sentiment enrichment to content in a Content Mining project type from the deployed Content Mining application. For more information, see [Enabling sentiment analysis](/docs/discovery-data?topic=discovery-data-contentminerapp#sentiment-analysis).
{: note}