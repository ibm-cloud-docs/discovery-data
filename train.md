---

copyright:
  years: 2019, 2021
lastupdated: "2021-10-02"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Improving result relevance with training
{: #train}

<!-- c/s help for the *Train* page. Do not delete.  -->

The relevance of natural language query results can be improved in {{site.data.keyword.discoveryfull}} with training.
{: shortdesc}

Relevancy training is optional; if the results of your queries meet your needs, no further training is necessary. For more information about when to use relevancy training, read the [Relevancy training for time-sensitive users](https://medium.com/ibm-data-ai/ibm-watson-discovery-relevancy-training-time-sensitive-18a190b0874a){: external} blog post on Medium.

This video demonstrates relevancy training and several other features. For more information on those features, see [Expanding the meaning of queries](/docs/discovery-data?topic=discovery-data-search-settings), [Identifying words to ignore](/docs/discovery-data?topic=discovery-data-stopwords), and [Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields):

![Demo: Watson Discovery Improving Result Relevancy](https://www.youtube.com/embed/wi_V9s8XF3c){: video output="iframe" data-script="none"  id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

-   To view the transcript, open the video on YouTube.
-   To access the **Train** page, open your project and select the **Improve and customize** icon on the navigation panel. On the **Improvement tools** panel, select **Improve relevance**, then **Relevancy training**.

To train {{site.data.keyword.ibmwatson}}, you'll need to:

-   Identify natural language queries that are representative of the queries your users would request.
-   Rate the results of each query as `relevant` or `not relevant`.

After Watson has enough training input, the information that you provided about result relevance for each query is used to learn about your project. Watson does not memorize; it learns from the specific information about individual queries and applies the patterns it has detected to new queries. It uses machine learning Watson techniques to find signals in your content and questions. After training is applied, {{site.data.keyword.discoveryshort}} then reorders the query results to display the most relevant results first. As you add more and more training data, {{site.data.keyword.discoveryshort}} learns how best to order your query results.

Natural language query results return a `confidence` score. For more information, see [Confidence scores](/docs/discovery-data?topic=discovery-data-train#confidence).

Adding a custom stopwords list can also improve the relevance of results for natural language queries. For more information, see [Identifying words to ignore](/docs/discovery-data?topic=discovery-data-stopwords).
{: tip}

If you would prefer to use the {{site.data.keyword.discoveryshort}} API to train {{site.data.keyword.discoveryshort}}, see the [API reference](https://{DomainName}/apidocs/discovery-data#listtrainingqueries){: external}.

You also can use the API to add curations. Curations is a beta feature that you can use to teach {{site.data.keyword.discoveryshort}} to return a specific document every time a certain query is submitted. For more information, see [Curations](/docs/discovery-data?topic=discovery-data-curations).

## Adding queries and rating results
{: #results}

Training consists of three parts:

- A natural language query
- The results of that query
- The rating you apply to each result

To train a project:

1.  On the *Train* page, enter a natural language query in the **Enter a question to train** field. Do not include a question mark in your query. Click the **Add+** button.
1.  Click **Rate results**.
1.  After the results are displayed, select **Relevant** or **Not relevant**.

    Select an option for each result.

    When you select **Relevant**, you apply a score of `10` to the result. **Not relevant** applies a score of `0`. You can use a different scoring scale if you use the API to rate results, but you can't mix scoring scales within the same project.
1.  When you are finished, click **Back to queries**.
1.  Continue adding queries and rating them.

    As you rate results, your progress is shown. Check your progress to see when you have done enough work to meet the training threshold needs. Your progress is broken into the following tasks:

    - Add more queries
    - Rate more results
    - Add more variety to your ratings

    You must evaluate at least 50 unique queries, maybe more depending on the complexity of your data.
1.  You can continue adding queries and rating results after you have reached the threshold. You should enter all queries you think your users will ask.
1.  To delete a trainig query, click the **Delete** icon.

    To delete all of the training queries in your collection at one time, use the API. For more information, see [Delete training queries](https://{DomainName}/apidocs/discovery-data#deletetrainingqueries){: external}.

Write your training queries with the same wording that your users would ask them, for example: `IBM Watson in healthcare`. Training queries should be written with some term overlap between the query and the desired answer; this will improve initial results when the natural language query is evaluated.
{: tip}

If two or more users attempt to train identical queries at the same time, one of the users will overwrite the others.
{: note}

## Testing and iterating on the relevancy of results
{: #testing-results}

When you are done rating results, and Watson has applied the training, test to see if your query results have improved. To do so, run test natural language queries that are related (but not identical) to your training queries. Check to see if the results of your test queries have improved.

If you would like to further improve results after testing, you can:

- Add more documents to your collection.
- Add more training queries.
- Rate more results, making sure to use both the `Relevant` and `Not relevant` ratings.

## Confidence scores
{: #confidence}

{{site.data.keyword.discoveryshort}} returns a `confidence` score for natural language queries of trained collections. This `confidence` score is not interchangeble with `confidence` scores returned by untrained collections.

The `confidence` score can range from `0.0` to `1.0`. The higher the number, the more relevant the result.

The `confidence` score can be found in the query results, under the `result_metadata` for each document. This number is calculated based on how relevant the result is estimated to be, compared to the trained model.

```JSON
{
  "matching_results": 4,
  "retrieval_details": {
    "document_retrieval_strategy": "trained"
  },
  "results": [
    {
	  "id": "eea16dfd5fe6139a25324e7481a32f89_13",
	  "result_metadata": {
	    "confidence": 0.08793
	  }
    }
  ]
}
```
{: codeblock}

The `document_retrieval_strategy` can be found under the `retrieval_details`. If you query a trained collection using the {{site.data.keyword.discoveryshort}} Query Language, or the trained model is temporarily unavailable, the `document_retrieval_strategy` will be `untrained`.

For more information on querying, see the [Query overview](/docs/discovery-data?topic=discovery-data-query-concepts).

## Understanding relevancy training
{: #understanding-training}

Answers to common questions about training a collection.

### How do I know if my system is trained?
{: #understanding-system}

Run a natural language query and check the `document_retrieval_strategy`. See [confidence scores](/docs/discovery-data?topic=discovery-data-train#confidence).

If you are using the API, see [List training queries](https://{DomainName}/apidocs/discovery-data#listtrainingqueries){: external}.

### How do I check errors and warnings?
{: #understanding-errors}

Open your project, then select the **Manage collections** icon on the navigation panel. Choose your collection, then open the **Activity** tab.

### How do I interpret the `confidence` score that appears in natural language query results after training?
{: #interpret-confidence}

See [confidence scores](/docs/discovery-data?topic=discovery-data-train#confidence).

## Interpreting relevancy training errors and warnings
{: #interpreting-errors}

Explanations of common error and warning messages.

### Warning: `Invalid training data found: The document was not returned in the top 100 search results for the given query, and will not be used for training`
{: #warning-docnotreturned}

This warning is caused by the `document_ids` in your training data not matching the `document_ids` in a search performed against the collection. Check your queries to make sure that the `document_id` of the document you are rating is returned in the top 100 results for that query. If it is not, then you might want to check two things:

- If the document is not returned in the top 100, it might not be an example of a high-quality result. Reevaluate whether to use the document.

- If the document is not returned at all, then review why it is not returned and see if there is any text in the document that matches portions of the query.

This warning indicates that you might have one or more failed queries. It is not an indication that training will not happen.
{: note}

### Error: `Invalid training data found: Syntax error when parsing query`
{: #error-syntax}

- A syntax error means there is an issue with the query syntax, which can happen when you add a filter to your natural language query.

### Error: `Training data quality standards not met: You will need additional training queries with labeled examples. (To be considered for training, each example must appear in the top 100 search results for its query.)`
{: #error-labels}

- You need to add more training data to train successfully. You need at least 49 unique training queries at a minimum, and each one needs at least one rated document. Minimum does not mean optimal; the size of the collection and other factors can increase the number of training examples needed to meet the minimum.

### Error: `Training data quality standards not met: Insufficient number of unique training queries. Expected at least n, but found m.`
{: #error-notunique}

- To meet the minimum training requirements, you need at least 50 unique training queries, and each one must have at least one rated document. If you have more than that and are still receiving this error message, you should check your notices for additional errors.

### Error: `Training data quality standards not met: No documents found with non-zero relevance labels.`
{: #error-relevance}

- Training data needs a sufficient amount of labeled data that specifies what documents are high value. This means that you need to rate some documents with non-zero values. You need to rate some documents as `Relevant` and some as `Not relevant`. At least one document must be rated `Relevant`.

### Error: `Training data quality standards not met: Training examples have no relevance label variety for X queries.`
{: #error-variety}

- One of the requirements for training is to have sufficient label diversity. This means at least 25% of the training queries must include both `Relevant` and `Not relevant` labels (if using the API, at least 25% of the queries should include two different numeric labels.)