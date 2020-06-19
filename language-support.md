---

copyright:
  years: 2019, 2020
lastupdated: "2020-06-19"

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

**X** = Supported in Watson Discovery

| Language | Parts of speech | Keywords | Entities | Document sentiment | Phrase sentiment | Dictionary | Regular expressions | Machine Learning | Advanced rule models | Smart Document Understanding |
|------|------|------|------|------|------|------|------|------|------|------|
| Arabic (`ar`) | **X** | **X** | **X** | **X** | | **X** | **X** | **X** | **X** | **X** |
| Chinese, simplified (`zh-CN`) | **X** | **X** | **X** | **X** | **X** | **X** | **X** | **X** | **X** | **X** |
| Chinese, traditional (`zh-TW`) | **X** | | | | **X** | **X** | **X** | **X** | **X** | **X** |
| Czech (`cs`) | **X** | | | | **X** | **X** | **X** | | | **X** |
| Danish (`da`) | **X** | | | | | **X** | **X** | | | **X** |
| Dutch (`nl`) | **X** | **X** | **X** | **X** | **X** | **X** | **X** | **X** | **X** | **X** |
| Finnish (`fi`) | **X** | | | | | **X** | **X** | | | **X** |
| French (`fr`) | **X** | **X** | **X** | **X** | | **X** | **X** | **X** | **X** | **X** |
| German (`de`) | **X** | **X** | **X** | **X** | | **X** | **X** | **X** | **X** | **X** |
| Hebrew (`he`) | **X** | | | | | **X** | **X** | | | **X** |
| Italian (`it`) | **X** | **X** | **X** | **X** | | **X** | **X** | **X** | **X** | **X** |
| Japanese (`ja`) | **X**| **X** | **X** | **X** | **X** | **X** | **X** | **X** | **X** | **X** |
| Korean (`ko`) | **X**| **X** | **X** | **X** | | **X** | **X** | **X** | **X** | **X** |
| Norwegian (Bokma&#778;l) (`nb`) | **X** | | | | | **X** | **X** | | | **X** |
| Norwegian (Nynorsk) (`nn`) | **X** | | | | | **X** | **X** | | | **X** |
| Polish (`pl`) | **X** | | | | | **X** | **X** | | | **X** |
| Portuguese, Brazilian (`pt-br`) | **X** | **X** | **X** | **X** | | **X** | **X** | **X** | **X** | **X** |
| Romanian (`ro`) | **X** | | | | **X** | **X**| **X** | | | **X** |
| Russian (`ru`) | **X** | | | | **X** | **X** | **X** | | | **X** |
| Slovak (`sk`) | **X** | | | | | **X**| **X** | | | **X** |
| Spanish (`es`) | **X** | **X** | **X** | **X** | **X** | **X** | **X** | **X** | **X** | **X** |
| Swedish (`sv`) | **X** | | | | | **X** | **X** | | | **X** |


You can select the collection language when you create your collection. See [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections). 
{: tip}

 <!-- ![Cloud Pak for Data only](images/cpdonly.png) --> For version 2.1.2 non-English language support, you must install the optional language pack `ibm-watson-discovery-pack1-prod`. Installation instructions for `ibm-watson-discovery-pack1-prod` are available in the [Installing the optional language pack](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/svc/watson/discovery-install.html){: external} section of the {{site.data.keyword.discovery-data_long}} installation instructions. The language pack does not need to be installed separately in {{site.data.keyword.discovery-data_long}} version 2.1.3 or later.
{: important}

## English-only support
{: #feature-support}

The following feature is currently supported in English only:

-  [Discovery for Content Intelligence](/docs/discovery-data?topic=discovery-data-output_schema)