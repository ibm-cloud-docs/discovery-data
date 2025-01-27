---

copyright:
  years: 2020, 2025
lastupdated: "2023-02-01"

keywords: improving results, troubleshooting search

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Improving your query results
{: #improvements}

Learn about actions you can take to improve the quality of your query results.
{: shortdesc}

You can use the tools that are built in to {{site.data.keyword.discoveryshort}} to make improvements.

## Results include more than exact matches
{: #improve-search-exact-match}

Unlike some other search applications, adding quotation marks to a phrase that you submit does *not* return only exact matches. Queries that are submitted from the product user interface are natural language queries. When quoted text is submitted in a natural language query, the phrase is used to boost result scores. However, results are not limited to documents that contain the entire phrase.

If you want more control over how queries are handled, you must use the query API. For more information about the `phrase` operator of the query API, see [Query operators](/docs/discovery-data?topic=discovery-data-query-operators#phrase).

## A short query returns irrelevant results
{: #improve-all-stopwords}

It might be that your query contains too many stop words and not enough distinct terms to trigger a meaningful search. When you submit a query, the query text is analyzed and optimized before it is submitted to the project. One of the changes that occurs is the removal of any stop words from the text. A *stop word* is a word that is considered to be not useful in distinguishing the semantic meaning of the content. Examples of stop words include terms such as `and`, `the`, and `about`. {{site.data.keyword.discoveryshort}} defines a list of stop words that it ignores automatically both when the data is indexed and when it is searched. When you submit a query that contains mostly or only stop words, such as `About us`, it is equivalent to submitting an empty query.

Although *us* is not included in the stop words list, it is lemmatized to *we*, which is listed as a stop word.
{: note}

You can edit the stop words that are used by your collection. However, you can only augment the stop words list; you cannot remove stop words. And the stop words that you define are used only at query time. They do not affect the stop word list that is used by {{site.data.keyword.discoveryshort}} when data is added to a collection and the index is created.

For more information, see [Identifying words to ignore](/docs/discovery-data?topic=discovery-data-stopwords).

## Results have too much text
{: #improve-too-much-text}

If the source document is large, consider splitting the document into smaller chunks.

To do so, you can create a Smart Document Understanding user-trained model. Find content in the document that can be used to consistently break your document into subsections. For example, maybe your document has chapters or subtitles. You can label the chapters with a custom label named `chapter`. After you teach the model to recognize the `chapter` content type, apply the model to your entire collection. For more information, see [Using Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields).

You can then split the document by the `chapter` field to create many subdocuments segmented by chapter. For more information, see [Split documents to make query results more succinct](/docs/discovery-data?topic=discovery-data-split-documents).

## Information from tables is not found
{: #improve-tables}

The table understanding enrichment must be applied to your collection for information from tables to be searchable. The table understanding enrichment is applied to collections automatically in some situations. If it isn't and your collection has an HTML field in its index, you can apply the *table understanding* enrichment yourself.

For more information, see [Understanding tables](/docs/discovery-data?topic=discovery-data-understanding_tables).

## Information from diagrams is not represented
{: #improve-images}

Text from diagrams and other images is not captured unless you enable the optical character recognition (OCR) setting for the collection. You can apply the setting to a collection after its initial creation. For more information, see [Managing data collections](/docs/discovery-data?topic=discovery-data-manage-collections).

## Search does not recognize significant terms
{: #improve-nlu}

If the results suggest that keywords, common nouns, or domain-specific terms in the query are not being recognized as significant, enrich your collection.

Use Watson Natural Language Understanding to find and tag terms that are generally understood to have special meaning, such as locations or company names. For more information, see [Applying prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu).

Teach {{site.data.keyword.discoveryshort}} about terms and patterns that have special meaning to your use case. For more information, see [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain).

## Default facets aren't useful
{: #improve-facets}

You can add facets that categorize documents based on data from enrichments that you apply to a collection. For example, you might want to show facets based on keywords or dictionary categories. For more information, see [Facets](/docs/discovery-data?topic=discovery-data-facets).

## Explore other search features
{: #improve-other-searches}

When you test your project from the {{site.data.keyword.discoveryshort}} user interface, you submit a natural language query. Search features are available that you can enable to influence how the natural language query search is done. And Discovery Query Language search is another type of search that you can leverage by using the API. If the initial results don't meet your needs, experiment with another search method.

-   Discovery Query Language (DQL) search: A search mechanism that accepts more complex queries. You must use the query API to submit DQL queries.

    For example, you can search for specific values in fields that are generated by enrichments that are applied to a collection.
-   Natural language query is the type of search that is triggered from the *Improve and customize* page. 

For more information about the Query API, see [Query API overview](/docs/discovery-data?topic=discovery-data-query-concepts).
