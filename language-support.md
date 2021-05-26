---

copyright:
  years: 2019, 2021
lastupdated: "2021-05-26"

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
{:external: target="_blank" .external}

# Language support
{: #language-support}

| Language | Supported features|
|:---|:---|
| Arabic (`ar`) | Advanced rule models, Dictionary, Document sentiment, Entities, Keywords, Machine Learning, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Bosnian (`bs`)\* | Dictionary, Parts of speech, Regular expressions |
| Chinese, simplified (`zh-CN`) | Advanced rule models, Dictionary, Document sentiment, Entities, Keywords, Machine Learning, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding|
| Chinese, traditional</br> (`zh-TW`) | Advanced rule models, Dictionary, Regular expressions, Machine Learning, Parts of speech, Phrase sentiment, Smart Document Understanding, Table Understanding |
| Croatian (`hr`)\* | Dictionary, Regular expressions, Parts of speech |
| Czech (`cs`) | Dictionary, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding  |
| Danish (`da`) | Dictionary, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Dutch (`nl`) | Advanced rule models, Dictionary, Document sentiment, Entities, Keywords, Machine Learning, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding |
| English (`en`) | Advanced rule models, Contracts, Dictionary, Document sentiment, Entities, Keywords, Machine Learning, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding |
| Finnish (`fi`) | Dictionary, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| French (`fr`) | Advanced rule models, Dictionary, Document sentiment, Entities, Keywords, Machine Learning, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| German (`de`) | Advanced rule models, Dictionary, Document sentiment, Entities, Keywords, Machine Learning, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Hebrew (`he`) | Dictionary, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Hindi (`hi`)\* | Dictionary, Parts of speech, Regular expressions |
| Italian (`it`) | Advanced rule models, Dictionary, Document sentiment, Entities, Keywords, Machine Learning, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Japanese (`ja`) | Advanced rule models, Dictionary, Document sentiment, Entities, Keywords, Machine Learning, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding |
| Korean (`ko`) | Advanced rule models, Dictionary, Document sentiment, Entities, Keywords, Machine Learning, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Norwegian (Bokma&#778;l) (`nb`) | Dictionary, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Norwegian (Nynorsk) (`nn`) | Dictionary, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Polish (`pl`) |  Dictionary, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Portuguese, Brazilian (`pt-br`) | Advanced rule models, Dictionary, Document sentiment, Entities, Keywords, Machine Learning, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Romanian (`ro`) | Dictionary, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding  |
| Russian (`ru`) | Dictionary, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding |
| Serbian (`sr`)\* | Dictionary, Parts of speech, Regular expressions|
| Slovak (`sk`) | Dictionary, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Spanish (`es`) | Advanced rule models, Dictionary, Parts of speech, Keywords, Entities, Document sentiment, Phrase sentiment, Regular expressions, Machine Learning, Smart Document Understanding, Table Understanding  |
| Swedish (`sv`) | Dictionary, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |


\* **Optical character recognition (OCR)** is not available for Bosnian, Croatian, Hindi, and Serbian. Serbian supports Latin script only.

You can select the collection language when you create your collection. See [Creating collections](/docs/discovery-data?topic=discovery-data-collections). 
{: tip}

 ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: For version 2.1.2 non-English language support, you must install the optional language pack `ibm-watson-discovery-pack1-prod`. Installation instructions for `ibm-watson-discovery-pack1-prod` are available in the [Installing the optional language pack](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/svc/watson/discovery-install.html){: external} section of the {{site.data.keyword.discovery-data_long}} installation instructions. The language pack does not need to be installed separately in {{site.data.keyword.discovery-data_long}} version 2.1.3 or later.
{: note}

## English-only support
{: #feature-support}

The following features are currently supported in English only:

-  [Document Retrieval for Contract project type](/docs/discovery-data?topic=discovery-data-projects#doc-retrieval-contracts)
-  ![IBM Cloud only](images/ibm-cloud.png) **IBM Cloud only**: [Patterns (beta)](/docs/discovery-data?topic=discovery-data-domain#patterns)