---

copyright:
  years: 2019, 2023
lastupdated: "2023-03-08"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Identifying words to ignore
{: #stopwords}

To ignore meaningless terms during searches, add a list of custom stop words. Stop words are words that are not useful in distinguishing the semantic meaning of the content.
{: shortdesc}

In English, `the`, `is` and `and` are examples of stop words.

The stop words that you define are filtered out of queries and improve the relevance of natural language query results.

For example, a company has three tiers of service. The documents in one of the collections pertain to only one tier, the Silver tier. You might want to add `"silver"` to the stop words list because the term doesn't help to distinguish the significance of one document over another, given that all of the documents relate to the Silver service tier. When a customer mentions the Silver tier in a query string, it is ignored. Other terms in the query that are more significant are used to search the data instead. Or maybe the document collection consists of car accident reports only. You might want to add `"car"` to the stop words list to prevent mentions of `car` in queries from adding noise to the search.

{{site.data.keyword.discoveryshort}} applies a list of default stop words for many of the supported languages automatically. These stop words are applied both at indexing time and at query time. The predefined stop words are ignored when content is indexed and they are filtered out of queries. However, stop words that you define are used at query time only. Your list doesn't replace the default list; it augments the default list. You can add stop words, but you cannot remove stop words.

Example custom stop word list:

```json
{
  "stopwords": [
    "a", "an", "the", "ibm", "what", "how", "when", "can", "should", ...
  ]
}
```
{: codeblock}

## Default stop word lists
{: #stopwords-default-lists}

You can access the default stop words list for English from the [Watson Developer Cloud GitHub repository](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_en.json){: external}.

For the following languages, {{site.data.keyword.discoveryshort}} uses the default stop words list that is defined by Apache Lucene. For more information about what words are included in the list, see the Lucene reference documentation:

- Arabic: [stopwords_ar.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/ar/stopwords.txt){: external}
- Czech: [stopwords_cs.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/cz/stopwords.txt){: external}
- Danish: [stopwords_da.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/snowball/danish_stop.txt){: external}
- Dutch: [stopwords_nl.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/snowball/dutch_stop.txt){: external}
- Finnish: [stopwords_fi.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/snowball/finnish_stop.txt){: external}
- French: [stopwords_fr.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/snowball/french_stop.txt){: external}
- German: [stopwords_de.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/snowball/german_stop.txt){: external}
Hindi: [stopwords_hi.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/hi/stopwords.txt){: external}
- Italian: [stopwords_it.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/snowball/italian_stop.txt){: external}
- Norwegian (both supported dialects): [stopwords_no.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/snowball/norwegian_stop.txt){: external}
- Portuguese: [stopwords_pt.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/snowball/portuguese_stop.txt){: external}
- Romanian: [stopwords_ro.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/ro/stopwords.txt){: external}
- Russian: [stopwords_ru.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/snowball/russian_stop.txt){: external}
- Spanish: [stopwords_es.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/snowball/spanish_stop.txt){: external}
- Swedish: [stopwords_sv.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/snowball/swedish_stop.txt){: external}
- Turkish: [stopwords_tr.txt](https://github.com/apache/lucene/blob/main/lucene/analysis/common/src/resources/org/apache/lucene/analysis/tr/stopwords.txt){: external}

These default stop words are documented in TXT format, but if you want to augment the list and submit it for use by {{site.data.keyword.discoveryshort}}, you must submit a JSON file. To see an example of the syntax of stop words list file, see the custom English stop words list file.
{: note}

For the remaining supported languages, no default stop words are used. You can specify a stop words list to use at query time for these languages. The list that you submit is not used when data is ingested.

Examples of stop word lists that you might want to apply at query time include:

- Japanese: [custom_stopwords_ja.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_ja.json){: external}
- Polish: [custom_stopwords_pl.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_pl.json){: external}

See [supported languages](/docs/discovery-data?topic=discovery-data-language-support) for the list of the languages that are supported by {{site.data.keyword.discoveryshort}}.

## Defining query-time stop words
{: #stopwords-task}

To define stop words, complete the following steps:

1.  Create a stop words file. The file must be a JSON file with the `json` file extension.

    Follow these guidelines:

    - Specify stop words in lowercase.
    - In general, keep your list of stop words under `200` total words. The size limit is one million characters. However, if you specify too many terms, you might negatively affect search accuracy.

    You can use the default English stop words list file, [custom_stopwords_en.json](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_en.json){: external}, as a starting point when you build a custom stop word list in English.

1.  From the navigation pane, open the **Improve and customize** page.
1.  Expand **Improve relevance** from the Improvement tools pane.
1.  Click **Stopwords**, and then click **Upload stopwords** for the collection.

    Only one stop words list can be uploaded per collection. The stop words list that you upload augments the default stop words list for your collection; it does not replace the default list.

1.  Click **Done**.

To disable a custom stop words file and revert to using the default stop words, delete the custom stop words file.
