---

copyright:
  years: 2019, 2024
lastupdated: "2022-10-20"

keywords: expansions,synonyms,query expansion

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Expanding the meaning of queries
{: #search-settings}



You can improve the quality of search results by expanding the meaning of the queries that are submitted by customers.
{: shortdesc}

To expand the scope of a query beyond exact matches, add a synonyms list to your collection. When synonyms are defined, the customer does not need to submit an exact phrase or keyword that your project is trained to understand. Even variations of the term are recognized and used to find the best results. For example, you can expand a query for `ibm` to include `international business machines` and `big blue`. Query expansion terms are typically synonyms, antonyms, or common misspellings for terms.

Synonyms that you add to improve the search results function differently from synonyms that you add to a dictionary. Dictionary synonyms are recognized and tagged at the time that a document is ingested. The synonyms that you define are recognized and tagged as occurrences of the associated dictionary term, so that they can be retrieved later by search. For more information about adding synonyms that are recognized when documents are processed, see [Dictionaries](/docs/discovery-data?topic=discovery-data-domain-dictionary).
{: note}

You can define two types of expansions:

Bidirectional
:   Each entry in the `expanded_terms` list expands to include all expanded terms. For example, a query for `ibm` expands to `ibm OR international business machines OR big blue`.

    Bidirectional example:

    ```json
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

Unidirectional
:   The `input_terms` in the query is replaced by the `expanded_terms`. For example, a query for `banana` is converted to `plantain OR fruit` and does not contain the original term, `banana`. If you want an input term to be included in the query, then repeat the input term in the expanded terms list.

    Unidirectional example:

    ```json
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
            "automobile",
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

    -   Specify the `input_terms` and `expanded_terms` in lowercase. Lowercase terms expand to uppercase.
    -   The synonyms files cannot contain terms that are specified as stop words. For example, if `on` is included in your stop words file, and you specify in your synonyms file that `rotfl` expands to `rolling on the floor laughing`, the expansion won't return the expected results. Check the words in the stop words file that is used by your collection by default to make sure that you don't use any of the same words. For more information, see [Identifying words to ignore](/docs/discovery-data?topic=discovery-data-stopwords).

    You can use the [expansions.json](https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/expansions.json){: external} file as a starting point when you build a query expansion list.

1.  From the navigation pane, open the **Improve and customize** page.
1.  Expand **Improve relevance** from the Improvement tools pane.
1.  Click **Synonyms**, and then click **Upload synonyms** for the collection.

    Do not upload a synonyms file while documents are being added to your collection. The ingestion processing that occurs when documents are added can cause the index to be unavailable.

    Only one synonyms list can be uploaded per collection. If a second expansion list is uploaded, the second list replaces the first.

1.  Run a test query to verify that the query expansion is working as expected.

    Query expansions are applied at query time, not during indexing, so you can add synonyms without reprocessing your collection.

To disable query expansion, delete the synonyms file. However, do not delete a synonyms file while new documents are being processed.
