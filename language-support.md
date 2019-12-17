---

copyright:
  years: 2019
lastupdated: "2019-12-16"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}
{:external: target="_blank" .external}

# Language support
{: #language-support}

The following languages are supported in {{site.data.keyword.discovery-data_long}} when the `ibm-watson-discovery-pack1-prod`language pack is installed.
{: shortdesc}

Installation instructions for `ibm-watson-discovery-pack1-prod` are available in the [Installing the optional language pack](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/svc/watson/discovery-install.html){: external} section of the {{site.data.keyword.discovery-data_long}} installation instructions.

`S` = Supported with installed language pack

`NS` = Not supported

| Language | Parts of speech | Keywords | Entities | Document sentiment | Phrase sentiment | Dictionary | Character Pattern | Machine Learning | Advanced rule models | Smart Document Understanding |
|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|
| Arabic (`ar`) |`S`|`S`|`S`|`S`|`NS`|`S`|`S`|`S`|`S`|`S`|
| Chinese, simplified (`zh-CN`) |`S`|`S`|`S`|`S`|`S`|`S`|`S`|`S`|`S`|`S`|
| Chinese, traditional (`zh-TW`) |`S`|`NS`|`NS`|`NS`|`S`|`S`|`S`|`S`|`S`|`S`|
| Dutch (`nl`) |`S`|`S`|`S`|`S`|`S`|`S`|`S`|`S`|`S`|`S`|
| French (`fr`) |`S`|`S`|`S`|`S`|`NS`|`S`|`S`|`S`|`S`|`S`|
| German (`de`) |`S`|`S`|`S`|`S`|`NS`|`S`|`S`|`S`|`S`|`S`|
| Italian (`it`) |`S`|`S`|`S`|`S`|`NS`|`S`|`S`|`S`|`S`|`S`|
| Japanese (`ja`) |`S`|`S`|`S`|`S`|`S`|`S`|`S`|`S`|`S`|`S`|
| Korean (`ko`) |`S`|`S`|`S`|`S`|`NS`|`S`|`S`|`S`|`S`|`S`|
| Portuguese, Brazilian (`pt-br`) |`S`|`S`|`S`|`S`|`NS`|`S`|`S`|`S`|`S`|`S`|
| Spanish (`es`) |`S`|`S`|`S`|`S`|`S`|`S`|`S`|`S`|`S`|`S`|
| Czech (`cs`) |`S`|`NS`|`NS`|`NS`|`S`|`S`|`S`|`NS`|`NS`|`S`|
| Slovak (`sk`) |`S`|`NS`|`NS`|`NS`|`NS`|`S`|`S`|`NS`|`NS`|`S`|
| Russian (`ru`) |`S`|`NS`|`NS`|`NS`|`S`|`S`|`S`|`NS`|`NS`|`S`|
| Polish (`pl`) |`S`|`NS`|`NS`|`NS`|`NS`|`S`|`S`|`NS`|`NS`|`S`|
| Romanian (`ro`) |`S`|`NS`|`NS`|`NS`|`S`|`S`|`S`|`NS`|`NS`|`S`|


You can select the collection language when you create your collection. See [Creating and managing collections](/docs/services/discovery-data?topic=discovery-data-collections#collections). 
{: tip}


## English-only support
{: #feature-support}

The following feature is currently supported in English only:

-  [Discovery for Content Intelligence](/docs/services/discovery-data?topic=discovery-data-output_schema).

The following feature (available using the API-only) is currently supported in English only:

-  Spelling correction