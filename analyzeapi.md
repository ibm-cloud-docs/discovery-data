---

copyright:
  years: 2019, 2022
lastupdated: "2022-04-11"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Analyze API
{: #analyzeapi}

Use the Analyze endpoint to process text documents through the enrichment pipeline of the {{site.data.keyword.discoveryshort}} service without storing the source documents.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

This approach is ideal for business automation purposes. For example, if you want to classify emails, you can use the Analyze API to synchronously call {{site.data.keyword.discoveryshort}} to get a classification of the email. Then, you can use the output of that classification in your business logic.

Use of the Analyze API affects license usage. For more information, see the latest [license information](http://www.ibm.com/software/sla/sladb.nsf/searchlis/?searchview&searchorder=4&searchmax=0&query=discovery){: external}.

The Analyze API supports JSON documents only.
{: important}

When you analyze a document with the API, you indicate how you want the document to be processed by specifying the collection to associate with the analysis. The document is not stored in the collection. Instead, the configuration settings of the collection are applied to the document. For example, if you want to find keyword references in a document, run the Analyze API against a collection where the Keywords enrichment is applied. The resulting document analysis identifies any keyword mentions in the document.

The following enrichments are supported in the Analyze API:

- [Dictionary](/docs/discovery-data?topic=discovery-data-domain#dictionary)
- [Regular expressions](/docs/discovery-data?topic=discovery-data-domain#regex)
- [Machine Learning and Watson Explorer Content Analytics Studio models](/docs/discovery-data?topic=discovery-data-domain#machinelearning)
- [Document classifier](/docs/discovery-data?topic=discovery-data-contentminerapp#create-doc-classifier)
- [Text classifier](/docs/discovery-data?topic=discovery-data-domain#classifier)
- [Advanced rule models](/docs/discovery-data?topic=discovery-data-domain#advanced-rules)
- [Entities](/docs/discovery-data?topic=discovery-data-nlu#nlu-entities)
- [Keywords](/docs/discovery-data?topic=discovery-data-nlu#nlu-keywords)
- [Sentiment of documents](/docs/discovery-data?topic=discovery-data-nlu#nlu-sentiment)

For the complete list of the enrichments that are supported in each language, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

For more information, see the {{site.data.keyword.discoveryshort}} [API reference](https://{DomainName}/apidocs/discovery-data#analyzedocument){: external}.

## Analysis example
{: #analyzeapi-example}

The following JSON file contains a quotation in the `Quote` field that you want to analyze to find any keyword mentions in the text.

```json
{
  "Author": "Jane Austen",
  "Book": "Pride and Prejudice",
  "Quote": "From this day you must be a stranger to one of your parents. Your mother will never see you again if you do not marry Mr. Collins, and I will never see you again if you do.",
  "Year": "1813/01/01",
  "Subject":"Parental love",
  "Speaker": "Mr. Bennett",
  "url": "https://www.gutenberg.org/files/1342/1342-h/1342-h.htm#link2HCH0020"
}
```
{: codeblock}

You know the name of a collection in your project where the *Keywords* enrichment is configured to be applied to documents in the collection. You can use the API to [list your collections](https://cloud.ibm.com/apidocs/discovery-data#listcollections){: external} to find the ID associated with the collection that you look for by name.

After you get the collection ID, include it in the POST request that you submit to apply the configuration settings from the collection to your JSON file. For example, the following request submits the JSON snippet in a file named `favorites2.json` for keyword analysis.

```curl
curl --location --request POST 'https://my-cloud-pak-for-data-cluster/discovery/zen-wd/instances/{instance-id}/api/v2/projects/{project-id}/collections/{collection-id}/analyze?version=2020-08-30' \
--header 'Authorization: Bearer ...' \
--form 'file=@"/quotations/favorites2.json"'
```
{: codeblock}

The result contains a list of keywords that were recognized in the quotation.

```json
{
  "result": {
    "enriched_Quote": [
      {
        "keywords": [
          {
            "text": "day",
            "mentions": [
              {
                "text": "day",
                "location": {
                  "begin": 10,
                  "end": 13
                }
              }
            ],
            "relevance": 0.673739
          },
          {
            "text": "stranger",
            "mentions": [
              {
                "text": "stranger",
                "location": {
                  "begin": 28,
                  "end": 36
                }
              }
            ],
            "relevance": 0.596757
          },
          {
            "text": "parents",
            "mentions": [
              {
                "text": "parents",
                "location": {
                  "begin": 52,
                  "end": 59
                }
              }
            ],
            "relevance": 0.568336
          },
          {
            "text": "mother",
            "mentions": [
              {
                "text": "mother",
                "location": {
                  "begin": 66,
                  "end": 72
                }
              }
            ],
            "relevance": 0.755562
          },
          {
            "text": "Mr. Collins",
            "mentions": [
              {
                "text": "Mr. Collins",
                "location": {
                  "begin": 118,
                  "end": 129
                }
              }
            ],
            "relevance": 0.945891
          }
        ]
      }
    ],
    "url": "https://www.gutenberg.org/files/1342/1342-h/1342-h.htm#link2HCH0020",
    "Subject": "Parental love",
    "Year": "1813/01/01",
    "Book": "Pride and Prejudice",
    "Author": "Jane Austen",
    "Quote": [
      "From this day you must be a stranger to one of your parents. Your mother will never see you again if you do not marry Mr. Collins, and I will never see you again if you do."
    ],
    "metadata": {
      "name": "favorites2.json"
    },
    "Speaker": "Mr. Bennett"
  },
  "notices": []
}
```
{: codeblock}

<!--## Monitoring usage
{: #api-usage}

You can monitor the usage of the Analyze API from the *API usage* page.

To access the **API usage** page, open the **Projects** page, select **Data usage**, then **API usage**.

Start date
:   The start date of the API call-monitoring period.

End date
:   The end date of the API call-monitoring period.

30-day call total
:   Number of calls to the Analyze API in the 30-day time interval that is indicated by the **Start date** and **End date**. The time interval is determined by calculating the consecutive time period with the highest number of API calls. The 30-day window updates as the time interval with the highest number of API call changes.

The **API usage** is not displayed until some time after API usage monitoring begins. A delay in displaying the final total number of the **30-day call total** might occur, even if the 30-day period that is listed includes the current date.
{: note}
-->