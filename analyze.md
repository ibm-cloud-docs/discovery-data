---

copyright:
  years: 2019, 2020
lastupdated: "2020-06-24"

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

The Analyze endpoint allows you to process text documents through {{site.data.keyword.discoveryshort}}'s conversion and enrichment pipeline without requiring the document to be stored. This is ideal for business automation purposes, for example if you want to classify emails - you can use Analyze to synchronously call {{site.data.keyword.discoveryshort}}, get a classification of the email, and use the output of that classification in your business logic. For details, see the {{site.data.keyword.discoveryshort}} [API reference](https://{DomainName}/apidocs/discovery-data#analyze-a-document){: external}.

Use of the Analyze API affects license usage, please reference the latest [license information](http://www.ibm.com/software/sla/sladb.nsf/searchlis/?searchview&searchorder=4&searchmax=0&query=(watson+discovery){: external}.