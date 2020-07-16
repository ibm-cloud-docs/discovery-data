---

copyright:
  years: 2019, 2020
lastupdated: "2020-07-14"

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

# IBM Cloud High availability and disaster recovery
{: #recovery}

![IBM Cloud only](images/cloudonly.png)</br>

{{site.data.keyword.discoveryfull}} is highly available in all {{site.data.keyword.cloud}} regions where {{site.data.keyword.discoveryshort}} is offered. However, recovering from potential disasters that affect an entire region requires planning and preparation.
{: shortdesc}

You are responsible for understanding your customization and usage of the service. You are also responsible for being ready to re-create an instance of the service in a new region and to restore your data in any region. See [How do I ensure zero downtime?](/docs/overview?topic=overview-zero-downtime#zero-downtime){: external} for more information.

## High availability
{: #ha}

{{site.data.keyword.discoveryfull}} supports high availability with no single point of failure. The service achieves high availability automatically and transparently by using the multi-zone region (MZR) feature provided by {{site.data.keyword.cloud_notm}}.

{{site.data.keyword.cloud_notm}} enables multiple zones that do not share a single point of failure within a single location. It also provides automatic load balancing across the zones within a region.

## Disaster recovery
{: #dr}

Disaster recovery can become an issue if an {{site.data.keyword.cloud_notm}} region experiences a significant failure that includes the potential loss of data. Because MZR is not available in all regions, wait for IBM to bring a region back online if it becomes unavailable. If underlying data services are compromised by the failure, also wait for IBM to restore those data services.

If a catastrophic failure occurs, IBM might not be able to recover data from database backups. In this case, you need to restore your data to return your service instance to its most recent state. You can restore the data to the same or to a different region.

Your disaster recovery plan includes knowing, preserving, and being prepared to restore all data that is maintained on {{site.data.keyword.cloud_notm}}.

## Backing up your data in Watson Discovery
{: #backupdata}

There are several methods for backing up the data stored in {{site.data.keyword.discoveryfull}}. Consider including these methods in your disaster recovery plan. Also consider backing up the following data types:

-  Data that you might want a copy of, such as source documents
-  Data that {{site.data.keyword.discoveryshort}} stores and that you want to extract and back up
  
Some data you cannot back up and must be recreated.

### Ingested documents
{: #backupdocs}

Your uploaded documents are converted, enriched, and stored in the search index. In the event of a disaster, the search index is not recoverable. Store a backup of all your source documents in a safe place.

If you also import documents by doing scheduled crawls of external data sources, you might want to retain your data source credentials externally so that you can re-establish your data sources quickly. For the list of available sources and the credentials needed for each one, see [Configuring IBM Cloud data sources](/docs/discovery-data?topic=discovery-data-sources).

### Training data
{: #backuptraining}

Refer to this task to back up your training data queries and examples for a trained project. Training data is used for explicit training of your projects and is stored on a per project basis. To extract the training data, use the API to download the queries and the ratings from {{site.data.keyword.discoveryshort}}. To back up training data queries and examples, complete the following steps:

1. Download your training data by using the [list training queries](https://{DomainName}/apidocs/discovery-data#list-training-queries){: external} API.
1. Save your training queries and examples locally.

The document IDs that you use in your training data point to the documents in your current project. Use the same IDs in your new projects to ensure that the correct documents are referenced. If the IDs do not match, your restored relevancy training will not work.
{: important}

### Expansion lists
{: #backupexpansions}

If you are using synonyms (query expansions) for query modification, back up your .json expansion list, and store it locally. For more information, see [Implementing synonyms](/docs/discovery-data?topic=discovery-data-search-settings#query-expansion).

### Stopwords
{: #backupstopwords}

In the case of stopwords, back up the text file. For more information about stopwords, see [Defining stopwords](/docs/discovery-data?topic=discovery-data-search-settings#stopwords).

### Collection information
{: #collectioninfo}

This is not required, but it is a good best practice to [retrieve the status](https://{DomainName}/apidocs/discovery-data#get-collection){: external} for each collection on a regular basis and store the information locally. By retaining these statistics, you can later verify that your restoration processes were successful if needed.
{: tip} 


### Smart Document Understanding models
{: #backupsdu}

If you use Smart Document Understanding (SDU), you have models associated with your configuration. To avoid loss of this information, [export your models](/docs/discovery-data?topic=discovery-data-configuring-fields#import), back them up, and store them locally. SDU models have the file extension of `.sdumodel`.


## Restoring your data to a new Watson Discovery instance
{: #restoredata}

Consider using your backups to restore to a new {{site.data.keyword.discoveryshort}} instance in a different data center, also known as a region or location. These regions or locations include Dallas; Washington, DC; London; Seoul; Tokyo; Sydney; and Frankfurt.
{: note}

To begin restoration, first start by reviewing your list of collections and associated data sources, as well as your file backups.

-  Create your projects and collections. Use the {{site.data.keyword.discoveryshort}} tooling, or the API. See [Create a project](https://{DomainName}/apidocs/discovery-data#create-a-project){: external} and [Create a collection](https://{DomainName}/apidocs/discovery-data#create-a-collection){: external}.
-  Add back stopwords into the collections. See [Defining stopwords](/docs/discovery-data?topic=discovery-data-search-settings#stopwords).  
-  If you use custom query expansion, add your query expansions. See [Implementing synonyms](/docs/discovery-data?topic=discovery-data-search-settings#query-expansion).
-  If you use any custom entity models from {{site.data.keyword.knowledgestudiofull}} for enrichment, reimport that model into your {{site.data.keyword.discoveryshort}} instance. For details, see [Managing enrichments](/docs/discovery-data?topic=discovery-data-configuring-fields#enrich-fields).

After you set up your projects and collections as they were before, begin ingesting your source documents. Depending upon how you ingested your documents previously, you can do so by using your own solution or one of the following methods:
-  The [API](https://{DomainName}/apidocs/discovery-data#add-a-document){: external}
-  A [connector](/docs/discovery-data?topic=discovery-data-sources)

### Restoring training data
{: #restoretraining}

After you restore your projects, you can begin the process of recreating your relevancy training models. To restore your training data queries and examples, recreate your individual training queries and the examples by using the [create training query](https://{DomainName}/apidocs/discovery-data#create-training-query){: external} API, or you can restore your queries and examples on {{site.data.keyword.discoveryshort}}. For more information about restoring your training data by using {{site.data.keyword.discoveryshort}}, see the instructions for accessing the **Train** page in [Improving result relevance with training](/docs/discovery-data?topic=discovery-data-train).

For the restore to work properly, note that the document IDs that you use in your training data point to the documents in your current project. Use the same IDs in your new projects to ensure that the correct documents are referenced. If the IDs do not match, your restored relevancy training will not work.
{: important}

### Restoring connections to external data sources
{: #restoreconnections}

In case of an unanticipated loss of data, you might lose your scheduled crawls of external data sources. See [Configuring IBM Cloud data sources](/docs/discovery-data?topic=discovery-data-sources) for the list of available sources.

To restore your external data, re-establish your connections to these data sources, and then re-crawl them.

To find the data source credentials that you stored, follow the instructions for your chosen data source in [Configuring IBM Cloud data sources](/docs/discovery-data?topic=discovery-data-sources). These instructions explain how you can reconnect to your data sources and get the data imported into {{site.data.keyword.discoveryshort}}.


### Restoring Smart Document Understanding models
{: #restoresdu}

To import a previously exported Smart Document Understanding (SDU) model, see [Importing and exporting models](/docs/discovery-data?topic=discovery-data-configuring-fields#import). SDU models have the file extension of `.sdumodel`.

When importing an SDU existing model into a new collection, it is a good best practice to create the new collection and add one document, then import the model and upload the remainder of your documents.
