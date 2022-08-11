---

copyright:
  years: 2019, 2021
lastupdated: "2022-08-11"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Improving result relevance with training
{: #train}

<!-- c/s help for the *Train* page. Do not delete.  -->

The relevance of natural language query results can be improved in {{site.data.keyword.discoveryfull}} with training.
{: shortdesc}

A relevancy model determines the most relevant documents to return in search results. Without relevancy training, a standard mechanism is used to determine relevance based on common factors. When you train a relevancy model, you help {{site.data.keyword.discoveryshort}} to use features that are unique to your documents as it determines relevance.

To train a relevancy model, you provide sample natural language queries, submit them to get results from your documents, and then rate those results. As you add more examples, the information you provide about result relevance for each query is used to learn about your project. After a successful relevancy training session, a ranker model is created. The model is used automatically by Discovery with the next natural language query. Discovery reorders the document results so that the most relevant results according to the relevancy training model are displayed first.

Relevancy training does not run continuously. Training occurs only when you initiate it. The set of documents that constitute the training data are used only during the training process. If a subsequent change is made to a document that was used to train the model, it does not change the trained model and does not trigger a new training session. Keep in mind that if many of the documents in your project change, it might be time to retrain the model to use the features from the updated documents.

At most one trained relevancy model is used at a time per project. If you retrain a model, the existing model is used until the new model is successfully trained, at which time the new model replaces the old model. You do not enable use of the training model with a query parameter. If present, the model is used for every natural language query that is submitted. The model is used whether you limit the search to one collection or all of the collections. For this reason, it is important that your training data represents queries that are likely to be answered by all of the collections in your project. To stop a project from using the relevancy training model, you can delete the model by using the API.

If documents that were used previously to train the model are removed from a collection, you must remove any references to them from the training data before you start to retrain the model. The model expects both the documents and queries from training data pairs to continue to exist. To remove these references, delete the training queries that returned the deleted documents. If the queries continue to be relevant, you can add them back to the training data and pair them with other documents.

For more information about the relevancy training API, see the [API reference documentation](https://cloud.ibm.com/apidocs/discovery-data#createtrainingquery){: external}.

The following 15-minute video demonstrates relevancy training, along with other features. The training information starts 9 minutes in.

![Demo: Watson Discovery Improving Result Relevancy](https://www.youtube.com/embed/wi_V9s8XF3c){: video output="iframe" data-script="none"  id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

To read a transcript of the video, [open the video on YouTube.com](https://www.youtube.com/watch?v=wi_V9s8XF3c), click the *More actions* icon, and then choose *Open transcript*.

## When to use relevancy training
{: #train-when}

Relevancy training is optional. Test the quality of your search results. If the results of your queries meet your needs, no further training is necessary. 

The training improves the relevancy of the documents that are returned in query responses. It does not improve the passages or answers that are returned per document. If you're using passage retrieval and your test results are returning good documents, but the wrong passages from the documents, relevancy training will not help.

For more information about when to use relevancy training, read the [Relevancy training for time-sensitive users](https://medium.com/ibm-data-ai/ibm-watson-discovery-relevancy-training-time-sensitive-18a190b0874a){: external} blog post on Medium.

## How fields are handled
{: #train-fields}

Unlike Discovery Query Language queries, with natural language queries you cannot specify which fields from the document you care about or how much significance to give to each one. Instead, when a natural language query is submitted, the root-level fields are all considered to have equal significance. When you teach Discovery with examples, the service figures out for you how much weight to give to each field.

Discovery builds a model that assigns different weights to term, bigram, and skip-gram matches for each of the root-level fields and balances them against matches from all of the other document fields. With enough examples, Discovery can return better answers because it knows where the best answers are typically stored.

Relevancy training cannot be used to give more weight to nested fields. Nested fields are grouped and assigned one overall score. No matter how much you train, Discovery never gives a nested field more weight than it gives to a root-level field. For more information about nested fields, see the [FAQ](/docs/discovery-data?topic=discovery-data-faqs#faq-nested-fields).
{: note}

## Training a project
{: #train-task}

The training data that is used to train the relevancy model includes these parts:

-   A natural language query that is representative of a query that your users might submit
-   Results of the query, which are returned by the service
-   The rating that you apply to the result that indicates whether the result is `relevant` or `not relevant`.

To apply relevancy training to a project, complete the following steps:

1.  Go to the **Improve and customize** page. On the **Improvement tools** panel, select **Improve relevance**, then **Relevancy training**.
1.  Enter a natural language query in the **Enter a question to train** field.

    Do not include a question mark in your query. Use the same wording as your users. For example, `IBM Watson in healthcare`. Write queries that include some of the terms that are mentioned in the target answer. Term overlap improves the initial results when the natural language query is evaluated.
1.  Click **Add+**.
1.  Click **Rate results**.
1.  After the results are displayed, assess each result, and then select **Relevant** or **Not relevant**, whichever option applies given the quality of the result.

    When you select **Relevant**, you apply a score of `10` to the result. **Not relevant** applies a score of `0`. You can use a different scoring scale if you use the API to rate results, but you can't mix scoring scales within the same project.
1.  When you are finished, click **Back to queries**.
1.  Continue adding queries and rating them.

    As you rate results, your progress is shown. Check your progress to see when enough rating information is available to meet the training threshold needs. Your progress is broken into the following tasks:

    -   Add more queries
    -   Rate more results
    -   Add more variety to your ratings

    You must evaluate at least 50 unique queries, maybe more, depending on the complexity of your data. You cannot add more than 10,000 training queries.
1.  You can continue adding queries and rating results after you reach the threshold. Enter all of the queries that you think your users will ask.

    To delete a training query, click the **Delete** icon. To delete all of the training queries in your collection at one time, use the API. For more information, see [Delete training queries](https://{DomainName}/apidocs/discovery-data#deletetrainingqueries){: external}.

If two or more users attempt to train identical queries at the same time, the ratings that are submitted by one of the users overwrites the others.
{: note}

## Testing and iterating on the relevancy of results
{: #testing-results}

When you are done rating results, and training is completed, test to see whether your query results are better. To do so, run test natural language queries that are related (but not identical) to your training queries. Review the results.

If you want to continue to improve the results after testing, you can:

-   Add more documents to your collection.
-   Add more training queries.
-   Rate more results, making sure to use both the `Relevant` and `Not relevant` ratings.

## Confidence scores
{: #confidence}

{{site.data.keyword.discoveryshort}} returns a `confidence` score for natural language queries of trained collections. This `confidence` score is not interchangeable with `confidence` scores that are returned by untrained collections.

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

The `document_retrieval_strategy` can be found under the `retrieval_details`. If you query a trained collection by using the {{site.data.keyword.discoveryshort}} Query Language, or the trained model is temporarily disabled, the `document_retrieval_strategy` is `untrained`.

For more information on querying a project, see the [Query overview](/docs/discovery-data?topic=discovery-data-query-concepts).

## Relevancy training limits
{: #train-limits}

The following limits apply to relevancy training models:

-    One model per project
-    10,000 queries per model
-    40 models per service instance for Enterprise and Premium plans; 20 models for Plus plan instances

## Other ways to improve relevancy
{: #train-alternatives}

If you prefer to use the {{site.data.keyword.discoveryshort}} API to train {{site.data.keyword.discoveryshort}}, see the [API reference](https://{DomainName}/apidocs/discovery-data#listtrainingqueries){: external}.

You also can use the API to add curations. Curations is a beta feature that you can use to teach {{site.data.keyword.discoveryshort}} to return a specific document every time a certain query is submitted. For more information, see [Curations](/docs/discovery-data?topic=discovery-data-curations).

Adding a custom stopwords list can also improve the relevance of results for natural language queries. For more information, see [Identifying words to ignore](/docs/discovery-data?topic=discovery-data-stopwords).

## Understanding relevancy training
{: #understanding-training}

Answers to common questions about training a project.

### How do I know whether my system is trained?
{: #understanding-system}

Run a natural language query and check the `document_retrieval_strategy`. See [confidence scores](/docs/discovery-data?topic=discovery-data-train#confidence).

If you are using the API, see [List training queries](https://{DomainName}/apidocs/discovery-data#listtrainingqueries){: external}.

### How do I check errors and warnings?
{: #understanding-errors}

Open the **Manage collections** page. Choose your collection, then open the **Activity** tab.

### How do I interpret the confidence score that appears in natural language query results after training?
{: #interpret-confidence}

See [confidence scores](/docs/discovery-data?topic=discovery-data-train#confidence).

## Interpreting relevancy training errors and warnings
{: #interpreting-errors}

The following list has explanations for some common error and warning messages.

### Warning: `Invalid training data found: The document was not returned in the top 100 search results for the given query, and will not be used for training`
{: #warning-docnotreturned}

This warning is caused by the `document_ids` in your training data not matching the `document_ids` in a search that is performed against the collection. Check your queries to make sure that the `document_id` of the document you are rating is returned in the top 100 results for that query. If it is not, then you might want to check two things:

-   If the document is not returned in the top 100, it might not be an example of a high-quality result. Reevaluate whether to use the document.
-   If the document is not returned at all, then review why it is not returned and see whether any text in the document matches portions of the query.

This warning indicates that you might have one or more failed queries. It doesn't mean that the training cannot be completed.
{: note}

### Error: `Invalid training data found: Syntax error when parsing query`
{: #error-syntax}

A syntax error means that the query is invalid, which can happen when you add a filter to your natural language query.

### Error: `Training data quality standards not met: You will need additional training queries with labeled examples. (To be considered for training, each example must appear in the top 100 search results for its query.)`
{: #error-labels}

You need to add more training data to train successfully. You need at least 49 unique training queries at a minimum, and each one needs at least one rated document. Minimum does not mean optimal; the size of the collection and other factors can increase the number of training examples that are needed to meet the minimum.

### Error: `Training data quality standards not met: Insufficient number of unique training queries. Expected at least n, but found m.`
{: #error-notunique}

To meet the minimum training requirements, you need at least 50 unique training queries, and each query must have at least one rated document. If you have more queries than the minimum and are still receiving this error message, check your notices for other errors.

### Error: `Training data quality standards not met: No documents found with non-zero relevance labels.`
{: #error-relevance}

Training data needs enough labeled data that specifies what documents are high value. Therefore, you need to rate some documents with nonzero values. You need to rate some documents as `Relevant` and some as `Not relevant`. At least one document must be rated `Relevant`.

### Error: `Training data quality standards not met: Training examples have no relevance label variety for X queries.`
{: #error-variety}

One of the requirements for training is to have sufficient label diversity. At least 25% of the training queries must include both `Relevant` and `Not relevant` labels. If you use the API, at least 25% of the queries must include two different numeric labels.
