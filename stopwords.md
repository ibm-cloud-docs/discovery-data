---

copyright:
  years: 2019, 2021
lastupdated: "2021-10-02"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Identifying words to ignore
{: #stopwords}

To ignore meaningless terms during searches, add a list of custom stop words. Stop words are words that are not useful in distinguishing the semantic meaning of the content.
{: shortdesc}

In English, `the`, `is` and `and` are examples of stop words.

The stop words you define are filtered out of queries and improves the relevance of natural language query results.

For example, a company has three tiers of service. The documents in one of the collections pertain to only one tier, the Silver tier. You might want to add `"silver"` to the stop words list because the term doesn't help to distinguish the significance of one document over another, given that all of the documents relate to the Silver service tier. When a customer mentions the Silver tier in a query string, it is ignored. Other terms in the query that are more significant are used to search the data instead. Or maybe the document collection consists of car accident reports only. You might want to add `"car"` to the stop words list to prevent mentions of `car` in queries from adding noise to the search.

{{site.data.keyword.discoveryshort}} applies a list of default stop words for most supported languages automatically. These stop words are applied both at indexing time and at query time. The predefined stop words are ignored when content is indexed and they are filtered out of queries. When you upload a custom list of stop words, they override the default list. However, your stop words are used at query time only.

Example custom stop word list:

```json
{
  "stopwords": [
    "a", "an", "the", "ibm", "what", "how", "when", "can", "should", ...
  ]
}
```
{: codeblock}

The following files include the default stop words list for different languages:

- Arabic: [custom_stopwords_ar.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_ar.json){: external}
- Czech: [custom_stopwords_cs.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_cs.json){: external}
- Dutch: [custom_stopwords_nl.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_nl.json){: external}
- English: [custom_stopwords_en.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_en.json){: external}
- French: [custom_stopwords_fr.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_fr.json){: external}
- German: [custom_stopwords_de.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_de.json){: external}
- Italian: [custom_stopwords_it.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_it.json){: external}
- Japanese: [custom_stopwords_ja.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_ja.json){: external}
- Polish: [custom_stopwords_pl.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_pl.json){: external}
- Portuguese: [custom_stopwords_pt.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_pt.json){: external}
- Romanian: [custom_stopwords_ro.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_ro.json){: external}
- Russian: [custom_stopwords_ru.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_ru.json){: external}
- Spanish: [custom_stopwords_es.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_es.json){: external}

See [supported languages](/docs/discovery-data?topic=discovery-data-language-support) for the list of all languages supported by {{site.data.keyword.discoveryshort}}. Some of the supported languages do not have a predefined stop words list.

You cannot upload a custom stop words file to serve as the default list for languages that do not have predefined stop words.
{: note}

To define stop words, complete the following steps:

1.  Create a stop words file. The file must be a JSON file with the `json` file extension.

    Follow these guidelines:

    - Specify stop words in lowercase.
    - Do not remove common terms like `a` and `the` from your custom file or query performance can be reduced.
    - In general, keep your list of stop words under `200` total words. The size limit is one million characters. However, if you specify too many terms, you might negatively affect search accuracy.

    You can use the default English stop words list file, [custom_stopwords_en.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_en.json){: external}, as a starting point when you build a custom stop word list in English.

1.  From the navigation pane, open the **Improve and customize** page.
1.  Expand **Improve relevance** from the Improvement tools pane.
1.  Click **Stopwords**, and then click **Upload stopwords**.

    Only one stop words list can be uploaded per collection. The stop words list that you upload replaces the default stop words list for your collection.
1.  Click **Done**.

To disable a custom stop words file and revert to using the default stop words, delete the custom stop words file.