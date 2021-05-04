---

copyright:
  years: 2019, 2021
lastupdated: "2021-05-04"

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


# Search settings
{: #search-settings}

<!-- c/s help for *Search settings* page. Do not delete. -->

You can improve the quality of search results by defining synonyms and stop words.
{: shortdesc}

Add synonyms that you want to apply to the query text that is submitted by users to expand the meaning of the input. 

Synonyms that you add to improve the search results function differently from synonyms that you add to a dictionary. Dictionary synonyms are recognized and tagged at the time that a document is ingested. The synonyms you define are recognized and tagged as occurences of the associated dictionary term, so that they can be retrieved later by search. For more information about adding synonyms that are recognized when documents are processed, see [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain#dictionary).
{: note}

A *stop word* is a sort of helper word, a word that is not significant on its own. In English, “the”, “is” and “and” are examples of stop words. You can label words that commonly occur in your data sources but that have no significant meaning as stop words. When you label them as stop words, you indicate that you want {{site.data.keyword.discoveryshort}} to ignore them.

To define synonyms or stop words, upload a file that lists the synonyms or stop words.

- [Expanding queries with synonyms](#query-expansion)
- [Defining stop words](#stopwords)

## Expanding queries with synonyms
{: #query-expansion}

To expand the scope of a query beyond exact matches, add a synonyms list to your collection. For example, you can expand a query for `ibm` to include `international business machines` and `big blue`. Query expansion terms are usually synonyms, antonyms, or typical misspellings for common terms.

You can define two types of expansions:

- **bidirectional**: Each entry in the `expanded_terms` list expands to include all expanded terms. For example, a query for `ibm` expands to `ibm OR international business machines OR big blue`.

  Bidirectional example:

  ```JSON
  {
    "expansions": [
      {
        "expanded_terms": [
          "ibm",
          "international business machines",
          "big blue"
        ]
      }
    ]
  }
  ```
  {: codeblock}

- **unidirectional**: The `input_terms` in the query is replaced by the `expanded_terms`. For example, a query for `banana` is converted to `plantain OR fruit` and does not contain the original term, `banana`. If you want an input term to be included in the query, then repeat the input term in the expanded terms list.

  Unidirectional example:

  ```JSON
  {
    "expansions": [
      {
        "input_terms": [
          "banana"
         ],
        "expanded_terms": [
          "plantain",
          "fruit"
         ]
       },
       {
        "input_terms": [
           "car"
         ],
        "expanded_terms": [
           "car",
           "automobile"
           "vehicle"
         ]
       }
     ]
   }
  ```
  {: codeblock}

To enable query expansion, complete the following steps:

1.  Create a synonyms list file. The file must be a JSON file with the `json` file extension.

    Follow these guidelines:

    - Specify the `input_terms` and `expanded_terms` in lowercase. Lowercase terms expand to uppercase.
    - Multiword terms are supported only in bidirectional expansions.
    - The synonyms files cannot contain terms that are specified as stopwords. For example, if `on` is included in your stopwords file, and you specify in your synonyms file that `rotfl` expands to `rolling on the floor laughing`, the expansion won't return the expected results. Check the words in the stopwords file that is used by your collection by default to make sure that you don't use any of the same words.
{: important}

    You can use the <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/expansions.json" download>expansions.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> file as a starting point when building a query expansion list.

1.  From the navigation pane, open the **Improve and customize** page. 
1.  Expand **Improve relevance** from the Improvement tools pane.
1.  Click **Synonyms**, and then click **Upload synonyms**.

    Do not upload a synonyms file while documents are being added to your collection. The ingestion processing that occurs when documents are added can cause the index to be unavailable and prevent queries from working properly.

    Only one synonyms list can be uploaded per collection. If a second expansion list is uploaded, the second list replaces the first.

1.  Run a test query to verify that the query expansion is working as expected.

    Query expansions are applied at query time, not during indexing, so you can add synonyms without reprocessing your collection.

To disable query expansion, delete the synonyms file. However, do not delete a synonyms file while new documents are being processed.

## Defining Stopwords
{: #stopwords}

Stop words are words that occur frequently and are therefore not useful in distinguishing the semantic content of one document from another. Stop words are filtered out of queries because they are not useful in searches. For example: `a, an, the`. Defining stop words can improve the relevance of results for natural language queries.

{{site.data.keyword.discoveryshort}} applies a default list of stop words for most supported languages. The specified stop words are removed at both index and query time. You can define and upload a custom list of stop words that overrides the default list. {{site.data.keyword.discoveryshort}} applies the appropriate default or custom stop words list to your collection based on the language specified for that collection.

Example custom stopword list:

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

1.  Create a stop words file.

    Follow these guidelines:

    - Specify stop words in lowercase.
    - Do not remove common terms like `a` and `the` from your custom file or query performance can be reduced.
    - In general, keep your list of stop words under `200` total words. The size limit is one million characters. However, if you specify too many terms, you might negatively affect search accuracy.

    You can use the default English stop words list file, named <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_en.json" download>custom_stopwords_en.json <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> as a starting point when building a custom stop word list in English.

1.  From the navigation pane, open the **Improve and customize** page. 
1.  Expand **Improve relevance** from the Improvement tools pane.
1.  Click **Stopwords**, and then click **Upload stopwords**.

    Do not upload a stop words file while documents are being added to your collection. The ingestion processing that occurs when documents are added can cause the index to be unavailable and prevent queries from working properly.

    Only one stop words list can be uploaded per collection. The stop words list that you upload replaces the default stop words list for your collection language.
1.  Go to the **Activity** page and recrawl or reprocess (whichever option is appropriate for your data source type) your collection so your documents are indexed with the updated list.

To disable a custom stop words file and revert to using the default stop words, delete the custom stop words file. However, do not delete a stop words file while new documents are being processed.
