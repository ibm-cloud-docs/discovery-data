---

copyright:
  years: 2019, 2020
lastupdated: "2020-12-04"

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

# Analyze API
{: #analyzeapi}

![Cloud Pak for Data only](images/cpdonly.png)

The Analyze endpoint allows you to process text documents through {{site.data.keyword.discoveryshort}}'s enrichment pipeline without requiring the document to be stored. This is ideal for business automation purposes, for example if you want to classify emails - you can use Analyze to synchronously call {{site.data.keyword.discoveryshort}}, get a classification of the email, and use the output of that classification in your business logic. For details, see the {{site.data.keyword.discoveryshort}} [API reference](https://{DomainName}/apidocs/discovery-data#analyzedocument){: external}.

The Analyze API supports JSON documents only.
{: important}

Documents processed using the Analyze API are not added to the specified collection.
{: note}

The following enrichments are supported in the Analyze API:

  -  [Dictionary](/docs/discovery-data?topic=discovery-data-create-enrichments#dictionary-enrichment)
  -  [Regular expressions](/docs/discovery-data?topic=discovery-data-create-enrichments#characterpattern-enrichment)
  -  [Machine Learning and Watson Explorer Content Analytics Studio models](/docs/discovery-data?topic=discovery-data-create-enrichments#machinelearning-enrichment)
  -  [Classifier](/docs/discovery-data?topic=discovery-data-create-enrichments#classifier-enrichment)
  -  [Advanced rule models](/docs/discovery-data?topic=discovery-data-create-enrichments#advanced-rules)
  -  [Entities](/docs/discovery-data?topic=discovery-data-create-enrichments#entities)
  -  [Keywords](/docs/discovery-data?topic=discovery-data-create-enrichments#keywords)
  -  [Sentiment of documents](/docs/discovery-data?topic=discovery-data-create-enrichments#sentiment)

For the complete list of the enrichments supported in each language, see [Language support](/docs/discovery-data?topic=discovery-data-language-support). 

You can monitor the usage of the Analyze API using the {{site.data.keyword.discoveryshort}} tooling. For more information, see [API usage](/docs/discovery-data?topic=discovery-data-projects#api-usage).

Use of the Analyze API affects license usage, please reference the latest [license information](http://www.ibm.com/software/sla/sladb.nsf/searchlis/?searchview&searchorder=4&searchmax=0&query=(watson+discovery){: external}.