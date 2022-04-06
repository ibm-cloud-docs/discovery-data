---

copyright:
  years: 2019, 2022
lastupdated: "2022-04-06"

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

Documents that are processed by using the Analyze API are not added to the specified collection.

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

## Monitoring usage
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
