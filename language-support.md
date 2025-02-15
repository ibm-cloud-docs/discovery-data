---

copyright:
  years: 2019, 2025
lastupdated: "2024-01-23"

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
|----------|-------------------|
| Arabic (`ar`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
| Bosnian (`bs`) | Classifier (Document and Text), Custom entities, Dictionary, Parts of speech, Regular expressions |
| Chinese, simplified (`zh-CN`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding|
| Chinese, traditional (`zh-TW`) | Advanced rules models, Classifier (Document and Text), Custom entities, Dictionary, Regular expressions, Machine Learning, Optical character recognition v1, Parts of speech, Phrase sentiment, Smart Document Understanding, Table Understanding |
| Croatian (`hr`) | Classifier (Document and Text), Custom entities, Dictionary, Regular expressions, Parts of speech |
| Czech (`cs`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding  |
| Danish (`da`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
| Dutch (`nl`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v2, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
| English (`en`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Contracts, Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v2, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
| Finnish (`fi`) | Classifier (Document and Text), Custom entities, Dictionary, Parts of speech, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
| French (`fr`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v2, Parts of speech, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
| German (`de`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v2, Parts of speech, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
| Hebrew (`he`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v2, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding. The optical character recognition (OCR) feature for Hebrew language text in images is a beta feature in {{site.data.keyword.discoveryshort}}. For more information, see [Release notes for {{site.data.keyword.discoveryshort}} for IBM Cloud](/docs/discovery-data?topic=discovery-data-release-notes#discovery-4october2023). |
| Hindi (`hi`) | Classifier (Document and Text), Custom entities, Dictionary, Parts of speech, Regular expressions, Stemmer |
| Italian (`it`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
| Japanese (`ja`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Table Understanding |
| Korean (`ko`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Norwegian (Bokma&#778;l) (`nb`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
| Norwegian (Nynorsk) (`nn`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
| Polish (`pl`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Portuguese, Brazilian (`pt-br`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v2, Parts of speech, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
| Romanian (`ro`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding  |
| Russian (`ru`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
| Serbian (`sr`)[^tabletext] | Classifier (Document and Text), Custom entities, Dictionary, Parts of speech, Regular expressions|
| Slovak (`sk`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Table Understanding |
| Spanish (`es`) | Advanced rules models, Built-in entities, Classifier (Document and Text), Custom entities, Dictionary, Document sentiment, Keywords, Machine Learning, Optical character recognition v2, Parts of speech, Phrase sentiment, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding  |
| Swedish (`sv`) | Classifier (Document and Text), Custom entities, Dictionary, Optical character recognition v1, Parts of speech, Regular expressions, Smart Document Understanding, Stemmer, Table Understanding |
{: caption="Feature support per language" caption-side="top"}

[^tabletext]: Serbian supports Latin script only.

Optical character recognition (OCR) v2 was introduced in Cloud-managed service instances on 2 November 2022. OCR v2 was introduced in {{site.data.keyword.icp4dfull_notm}} instances with version 4.7.1.
{: note}



## English-only support
{: #feature-support}

The following features are currently supported in English only:

-  [Document Retrieval for Contract project type](/docs/discovery-data?topic=discovery-data-projects#doc-retrieval-contracts)
-  [IBM Cloud]{: tag-ibm-cloud} [Patterns (beta)](/docs/discovery-data?topic=discovery-data-domain-pattern)
