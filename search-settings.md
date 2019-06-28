---

copyright:
  years: 2019
lastupdated: "2019-06-21"

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


# Search settings
{: #search-settings}

<!-- Help for Search settings screen -->

You can improve the quality of search results by using the **Search settings** screen to upload a **Synonyms** file (to enable query expansions) as well as a **Stopwords** file.
{: shortdesc}

In addition, you can use the API to enable autocomplete, see the
[Autocomplete](https://{DomainName}/apidocs/discovery-data#get-autocomplete-suggestions){: external} method. 

To access the **Search settings** screen, [create a new collection (or open an existing one)](/docs/services/discovery-data?topic=discovery-data-collections#collections), and click the **Search settings** tab. 
 
Upload or delete a synonyms or stopwords file by clicking the appropriate **Upload** button or **Delete** icon.

If you make significant changes to your synonyms or stopwords files, you should go to the **Overview** screen and click the **Reprocess collection** button so that your documents are indexed with the updated lists.

Stopwords and synonyms files cannot contain overlapping terms. If a [stopword](/docs/services/discovery-data?topic=discovery-data-stopwords#stopwords) in your stopwords file is also included within your synonyms ([query expansion](/docs/services/discovery-data?topic=discovery-data-query-expansion#query-expansion)) file, the query expansion will not work. For example, if `on` is included in your stopwords file, and you specify in your synonyms file that `rotfl` should expand to `rolling on the floor laughing`, that expansion will not return the expected results. A stopwords file is enabled by default in each collection (file name: `custom_stopwords_[language].json`) in {{site.data.keyword.discovery-data_short}}, so you should compare the words in that file to your synonyms (query expansion) file and adjust accordingly. 
{: important}

## Implementing query expansion
{: #query-expansion}

You can expand the scope of a query beyond exact matches - for example, you can expand a query for "ibm" to include "international business machines" and "big blue" - by uploading a list of query expansion terms. Query expansion terms are usually synonyms, antonyms, or typical misspellings for common terms.
{: shortdesc}

The synonyms (query expansion) file must be a JSON file and must have the file extension of `json`.

You can define two types of expansions:
-  **bidirectional** - each `expanded_term` will expand to include all expanded terms. For example, a query for `ibm` would expand to `ibm OR international business machines OR big blue`). 
-  **unidirectional** - the `input_terms` in the query will be replaced by the `expanded_terms`. For example, a query for `banana` could expand to `plantain` and `fruit`. `input_terms` are not used as part of the resulting query. In the previous `banana` example, the query `banana` would be converted to `plantain` OR `fruit` and not contain the original term.

Multi-word terms are supported only for bidirectional expansions.
{: note}

This file can be used as a starting point when building a query expansion list:
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/expansions.json" download>expansions.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. You can modify this file to create a custom query expansion list.

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

Unidirectional example:
```JSON
 {
   "expansions": [
     {
      "input_terms": [
         "car"
       ],
      "expanded_terms": [
         "car",
         "automobile"
         "vehicle"
       ]
     },
     {
      "input_terms": [
        "banana"
       ],
      "expanded_terms": [
        "banana",
        "plantain",
        "fruit"
       ]
     }
   ]
 }
```
{: codeblock}

Notes about query expansion:

-  Only one synonyms (query expansion) list can be uploaded per collection; if a second expansion list is uploaded, it will replace the first.
-  All `input_terms` and `expanded_terms` should be lowercase. Lowercase terms will expand to uppercase.
-  The query expansion list must be written in JSON.
-  To disable query expansion, delete the synonyms (query expansion) file.
-  Query expansion is performed on the `query` method.
-  Each set of expansions is associated with a single collection. 
-  Query expansions are applied at query time, not during indexing, so the synonyms (query expansion) file can be updated without the need to reprocess your collection.
-  Do not upload or delete a synonyms (query expansion) file at the same time documents are being ingested into your collection. This could cause the index to be unavailable for that brief period and queries will fail.

## Defining Stopwords
{: #stopwords}

Stopwords are words that are filtered out of queries because they are common terms that are not useful in a search, for example: `a, an, the`. Adding common words to a stopwords file can also improve the relevance of results for natural language queries.
{: shortdesc}

 {{site.data.keyword.discovery-data_short}} applies a default stopwords file for several languages at query time. However, you can define and upload a custom stopwords file that will override the default file. {{site.data.keyword.discovery-data_short}} will apply the appropriate default or custom stopwords file to your collection based on the language specified for that collection. 

Example custom stopword list:

```JSON
{"stopwords": ["a", "an," "the", "ibm", "what", "how", "when", "can", "should", ...]}
```

This file contains all the default English stopwords <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_en.json" download>custom_stopwords_en.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. It can be used as a starting point when building a custom stopword file in English. Creating a custom stopword file that does not include very common terms like `a` and `the` can lead to reduced query performance, so it is recommended that you keep these words in your custom stopword file. 

Following are stopword files for several other supported languages. They all include the default stopwords for that language:

-  Dutch: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_nl.json" download>custom_stopwords_nl.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
-  French: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_fr.json" download>custom_stopwords_fr.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
-  German: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_de.json" download>custom_stopwords_de.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. 
-  Italian: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_it.json" download>custom_stopwords_it.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
-  Japanese: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_ja.json" download>custom_stopwords_ja.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
-  Spanish: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_es.json" download>custom_stopwords_es.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. 
-  Portuguese: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_pt.json" download>custom_stopwords_pt.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. 
-  Arabic: <a target="_blank" href="https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/custom_stopwords_ar.json" download>custom_stopwords_ar.json <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. 

See [supported languages](/docs/services/discovery-data?topic=discovery-data-language-support#supported-languages) for the list of all languages supported by {{site.data.keyword.discovery-data_short}} . Several supported languages do not have a default stopwords list.

Notes about stopwords:

-  Only one custom stopwords file can be uploaded per collection; if a second custom stopwords file is uploaded, it will replace the first.
-  The size limit for a custom stopword list file is one million characters. However, if you upload a custom stopwords file with a large number of terms, you may negatively affect search accuracy. The number of words is dependent on the language, the document contents, and the words chosen. A good best practice would be to keep your list of stopwords under `200` total words. 
-  All stopwords should be lowercase. 
-  To disable a custom stopword file, delete the custom stopword file.
-  Do not upload or delete a custom stopword file at the same time documents are being ingested into your collection. This could cause the index to be unavailable for that brief period and queries will fail.
-  Stopwords are removed at both index and query time. A good best practice is to upload your custom stopword file before crawling/uploading all of your documents.
   - If your documents have already been indexed with the default stopwords file, and you then add a custom stopwords file, the new custom stopwords will remain in the index for those documents. In that case, queries containing the new stopwords will filter them out at query time.
   - If a user searches for a word that was a stopword at one point in time, but has since been removed from the custom stopwords file, they will not find documents that match the original stopword because the term was removed at index time. To fix this issue, go to the **Overview** screen and click **Reprocess collection** so that your documents are indexed with the updated custom stopwords file.

