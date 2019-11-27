---

copyright:
  years: 2019
lastupdated: "2019-11-27"

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

# Customizing and improving your project
{: #improve}

<!-- c/s help for the *Improve and customize* page. Do not delete. -->

You can use the **Improve and Customize** page in the {{site.data.keyword.discovery-data_long}} to try out queries, then add and test customizations to improve the query results for your project.
{: shortdesc}

To access the **Improve and Customize** page, select the **Improve and customize** icon on the navigation panel.

**To improve and customize your Document Retrieval project**:
1.  Enter a natural language query in the query box.
1.  Review the query results displayed. You can view the source document for each result by clicking on **View* passage** or **View document**.
1.  Configure the desired improvement tools. 
1.  For some of the tools, after you apply the improvement, a **Recrawl** or **Reprocess** of the collections in your project will start automatically. To do so manually, open the **Activity** page of each collection.
1.  Retry the query.

**To improve and customize your Conversational Search project**:
1.  Enter a question in the chat box.
1.  Review the query results displayed. 
1.  Configure the desired improvement tools. 
1.  For some of the tools, after you apply the improvement, a **Recrawl** or **Reprocess** of the collections in your project will start automatically. To do so manually, open the **Activity** page of each collection.
1.  Retry the question.


## Improvement tools
{: #improvement-tools}

The improvement tools available will vary depending on the **Project type** selected.

**Customize display**
-  **Facets**
   Create hierarchical categories within your data. You can also use facets generated from the results of your search (Dynamic facets). For more information, see [Creating facets](/docs/services/discovery-data?topic=discovery-data-facets)
-  **Search bar**
   Options: 
     -  **Autocomplete** - Suggested autocompletion of queries as they are typed. For more information, see the [Autocomplete](https://{DomainName}/apidocs/discovery-data#get-autocomplete-suggestions){: external} method.
     -  **Spelling suggestions** - Spelling suggestions will be offered for likely typos when searching.
-  **Search results**
   Options:
     -  **Passages** - A relevant passage is returned as a query result. You can specify the number of passages returned per document (**Passages per document**) as well as the **Maximum characters in a passage**. For details on passage retrieval, see [passages](/docs/services/discovery-data?topic=discovery-data-query-parameters#passages).
     -  **Field** - The specified field is used as the title of a query result (the title appears under each query result, along with the collection name).
  
**Extract meaning**
For more information about each of the following enrichments, see [Extracting meaning](/docs/services/discovery-data?topic=discovery-data-create-enrichments#extract-meaning)
-  **Entities**
-  **Parts of speech**
-  **Keywords**
-  **Sentiment of documents**

The **Contracts**, **Invoices**, and **Purchase orders** enrichments are only available if you have purchased and installed {{site.data.keyword.discovery-data_short}} for Content Intelligence and chosen the **Project type** of **Document retrieval**. See [Understanding {{site.data.keyword.discovery-data_short}} for Content Intelligence](/docs/services/discovery-data?topic=discovery-data-output_schema) for more information. You can select only one of these enrichments.

-  **Contracts**
-  **Invoices**
-  **Purchase orders**


**Teach domain concepts**
-  **Dictionaries** - Dictionaries allows you to enrich document fields in your collection. The enrichment terms can be synonyms (car, automotive, auto), or words in the same category (carburetor, piston, valves). For more information see [Dictionary enrichments](/docs/services/discovery-data?topic=discovery-data-create-enrichments#dictionary-enrichment).
-  **Classifiers** - The Classifier uses the labels and text examples you have specified in a `.csv` file to predict the categories of the documents in your collection. For more information see the [Classifier enrichment](/docs/services/discovery-data?topic=discovery-data-create-enrichments#classifier-enrichment).
-  **Character patterns** - The Character pattern enrichment uses regular expressions to identify and extract information from fields in your collection. For more information see [Character pattern enrichment](/docs/services/discovery-data?topic=discovery-data-create-enrichments#characterpattern-enrichment).
-  **Machine learning** - This enrichment uses models created in {{site.data.keyword.knowledgestudiofull}} for {{site.data.keyword.icp4dfull}} or Watson Explorer Content Analytics Studio to enrich your collection. For more information, see [Machine Learning enrichments](/docs/services/discovery-data?topic=discovery-data-create-enrichments#machinelearning-enrichment).
-  **Advanced rule models** - (beta) - This beta enrichment uses a model created and exported from the Advanced rule editor of {{site.data.keyword.knowledgestudiofull}} for {{site.data.keyword.icp4dfull}}. For more information, see [Advanced rule models enrichment](/docs/services/discovery-data?topic=discovery-data-create-enrichments#advanced-rules).


**Define structure**
-  **New fields** - Annotate fields within your documents to train a custom conversion model. As you annotate, Watson is learning and will start predicting annotations. For more information, see [Identify fields](/docs/services/discovery-data?topic=discovery-data-field-settings#identify-fields).
-  **Hidden fields** - This option allows you to choose which fields should be included in the index for this collection. You can switch off any fields you do not want to index. For more information, see [Managing fields](/docs/services/discovery-data?topic=discovery-data-field-settings#field-settings).
-  **Document splitting** - This option allows you to split your documents into segments based on a field name. Once split, each segment is a separate document that will be enriched, indexed, and returned as a separate query result. For more information, see [Managing fields](/docs/services/discovery-data?topic=discovery-data-field-settings#field-settings).

**Improve relevance**
-  **Synonyms** - You can expand the scope of a query beyond exact matches - for example, you can expand a query for "ibm" to include "international business machines" and "big blue" - by uploading a list of synonyms. For more information, see [Implementing synonyms](/docs/services/discovery-data?topic=discovery-data-query-expansion#query-expansion).
-  **Stopwords** - Stopwords are filtered out of queries because they are common terms that are not useful in a search. For more information, see [Defining stopwords](/docs/services/discovery-data?topic=discovery-data-stopwords#stopwords).
-  **Data management** - Add additional data to your collections. For more information, see [Configuring data sources](/docs/services/discovery-data?topic=discovery-data-collection-types#collection-types).
-  **Relevancy training** - The relevance of natural language query results can be improved in {{site.data.keyword.discovery-data_long}} with training. For more information, see [Improving result relevance with training](/docs/services/discovery-data?topic=discovery-data-train#train).



