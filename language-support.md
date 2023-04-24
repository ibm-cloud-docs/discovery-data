---

copyright:
  years: 2019, 2023
lastupdated: "2023-04-24"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Language support
{: #language-support}

When you create a collection, you specify the language of the collection. All of the documents that you add to a collection must be written in the same language.
{: shortdesc}

Discovery is not optimized for multilingual search. Although you can add several collections, each one with documents in a separate language, into one project, the query results from the project will be unpredictable. The results might include irrelevant passages from a document in a language that is different from the language of the user's query.
{: note}

The following table describes the product features that are supported in each language.

| Language | Supported features|
|:---|:---|
| Arabic (`ar`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Bosnian (`bs`) | Classifier (Document and Text), Custom entities, Dictionary, Parts of speech, Regular expressions |
| Chinese, simplified (`zh-CN`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding|
| Chinese, traditional (`zh-TW`) | Advanced rules models, Classifier (Document and Text), Custom entities, Dictionary, Regular expressions, Machine Learning, Optical character recognition v1, Parts of speech, Phrase sentiment, Smart Document Understanding, Table Understanding |
| Croatian (`hr`) | Classifier (Document and Text), Custom entities, Dictionary, Regular expressions, Parts of speech |
| Czech (`cs`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding  |
| Danish (`da`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Dutch (`nl`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1 (Installed), Optical character recognition v2 (Cloud-managed), Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding |
| English (`en`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Contracts, Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1 (Installed), Optical character recognition v2 (Cloud-managed), Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding |
| Finnish (`fi`) | Classifier (Document and Text), Custom entities, Dictionary, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| French (`fr`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1 (Installed), Optical character recognition v2 (Cloud-managed), Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| German (`de`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1 (Installed), Optical character recognition v2 (Cloud-managed), Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Hebrew (`he`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v2 (Cloud-managed), Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Hindi (`hi`) | Classifier (Document and Text), Custom entities, Dictionary, Parts of speech, Regular expressions |
| Italian (`it`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Japanese (`ja`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding |
| Korean (`ko`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Norwegian (Bokma&#778;l) (`nb`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Norwegian (Nynorsk) (`nn`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Polish (`pl`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Portuguese, Brazilian (`pt-br`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1 (Installed), Optical character recognition v2 (Cloud-managed), Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Romanian (`ro`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding  |
| Russian (`ru`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding |
| Serbian (`sr`)[^tabletext] | Classifier (Document and Text), Custom entities, Dictionary, Parts of speech, Regular expressions|
| Slovak (`sk`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Spanish (`es`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1 (Installed), Optical character recognition v2 (Cloud-managed), Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding  |
| Swedish (`sv`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
{: caption="Feature support per language" caption-side="top"}

[^tabletext]: Serbian supports Latin script only.

Optical character recognition (OCR) v2 was introduced in Cloud-managed service instances on 2 November 2022.
{: note}

<!-- **{{site.data.keyword.icp4dfull_notm}}**: For version 2.1.2 non-English language support, you must install the optional language pack `ibm-watson-discovery-pack1-prod`. Installation instructions for `ibm-watson-discovery-pack1-prod` are available in the [Installing the optional language pack](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/svc/watson/discovery-install.html){: external} section of the {{site.data.keyword.discovery-data_long}} installation instructions. The language pack does not need to be installed separately in {{site.data.keyword.discovery-data_long}} version 2.1.3 or later.
{: note}
-->

## English-only support
{: #feature-support}

The following features are currently supported in English only:

-  [Document Retrieval for Contract project type](/docs/discovery-data?topic=discovery-data-projects#doc-retrieval-contracts)
-  [IBM Cloud]{: tag-ibm-cloud} [Patterns (beta)](/docs/discovery-data?topic=discovery-data-domain-pattern)
