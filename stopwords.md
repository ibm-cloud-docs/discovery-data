---

copyright:
  years: 2019, 2021
lastupdated: "2021-05-05"

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

To teach {{site.data.keyword.discoveryshort}} about terms to ignore, add a list of custom stop words. Stop words are words that are not useful in distinguishing the semantic meaning of the content.
{: shortdesc}

In English, `the`, `is` and `and` are examples of stop words.

The stop words you define are applied both at indexing time and at query time. They are ignored when content is indexed and they are filtered out of queries because they are not useful in searches. When you define your own stop words, you can improve the relevance of natural language query results.

{{site.data.keyword.discoveryshort}} applies a list of stop words for most supported languages automatically. You can define and upload a custom list of stop words that overrides the default list.

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

See [supported languages](/docs/discovery-data?topic=discovery-data-language-support) for the list of all languages supported by {{site.data.keyword.discoveryshort}}. Some of the supported languages do not have a default stop words list.

To define stop words, complete the following steps:

1.  Create a stop words file. The file must be a JSON file with the `json` file extension.

    Follow these guidelines:

    - Specify stop words in lowercase.
    - Do not remove common terms like `a` and `the` from your custom file or query performance can be reduced.
    - In general, keep your list of stop words under `200` total words. The size limit is one million characters. However, if you specify too many terms, you might negatively affect search accuracy.

    You can use the default English stop words list file, named <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_en.json" download>custom_stopwords_en.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> as a starting point when you build a custom stop word list in English.

1.  From the navigation pane, open the **Improve and customize** page. 
1.  Expand **Improve relevance** from the Improvement tools pane.
1.  Click **Stopwords**, and then click **Upload stopwords**.

    Do not upload a stop words file while documents are being added to your collection. The ingestion processing that occurs when documents are added can cause the index to be unavailable.

    Only one stop words list can be uploaded per collection. The stop words list that you upload replaces the default stop words list for your collection language.
1.  Go to the **Activity** page and recrawl or reprocess (whichever action is appropriate for your data source type) your collection so that your documents are indexed with the updated list.

To disable a custom stop words file and revert to using the default stop words, delete the custom stop words file. However, do not delete a stop words file while new documents are being processed.
