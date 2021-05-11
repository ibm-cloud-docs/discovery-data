---

copyright:
  years: 2019, 2021
lastupdated: "2021-05-10"

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


# Identifying words to ignore
{: #stopwords}

To ignore meaningless terms during searches, add a list of custom stop words. Stop words are words that are not useful in distinguishing the semantic meaning of the content.
{: shortdesc}

In English, `the`, `is` and `and` are examples of stop words.

The stop words you define are filtered out of queries and improves the relevance of natural language query results.

For example, a company has three tiers of service. The documents in one of the collections pertain to only one tier, the Silver tier. You might want to add `"silver"` to the stop words list because the term doesn't help to distinguish the significance of one document over another, given that all of the documents relate to the Silver service tier. When a customer mentions the Silver tier in a query string, it is ignored. Other terms in the query that are more significant are used to search the data instead. Or maybe the document collection consists of car accident reports only. You might want to add `"car"` to the stop words list to prevent mentions of `car` in queries from adding noise to the search.

{{site.data.keyword.discoveryshort}} applies a list of default stop words for most supported languages automatically. These stop words are applied both at indexing time and at query time. The predefined stop words are ignored when content is indexed and they are filtered out of queries. When you upload a custom list of stop words, they override the default list. However, your stop words are used at query time only. 

Example custom stop word list:

```JSON
{"stopwords": ["a", "an", "the", "ibm", "what", "how", "when", "can", "should", ...]}
```

The following files include the default stop words list for different languages:

- Arabic: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_ar.json" download>custom_stopwords_ar.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
- Czech: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_cs.json" download>custom_stopwords_cs.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
- Dutch: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_nl.json" download>custom_stopwords_nl.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
- English: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_en.json" download>custom_stopwords_en.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
- French: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_fr.json" download>custom_stopwords_fr.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
- German: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_de.json" download>custom_stopwords_de.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. 
- Italian: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_it.json" download>custom_stopwords_it.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
- Japanese: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_ja.json" download>custom_stopwords_ja.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
- Polish: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_pl.json" download>custom_stopwords_pl.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
- Portuguese: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_pt.json" download>custom_stopwords_pt.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. 
- Romanian: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_ro.json" download>custom_stopwords_ro.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
- Russian: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_ru.json" download>custom_stopwords_ru.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
- Spanish: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_es.json" download>custom_stopwords_es.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. 

See [supported languages](/docs/discovery-data?topic=discovery-data-language-support) for the list of all languages supported by {{site.data.keyword.discoveryshort}}. Some of the supported languages do not have a predefined stop words list. 

You cannot upload a custom stop words file to serve as the default list for languages that do not have predefined stop words.
{: note}

To define stop words, complete the following steps:

1.  Create a stop words file. The file must be a JSON file with the `json` file extension.

    Follow these guidelines:

    - Specify stop words in lowercase.
    - Do not remove common terms like `a` and `the` from your custom file or query performance can be reduced.
    - In general, keep your list of stop words under `200` total words. The size limit is one million characters. However, if you specify too many terms, you might negatively affect search accuracy.

    You can use the default English stop words list file, named <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_en.json" download>custom_stopwords_en.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> as a starting point when you build a custom stop word list in English.

1.  From the navigation pane, open the **Improve and customize** page. 
1.  Expand **Improve relevance** from the Improvement tools pane.
1.  Click **Stopwords**.

    Do not update the stopwords file while new documents are being processed. The index is closed while the stop words are updated, which can cause ingestion to fail.
    {: note}

1.  Click **Upload stopwords**.

    Only one stop words list can be uploaded per collection. The stop words list that you upload replaces the default stop words list for your collection.
1.  Click **Done**.

To disable a custom stop words file and revert to using the default stop words, delete the custom stop words file. Do not delete the stopwords file while new documents are being processed.