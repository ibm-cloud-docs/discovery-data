---

copyright:
  years: 2019, 2024
lastupdated: "2023-03-13"

keywords: Watson NLP, entities, keywords, pos, part of speech, sentiment

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Detect sentiment
{: #nlu-sentiment}

Use the built-in Watson Natural Language Processing (NLP) sentiment enrichment to analyze the sentiment that is expressed in text and indicate whether the text is `positive`, `neutral`, or `negative`.
{: shortdesc}

To understand the sentiment of an entire document, apply this enrichment to a field that contains as much of the text from the document as possible, such as the `text` field.

To analyze sentiment in text from multiple fields at one time and capture the overall sentiment of the document, use the Content Mining application. For more information, see [Detecting phrases that express sentiment](/docs/discovery-data?topic=discovery-data-cm-phrase-sentiment).

## Adding the enrichment
{: #nlu-sentiment-task}

To add the sentiment enrichment, complete the following steps:

1.  Open your project and go to the *Manage collections* page.
1.  Click to open the collection that you want to enrich.
1.  Open the **Enrichments** tab.
1.  Scroll to find and select the Sentiment enrichment.
1.  Choose one or more fields to apply the enrichment to.

    You can apply enrichments to the `text` and `html` fields, and to custom fields that were added from uploaded JSON or CSV files or from the Smart Document Understanding (SDU) tool.

1.  Click **Apply changes and reprocess**.

Enrichments that you enable are applied to the documents in random order. For information about how to remove an enrichment, see [Managing enrichments](/docs/discovery-data?topic=discovery-data-manage-enrichments).

## Example
{: #nlu-sentiment-example}

### Input
{: #nlu-sentiment-example-input}

```text
"It is powerful and easy to use and integrate with third party applications."
```
{: codeblock}

### Response
{: #nlu-sentiment-example-response}

In the JSON output:

- `score` = Sentiment score from `-1` (negative) to `1` (positive)
- `label` = `positive`, `negative`, or `neutral`
- `mixed` = Indicates that the document expresses a combination of different sentiments

```json
{
  "sentiment": {
    "score": 0.9255063900060722,
    "mixed": false,
    "label": "positive"
  }
}
 ```
{: codeblock}
