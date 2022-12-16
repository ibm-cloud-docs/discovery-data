---

copyright:
  years: 2019, 2022
lastupdated: "2022-12-16"

keywords: analyze on demand, on-demand, automate analysis

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Analyze API  ![Enterprise plan](images/enterprise.png) ![Cloud Pak for Data](images/cp4d.png)
{: #analyzeapi}

Use the Analyze API to process text documents through the enrichment pipeline of the {{site.data.keyword.discoveryshort}} service without storing the source documents.
{: shortdesc}

The Analyze API is supported with Enterprise plan deployments and installed deployments only.
{: note}

This approach is ideal for business automation purposes. For example, if you want to classify emails, you can use the Analyze API to synchronously call {{site.data.keyword.discoveryshort}} to get a classification of the email. Then, you can use the output of that classification in your business logic.

The Analyze API supports JSON documents only.
{: important}

When you analyze a document with the API, you indicate how you want the document to be processed by specifying the collection to associate with the analysis. The document is not stored in the collection. Instead, the configuration settings of the collection are applied to the document. For example, if you want to find entity references in a document, run the Analyze API against a collection where the *Entities* enrichment is applied. The resulting document analysis identifies any entity mentions in the document.

The following enrichments are supported in the Analyze API:

-   [Advanced rules models](/docs/discovery-data?topic=discovery-data-domain-advanced-rules)
-   [Contracts](/docs/discovery-data?topic=discovery-data-contracts-schema)
-   [Custom entities](/docs/discovery-data?topic=discovery-data-entity-extractor)
-   [Dictionary](/docs/discovery-data?topic=discovery-data-domain-dictionary)
-   [Document classifier](/docs/discovery-data?topic=discovery-data-cm-doc-classifier)
-   [Entities (NLP)](/docs/discovery-data?topic=discovery-data-nlu#nlu-entities)
-   [Keywords (NLP)](/docs/discovery-data?topic=discovery-data-nlu#nlu-keywords)
-   [Machine Learning and Watson Explorer Content Analytics Studio models](/docs/discovery-data?topic=discovery-data-domain-ml)
-   [Regular expressions](/docs/discovery-data?topic=discovery-data-domain-regex)
-   [Patterns](/docs/discovery-data?topic=discovery-data-domain-pattern) ![Enterprise plan](images/enterprise.png)
-   [Sentiment of documents](/docs/discovery-data?topic=discovery-data-nlu#nlu-sentiment)
-   [Table understanding](/docs/discovery-data?topic=discovery-data-understanding_tables)\*
-   [Text classifier](/docs/discovery-data?topic=discovery-data-domain-classifier)

\* For the table understanding enrichment to produce any results, the input must contain a `<table>` HTML element to analyze.

For the complete list of the enrichments that are supported in each language, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

For more information, see the {{site.data.keyword.discoveryshort}} [API reference](https://{DomainName}/apidocs/discovery-data#analyzedocument){: external}.

## Analysis example
{: #analyzeapi-example}

The data that you submit for analysis must be in JSON format. The text must be specified as a string; it cannot be specified as an array. For example, the following JSON file contains a quotation in the `Quote` field that you want to analyze to find any keyword mentions in the text.

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
curl --location --request POST \
'https://my-cloud-pak-for-data-cluster/discovery/zen-wd/instances/{instance-id}/api/v2/ \
projects/{project-id}/collections/{collection-id}/analyze?version=2020-08-30' \
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

You cannot submit an array of objects as input. For example, you might want to analyze multiple quotations, so your source might look as follows:

```json
{
  "quotations":[
    {
      "Author": "Jane Austen",
      "Book": "Sense and Sensibility",
      "Quote": "Is there a felicity in the world superior to this?",
      "Year": "1811/01/01",
      "Subject": "Nature",
      "Speaker": "Marianne Dashwood",
      "url": "https://www.gutenberg.org/files/1342/1342-h/1342-h.htm#link2HCH0059"
    },
    {
      "Author": "Jane Austen",
      "Book": "Persuasion",
      "Quote": "A man does not recover from such a devotion of the heart to such a woman. He ought not; he does not.",
      "Subject": "Romantic love",
      "Year": "1818/01/01",
      "Speaker": "Captain Wentworth",
      "url": "https://www.gutenberg.org/files/105/105-h/105-h.htm#chap20"
    }
  ]
}
```
{: codeblock}

If so, break each object into a separate file and analyze each file individually.

## Analyzing a text snippet
{: #analyzeapi-text}

You can submit text for analysis as long as you specify the text in JSON format by using syntax like this:

```json
{
"text":"The text that you want to analyze."
}
```
{: codeblock}

The following example request shows how to analyze text that you specify in the request, not that you pass in a physical file.

```curl
curl --location --request POST \
'https://my-cloud-pak-for-data-cluster/discovery/zen-wd/instances/{instance-id}/api/v2/ \
projects/{project-id}/collections/{collection-id}/analyze?version=2020-08-30' \
--header 'Authorization: Bearer ...' \
--form 'file={"text": "ISO 9000 is a standard."}'
```
{: codeblock}

The response might looks as follows.

```json
{
  "result" : {
    "enriched_text" : [ {
      "entities" : [ {
        "text" : "ISO 9000",
        "type" : "my_iso_pattern",
        "mentions" : [ {
          "text" : "ISO 9000",
          "confidence" : 1.0,
          "location" : {
            "begin" : 0,
            "end" : 8
          }
        } ],
        "model_name" : "My ISO Pattern"
      }, {
        "text" : "9000",
        "type" : "Number",
        "mentions" : [ {
          "text" : "9000",
          "confidence" : 0.8,
          "location" : {
            "begin" : 4,
            "end" : 8
          }
        } ],
        "model_name" : "natural_language_understanding"
      } ]
    } ],
    "metadata" : { },
    "text" : [ "ISO 9000 is a standard." ]
  },
  "notices" : [ ]
}
```
{: codeblock}

## Analyzing HTML content
{: #analyzeapi-html}

You can analyze HTML as long as you submit the html in JSON format by using syntax like this:

```json
{
"html":"<p>My html content.</p>"
}
```
{: codeblock}

The following example request shows how to analyze text that you specify in the request, not that you pass in a physical file. 

The collection to which the request is made has the following enrichments applied to it, which means these enrichment will be applied to the content that you submit with the API request:

-   Entities
-   Keywords
-   Table Understanding

### Request example
{: #analyzeapi-html-request}

The body of the request contains `form-data` with the name `file`. The value is the JSON content to be analyzed.

```curl
curl --location --request POST \
'https://cpd-abc.example.com/discovery/abc-wd/instances/1671204318684041/api/v2/projects/d457fcd9-a4ce-4637-a340-33123b5cbe2c/collections/2d47dbcc-64c7-84e9-0000-01851bb9d998/analyze?version=2020-08-30' \
--header 'Authorization: Bearer ...' \
--form 'file={
  "html":"<html><head>This is my html file</head><body><p>My file contains a table.</p><table><tbody><tr><th>Holiday</th><th>Popular greeting</th></tr><tr><td>Christmas</td><td>Merry Christma!s</td></tr></tbody></table></body></html>",
  "text":"This is a sentence that contains key words, such as George Washington and Boston, MA."
}'
```
{: codeblock}

### Results
{: #analyzeapi-html-results}

The results show the output of the Entities, Keywords, and Table Understanding enrichments on the `text` and `html` fields that were submitted.

```
{
    "result": {
        "text": [
            "This is a sentence that contains key words, such as George Washington and Boston, MA."
        ],
        "enriched_text": [
            {
                "keywords": [
                    {
                        "text": "George Washington",
                        "mentions": [
                            {
                                "text": "George Washington",
                                "location": {
                                    "begin": 52,
                                    "end": 69
                                }
                            }
                        ],
                        "relevance": 0.952591
                    },
                    {
                        "text": "Boston",
                        "mentions": [
                            {
                                "text": "Boston",
                                "location": {
                                    "begin": 74,
                                    "end": 80
                                }
                            }
                        ],
                        "relevance": 0.578079
                    },
                    {
                        "text": "MA",
                        "mentions": [
                            {
                                "text": "MA",
                                "location": {
                                    "begin": 82,
                                    "end": 84
                                }
                            }
                        ],
                        "relevance": 0.146905
                    }
                ],
                "entities": [
                    {
                        "text": "George Washington",
                        "type": "Location",
                        "mentions": [
                            {
                                "text": "George Washington",
                                "confidence": 0.54922265,
                                "location": {
                                    "begin": 52,
                                    "end": 69
                                }
                            }
                        ],
                        "model_name": "natural_language_understanding"
                    },
                    {
                        "text": "Boston, MA",
                        "type": "Location",
                        "mentions": [
                            {
                                "text": "Boston, MA",
                                "confidence": 0.66049105,
                                "location": {
                                    "begin": 74,
                                    "end": 84
                                }
                            }
                        ],
                        "model_name": "natural_language_understanding"
                    }
                ]
            }
        ],
        "metadata": {},
        "enriched_html": [
            {
                "tables": [
                    {
                        "body_cells": [
                            {}
                        ],
                        "location": {
                            "begin": 99,
                            "end": 183
                        },
                        "row_headers": [],
                        "key_value_pairs": [],
                        "section_title": {},
                        "contexts": [],
                        "text": "Holiday Popular greeting Christmas Merry Christmas!",
                        "table_headers": [],
                        "title": {},
                        "column_headers": []
                    }
                ]
            }
        ],
        "html": [
            "<html><head>This is my html file</head><body><p>My file contains a table.</p><table><tbody><tr><th>Holiday</th><th>Popular greeting</th></tr><tr><td>Christmas</td><td>Merry Christmas!</td></tr></tbody></table></body></html>"
        ]
    },
    "notices": []
}
```
{: codeblock}

## Analyze API limits
{: #analyzeapi-limits}

The following table shows the file size and usage limits for the Analyze API.

| Deployment type | File size limit | Concurrent collections limit | Concurrent queries per collection limit |
|-----------------|-----------------|------------------------------|-----------------------------------------|
| Cloud Pak for Data installed deployment | Unlimited | Unlimited | Unlimited |
| Enterprise plan managed deployment | 50 KB | 5 | 5 |
{: caption="Limits applied to Analyze API usage" caption-side="top"}

Use of the Analyze API from {{site.data.keyword.discoveryshort}} Cartridge for {{site.data.keyword.icp4dfull_notm}} affects license usage. For more information, see the latest [license information](https://www-40.ibm.com/software/sla/sladb.nsf/displaylis/F644E41EA1B29A96002587F10057A1C7?OpenDocument){: external}.

## Monitoring usage  ![Cloud Pak for Data](images/cp4d.png)
{: #api-usage}

You can monitor the usage of the Analyze API from the *API usage* page.

The *API usage* page is available from installed deployments only. For Enterprise plans, analyze method call information is combined with query method call information and is reported as part of the query metrics.
{: note}

To access the **API usage** page, open the **Projects** page, select **Data usage**, then **API usage**.

Start date
:   The start date of the API call-monitoring period.

End date
:   The end date of the API call-monitoring period.

30-day call total
:   Number of calls to the Analyze API in the 30-day time interval that is indicated by the **Start date** and **End date**. The time interval is determined by calculating the consecutive time period with the highest number of API calls. The 30-day window updates as the time interval with the highest number of API call changes.

The **API usage** is not displayed until some time after API usage monitoring begins. A delay in displaying the final total number of the **30-day call total** might occur, even if the 30-day period that is listed includes the current date.
{: note}
