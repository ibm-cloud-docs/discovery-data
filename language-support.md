---

copyright:
  years: 2019, 2020
lastupdated: "2020-07-23"

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
| Arabic (`ar`) | Parts of speech, Keywords, Entities, Document sentiment, Dictionary, Regular expressions, Machine Learning, Advanced rule models, Smart Document Understanding, Table Understanding |
| Chinese, simplified (`zh-CN`) | Parts of speech, Keywords, Entities, Document sentiment, Phrase sentiment, Dictionary, Regular expressions, Machine Learning, Advanced rule models, Smart Document Understanding, Table Understanding |
| Chinese, traditional</br> (`zh-TW`) | Parts of speech, Phrase sentiment, Dictionary, Regular expressions, Machine Learning, Advanced rule models, Smart Document Understanding, Table Understanding |
| Czech (`cs`) | Parts of speech, Phrase sentiment, Dictionary, Regular expressions, Smart Document Understanding, Table Understanding  |
| Danish (`da`) | Parts of speech, Dictionary, Regular expressions, Smart Document Understanding, Table Understanding |
| Dutch (`nl`) |Parts of speech, Keywords, Entities, Document sentiment, Phrase sentiment, Dictionary, Regular expressions, Machine Learning, Advanced rule models, Smart Document Understanding, Table Understanding |
| English (`en`) | Parts of speech, Keywords, Entities, Document sentiment, Phrase sentiment, Dictionary, Regular expressions, Machine Learning, Advanced rule models, Smart Document Understanding, Table Understanding |
| Finnish (`fi`) | Parts of speech, Dictionary, Regular expressions, Smart Document Understanding, Table Understanding |
| French (`fr`) | Parts of speech, Keywords, Entities, Document sentiment, Dictionary, Regular expressions, Machine Learning, Advanced rule models, Smart Document Understanding, Table Understanding |
| German (`de`) | Parts of speech, Keywords, Entities, Document sentiment, Dictionary, Regular expressions, Machine Learning, Advanced rule models, Smart Document Understanding, Table Understanding |
| Hebrew (`he`) | Parts of speech, Dictionary, Regular expressions, Smart Document Understanding, Table Understanding |
| Italian (`it`) | Parts of speech, Keywords, Entities, Document sentiment, Dictionary, Regular expressions, Machine Learning, Advanced rule models, Smart Document Understanding, Table Understanding |
| Japanese (`ja`) | Parts of speech, Keywords, Entities, Document sentiment, Phrase sentiment, Dictionary, Regular expressions, Machine Learning, Advanced rule models, Smart Document Understanding, Table Understanding |
| Korean (`ko`) | Parts of speech, Keywords, Entities, Document sentiment, Dictionary, Regular expressions, Machine Learning, Advanced rule models, Smart Document Understanding, Table Understanding |
| Norwegian (Bokma&#778;l) (`nb`) | Parts of speech, Dictionary, Regular expressions, Smart Document Understanding, Table Understanding |
| Norwegian (Nynorsk) (`nn`) | Parts of speech, Dictionary, Regular expressions, Smart Document Understanding, Table Understanding |
| Polish (`pl`) |  Parts of speech, Dictionary, Regular expressions, Smart Document Understanding, Table Understanding |
| Portuguese, Brazilian (`pt-br`) | Parts of speech, Keywords, Entities, Document sentiment, Dictionary, Regular expressions, Machine Learning, Advanced rule models, Smart Document Understanding, Table Understanding |
| Romanian (`ro`) | Parts of speech, Phrase sentiment, Dictionary, Regular expressions, Smart Document Understanding, Table Understanding  |
| Russian (`ru`) | Parts of speech, Phrase sentiment, Dictionary, Regular expressions, Smart Document Understanding, Table Understanding |
| Slovak (`sk`) | Parts of speech, Dictionary, Regular expressions, Smart Document Understanding, Table Understanding |
| Spanish (`es`) | Parts of speech, Keywords, Entities, Document sentiment, Phrase sentiment, Dictionary, Regular expressions, Machine Learning, Advanced rule models, Smart Document Understanding, Table Understanding  |
| Swedish (`sv`) | Parts of speech, Dictionary, Regular expressions, Smart Document Understanding, Table Understanding |


You can select the collection language when you create your collection. See [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections). 
{: tip}

 ![Cloud Pak for Data only](images/cpdonly.png) For version 2.1.2 non-English language support, you must install the optional language pack `ibm-watson-discovery-pack1-prod`. Installation instructions for `ibm-watson-discovery-pack1-prod` are available in the [Installing the optional language pack](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/svc/watson/discovery-install.html){: external} section of the {{site.data.keyword.discovery-data_long}} installation instructions. The language pack does not need to be installed separately in {{site.data.keyword.discovery-data_long}} version 2.1.3 or later.
{: important}

## English-only support
{: #feature-support}

The following feature is currently supported in English only:

-  ![Cloud Pak for Data only](images/cpdonly.png) [Discovery for Content Intelligence](/docs/discovery-data?topic=discovery-data-output_schema). The Discovery for Content Intelligence enrichments (`Contracts`, `Invoices`, and `Purchase orders`) are available only if you purchase and install Discovery for Content Intelligence.