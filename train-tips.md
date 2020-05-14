---

copyright:
  years: 2019, 2020
lastupdated: "2020-05-13"

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

# Relevancy training tips
{: #relevancy-tips}

Answers to common questions about training a collection and explanations of common error and warning messages. For more information on training queries, see [Improving result relevance with training](/docs/discovery-data?topic=discovery-data-train).
{: shortdesc}

## Understanding training
{: #understanding-training}

Answers to common questions about training a collection.

### How do I know if my system is trained?
{: #understanding-system}

Run a natural language query and check the `document_retrieval_strategy`. See [confidence scores](/docs/discovery-data?topic=discovery-data-train#confidence).

If using the API, see [List training queries](https://{DomainName}/apidocs/discovery-data#list-training-queries){: external}.

### How do I check errors and warnings?
{: #understanding-errors}

Open your project, then select the **Manage collections** icon on the navigation panel. Choose your collection, then open the **Activity** tab. For more information, see [Collection activity](/docs/discovery-data?topic=discovery-data-collections#collection-overview).

### How do I interpret the `confidence` score that appears in natural language query results after training?
{: #interpret-confidence}

See [confidence scores](/docs/discovery-data?topic=discovery-data-train#confidence). 

## Interpreting Errors and Warnings
{: #interpreting-errors}

Explanations of common error and warning messages.

### Warning: `Invalid training data found: The document was not returned in the top 100 search results for the given query, and will not be used for training`
{: #warning-docnotreturned}

This warning is caused by the `document_ids` in your training data not matching the `document_ids` in a search performed against the collection. You should check your queries, make sure that the `document_id` of the document you are rating is returned in the top 100 results for that query. If it is not, then you might want to check two things:  

- If the document is not returned in the top 100, it might not be a good example of a high-quality result, and you might want to revisit why this document was chosen.  

- If the document is not returned at all, then you should review why it is not returned and see if there is any text in the document that matches portions of the query.  

This warning indicates that you might have one or more failed queries. It is not an indication that training will not happen.
{: note}  

### Error: `Invalid training data found: Syntax error when parsing query`
{: #error-syntax}

- This means there is an issue with the actual query syntax. Validate that the queries return results and don’t raise a syntax error. This can only occur if you added a filter to your natural language query.

### Error: `Training data quality standards not met: You will need additional training queries with labeled examples. (To be considered for training, each example must appear in the top 100 search results for its query.)`
{: #error-labels}

- This means that you need to add more training data in order to train successfully. You need at least 49 unique training queries at a minimum, and each one needs at least one rated document. Minimum does not equate to optimal; the size of the collection and other factors can increase the number of training examples needed to meet the minimum.  

### Error: `Training data quality standards not met: Insufficient number of unique training queries. Expected at least n, but found m.`
{: #error-notunique}

- In order to meet the minimum training requirements; you need at least 50 unique training queries at a minimum, and each one needs at least one rated document. If you have more than that and are still receiving this error message, you should check your notices for additional errors.  

### Error: `Training data quality standards not met: No documents found with non-zero relevance labels.`
{: #error-relevance}

- Training data needs enough labeled data that specifies what documents are high value. This means that you need to rate some documents with non-zero values. You need to rate some documents as `Relevant` and some as `Not relevant`. At least one document must be rated `Relevant`.

### Error: `Training data quality standards not met: Training examples have no relevance label variety for X queries.`
{: #error-variety}

- One of the requirements for training is to have sufficient label diversity. This means at least 25% of the training queries must include both `Relevant` and `Not relevant` labels (if using the API, at least 25% of the queries should include two different numeric labels.)