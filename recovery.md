---

copyright:
  years: 2019, 2025
lastupdated: "2024-03-04"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# High availability and disaster recovery
{: #recovery}

{{site.data.keyword.discoveryfull}} is highly available in all {{site.data.keyword.cloud}} regions where {{site.data.keyword.discoveryshort}} is offered. However, recovering from potential disasters that affect an entire region requires planning and preparation.
{: shortdesc}

[IBM Cloud]{: tag-ibm-cloud}

This information applies only to managed deployments.
{: note}

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

You have several methods to back up the data that is stored in {{site.data.keyword.discoveryfull}}. You can back up the following data in your disaster recovery plan:

-  Data as a copy of the source documents
-  Data that is imported and exported from {{site.data.keyword.discoveryshort}}

 You can back up the resources that are listed in the following table to prevent data loss during disaster recovery.

| Resource | Backup process | UI support for resource download | UI support for resource upload | API support |
|----------|--------------------------------|-------------|-------------|-------------|
| Uploaded and crawled files | Securely store the backups for all source documents of the ingested data. For more information, see [Ingested documents](#backupdocs).  \n  \n Preserve the credentials of data sources for recrawling by reconnecting to the original data sources. For more information, see [Restoring connections to external data sources](/docs/discovery-data?topic=discovery-data-recovery#restoreconnections).  \n  \n For more information, see [Note](#note-uploaded-crawled-data). | No | No | Download – No  \n Upload - No |
| Relevancy training data | Download all training queries and examples and save them locally to back up the training data. For more information, see [Training data](#backuptraining). | No| No| Download – Yes  \n Upload - Yes |
| Expansion list | Download the expansion lists through [API](https://cloud.ibm.com/apidocs/discovery-data#listexpansions) and store them locally to restore the expansion lists. For more information, see [Expansion lists](#backupexpansions). | No | Yes| Download – Yes  \n Upload - Yes |
| Stop words list| Download the stop words lists through [API](https://cloud.ibm.com/apidocs/discovery-data#getstopwordlist) and store them locally to restore the stop words lists. For more information, see [Stop words](/docs/discovery-data?topic=discovery-data-stopwords). | No | Yes | Download – Yes  \n Upload - Yes |
| Smart Document Understanding user-trained model | Export your models and store them locally to back them up. For more information, see [Restoring Smart Document Understanding models](/docs/discovery-data?topic=discovery-data-recovery#backupsdu). | Yes | Yes | Download - No  \n Upload - No |
| Text classifier enrichment | Back up the .csv files of the classifier and store them locally. For more information, see [Text classifier](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-domain-classifier). | No | Yes | Upload - No  \n Download - No |
| Sentence classifier enrichment from sentence labelling | Download the .sc files of the sentence classifier models you created from the sentence labelling UI. For more information, see [Restoring sentence classifiers](/docs/discovery-data?topic=discovery-data-recovery#restore-sentence-classifier).| Yes | Yes | Download - No  \n Upload - No |
| Document classifier enrichment | Back up  the .csv files of the classifier and store them locally. For more information, see [Content Mining application resources](/docs/discovery-data?topic=discovery-data-recovery#cm-resources).  | No | Yes | Download - No  \n Upload - Yes |
| Dictionary enrichment | Download the .csv files of the dictionaries that you created by using the {{site.data.keyword.discoveryshort}} UI or Content Mining application. For more information, see [Restoring dictionary enrichments](/docs/discovery-data?topic=discovery-data-recovery#restoredictionary).  \n  \n You cannot download the dictionary as CSV files, if you created the dictionary by uploading the CSV files. | Yes | Yes | Download - No  \n Upload - Yes |
| Entity extractor enrichment | Download the entity extractor models and store them locally to back up the models. For more information, see [Restoring entity extractors](/docs/discovery-data?topic=discovery-data-recovery#restoreextractorenrich). | Yes | Yes | Download - No  \n Upload - No |
| Regular expression enrichment | Keep the terms of the regular expression that you specified in the {{site.data.keyword.discoveryshort}} UI. For more information, see [Regular expressions enrichments](/docs/discovery-data?topic=discovery-data-recovery#backupregexpenrich).   \n  \n You can create the regular expression enrichment through [API](/apidocs/discovery-data#createenrichment), but you cannot download it. | No | Yes | Download - No  \n Upload - Yes |
| Pattern enrichment | Download the pattern enrichments as .zip files and store them locally. For more information, see [Pattern enrichments](/docs/discovery-data?topic=discovery-data-recovery#patternenrich) and [Restoring pattern enrichments](/docs/discovery-data?topic=discovery-data-recovery#restorepatternenrich). | Yes | Yes | Download - No \n Upload - No |
| Advanced rules enrichment | Back up the original model files as .zip files and store them locally. For more information, see [Advanced rules models enrichment](/docs/discovery-data?topic=discovery-data-recovery#advrmenrich). | No | Yes | Download - No  \n Upload - No |
| Rule-based models created in Knowledge Studio | Back up the original model files as .pear files and store them locally. For more information, see [Use imported ML models to find custom terms](/docs/discovery-data?topic=discovery-data-domain-ml). | No | Yes | Download - No \n Upload - Yes |
| Machine learning models created in Knowledge Studio | Back up the original model files as .zip files and store them locally. For more information, see [Use imported ML models to find custom terms](/docs/discovery-data?topic=discovery-data-domain-ml). | No | Yes | Download - No \n Upload - Yes |
| [IBM Cloud Pak for Data]{: tag-cp4d} Custom UIMA text analysis models| Back up the original model files as .pear files and store them locally. For more information, see [Use imported ML models to find custom terms](/docs/discovery-data?topic=discovery-data-domain-ml). | No | Yes | Download - No  \n Upload - Yes |
{: row-headers}
{: class="comparison-table"}
{: caption="Resource recovery support details" caption-side="top"}
{: summary="This table has row and column headers. The row headers identify resources. The column headers identify the different types of recovery support. To understand which recovery methods are supported for a resource, go to the row that describes the resource, and find the column for the recovery method that you are interested in."}

You cannot subsequently download files that you add to {{site.data.keyword.discoveryshort}} because the original files are not stored in {{site.data.keyword.discoveryshort}}. However, you can retrieve information from the file that is stored in the collection index when the original file is processed. Use the [Query API](/apidocs/discovery-data#query) to submit a query that will return a passage from the file of interest, and then check the response body for data from the file. For example, for some file types, text from the original file is stored in the `text` field.
{: note}
{: #note-uploaded-crawled-data}

For information about resources that are created with the Content Mining application, see [Content Mining resources](#cm-resources).

### Sentence classifier enrichments
{: #backup-sentence-classifier}

To back up sentence classifier models that were created from the sentence labeling UI, download the models and store them locally. A model must be fully trained before it can be downloaded. For more information, see [Downloading the sentence classifier model](/docs/discovery-data?topic=discovery-data-sentence-classifier#sentence-classifier-download).

### Ingested documents
{: #backupdocs}

Your uploaded documents are converted, enriched, and stored in the search index. If a disaster occurs, the search index is not recoverable. Store a backup of all your source documents in a safe place.

If you also import documents by doing scheduled crawls of external data sources, you might want to retain your data source credentials externally so that you can reestablish the connection to your data sources quickly. For the list of available sources and the credentials that are needed for each one, see [Configuring {{site.data.keyword.cloud_notm}} data sources](/docs/discovery-data?topic=discovery-data-sources).

You can get some of the text that was stored in the index when the original document was ingested by using the Query API. For more information, see [Recovering documents](/docs/discovery-data?topic=discovery-data-migrate-to-v2#migrate-to-v2-advanced-transfer).

### Training data
{: #backuptraining}

Refer to this task to back up your training data queries and examples for a trained project. Training data is used for explicit training of your projects and is stored on a per project basis. To extract the training data, use the API to download the queries and the ratings from {{site.data.keyword.discoveryshort}}. To back up training data queries and examples, complete the following steps:

1. Download your training data by using the [list training queries](https://{DomainName}/apidocs/discovery-data#listtrainingqueries){: external} API.
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

This is not required, but it is a best practice to [retrieve the status](https://{DomainName}/apidocs/discovery-data#getcollection){: external} for each collection regularly and store the information locally. By retaining these statistics, you can later verify that your restoration processes were successful if needed.
{: tip} 

### Smart Document Understanding models
{: #backupsdu}

If you use Smart Document Understanding (SDU), you have models that are associated with your configuration. To avoid loss of this information, [export your models](/docs/discovery-data?topic=discovery-data-configuring-fields#import), back them up, and store them locally. SDU models have the file extension of `.sdumodel`.

### Dictionary enrichments
{: #backupdictionary}

1. Open your project, and click **Improve and customize**.
1. On the **Improvement tools** panel, click **Teach domain concepts** and then **Dictionaries**.
1. Click the download icon next to your dictionary. Your dictionary then downloads as a .csv file.

### Regular expressions enrichments
{: #backupregexpenrich}

Back up your regular expressions as a .csv file, and store them locally. Note the regular expressions that you specified to create your enrichments so that you can re-create the enrichments from them. For more information, see [Regular expressions](/docs/discovery-data?topic=discovery-data-domain-regex).

### Machine learning enrichments
{: #mlenrich}

Back up your machine learning model .zip or .pear files, and store them locally. For more information, see [Machine learning enrichments and Watson Explorer Content Analytics Studio models](/docs/discovery-data?topic=discovery-data-domain-ml).

### Pattern enrichments
{: #patternenrich}

1. Open your project.
1. On the *Improvement tools* panel of the *Improve and customize* page, click **Teach domain concepts** and then **Patterns (Beta)**.
1. Click the download icon next to your pattern. Your pattern model then downloads as a .zip file.

### Advanced rules models enrichment
{: #advrmenrich}

Back up your model files as .zip files, and store them locally. For more information, see [Advanced rules models](/docs/discovery-data?topic=discovery-data-domain-ml#advanced-rules).

### Classifier enrichments
{: #classifierenrich}

Back up your classifier .csv files, and store them locally. For more information, see [Classifier](/docs/discovery-data?topic=discovery-data-domain-classifier).

### Entity extractor enrichments
{: #extractorenrich}

To back up entity extractor models, download the models and store them locally. A model must be fully trained before it can be downloaded. For more information, see [Exporting the entity extractor](/docs/discovery-data?topic=discovery-data-entity-extractor#entity-extractor-export).

## Content Mining application resources
{: #cm-resources}

You cannot back up certain data types and must manually re-create them. There are several Content Mining custom user resources that the application does not automatically back up. If data loss occurs, you must either manually re-create the following custom user resources in the Content Mining application or upload a locally saved file that contains the resource:

-   Custom map
-   Searched document export: You can export a searched document in the **Documents** view in the Content Mining application, but you cannot reupload it in the application.
-   Facet analysis result export: You can download the results of your facet analysis by clicking the **Export** icon, then **Export results**, and **Export** in the **Analysis export options** dialog box.
-   Collection: You can restore a Content Mining collection if you stored the collection locally as a .csv file and then upload it in the application. Otherwise, you must manually re-create the collection.
-   Document classifier: You can restore a document classifier if you stored the document classifier locally as a .csv file and then upload it in the application. Otherwise, you must manually re-create the document classifier.
-   Custom annotators

    -   Dictionary: You can restore a dictionary in the application if you stored the dictionary locally as a .csv file and upload it in the application. 
    -   Regular expressions: You can restore a regular expression in the application if you stored the regular expression locally as a .csv file and upload it in the application.
    -   Machine learning models: You can restore a machine learning model if you stored the model locally as a .zip file and then upload it in the application.
    -   PEAR File: You can upload a .pear file if you stored the file locally and then upload it in the application.

You cannot back up the following resources locally and must recreate them in the Content Mining application.

-   Saved analysis
-   Report
-   Dashboard

## Restoring your data to a new Watson Discovery instance
{: #restoredata}

Consider using your backups to restore to a new {{site.data.keyword.discoveryshort}} instance in a different data center, also known as a region or location.
{: note}

To begin restoration, first start by reviewing your list of collections and associated data sources, as well as your file backups.

-    Create your projects and collections. Use the {{site.data.keyword.discoveryshort}} tooling, or the API. See [Create a project](https://{DomainName}/apidocs/discovery-data#createproject){: external} and [Create a collection](https://{DomainName}/apidocs/discovery-data#createcollection){: external}.
-    Add back stopwords into the collections. See [Defining stopwords](/docs/discovery-data?topic=discovery-data-stopwords). 
-    If you use custom query expansion, add your query expansions. See [Implementing synonyms](/docs/discovery-data?topic=discovery-data-search-settings).
-    If you use any custom entity models from {{site.data.keyword.knowledgestudiofull}} for enrichment, reimport that model into your {{site.data.keyword.discoveryshort}} instance. For details, see [Managing enrichments](/docs/discovery-data?topic=discovery-data-managing-enrichments).

After you set up your projects and collections as they were before, begin ingesting your source documents. Depending upon how you ingested your documents previously, you can do so by using your own solution or one of the following methods:

-   The [API](https://{DomainName}/apidocs/discovery-data#adddocument){: external}
-   A [connector](/docs/discovery-data?topic=discovery-data-sources)

### Restoring sentence classifiers
{: #restore-sentence-classifier}

To restore a sentence classifier model that was created from the sentence labeling UI, import the exported .sc file to create a new machine learning model. You cannot open the exported model in the sentence labeling UI to continue working with it. However, you can import a finished model and apply it to collections as a sentence classifier enrichment.

For more information about how to import a sentence classifier model to create a machine learning enrichment, see [Use imported ML models to find custom terms](/docs/discovery-data?topic=discovery-data-domain-ml).

### Restoring training data
{: #restoretraining}

After you restore your projects, you can begin the process of re-creating your relevancy training models. To restore your training data queries and examples, re-create your individual training queries and the examples by using the [create training query](https://{DomainName}/apidocs/discovery-data#createtrainingquery){: external} API, or you can restore your queries and examples on {{site.data.keyword.discoveryshort}}. For more information about restoring your training data by using {{site.data.keyword.discoveryshort}}, see the instructions for accessing the **Train** page in [Improving result relevance with training](/docs/discovery-data?topic=discovery-data-train).

For the restore to work properly, note that the document IDs that you use in your training data point to the documents in your current project. Use the same IDs in your new projects to ensure that the correct documents are referenced. If the IDs do not match, your restored relevancy training will not work.
{: important}

### Restoring connections to external data sources
{: #restoreconnections}

In case of an unanticipated loss of data, you might lose your scheduled crawls of external data sources. See [Configuring {{site.data.keyword.cloud_notm}} data sources](/docs/discovery-data?topic=discovery-data-sources) for the list of available sources.

To restore your external data, reestablish your connections to these data sources, and then recrawl them.

To find the data source credentials that you stored, follow the instructions for your chosen data source in [Configuring {{site.data.keyword.cloud_notm}} data sources](/docs/discovery-data?topic=discovery-data-sources). These instructions explain how you can reconnect to your data sources and get the data imported into {{site.data.keyword.discoveryshort}}.

### Restoring Smart Document Understanding models
{: #restoresdu}

To import a previously exported Smart Document Understanding (SDU) model, see [Importing and exporting models](/docs/discovery-data?topic=discovery-data-configuring-fields#import). SDU models have the file extension of `.sdumodel`.

When importing an SDU existing model into a new collection, it is a best practice to create the new collection and add one document, then import the model and upload the remainder of your documents.

### Restoring dictionary enrichments
{: #restoredictionary}

1. Open your project.
1. On the *Improvement tools* panel of the *Improve and customize* page, click **Teach domain concepts**, **Dictionaries**, and then **Upload**.
1. In the **Apply dictionary** dialog box, enter a name for your .csv file, select a language, specify the facet path, click **Upload**, and select your dictionary .csv file.
1. Click **Create**.

After you upload dictionary .csv files for recovery, you cannot use the dictionary editor to further edit the terms. If you want to use the dictionary editor, create a dictionary, and manually add the dictionary terms.
{: note}

For information about uploading a dictionary enrichment .csv file, see [Dictionary](/docs/discovery-data?topic=discovery-data-domain-dictionary).

### Restoring pattern enrichments
{: #restorepatternenrich}

You can restore pattern enrichment .zip files as advanced rules models .zip files by completing the following steps:

1. Open your project.
1. On the *Improvement tools* panel of the *Improve and customize* page, click **Teach domain concepts**, **Advanced rules models**, and then **Upload**.
1. In the **Apply advanced rules model** dialog box, enter a name for your .zip file, select a language, specify a result field, click **Upload**, and select your advanced rules models .zip file.
1. Click **Create**.

After you upload pattern model .zip files for recovery, you cannot use the pattern editor to further edit the .zip files.
{: note}

For more information about uploading an advanced rules models .zip file, see [Advanced rules models](/docs/discovery-data?topic=discovery-data-domain-ml#advanced-rules).

### Restoring entity extractors
{: #restoreextractorenrich}

To restore an entity extractor model, import the exported .ent file to create a new machine learning model. You cannot open the exported model in the entity extractor tool to continue working with it. However, you can import a finished model and apply it to collections as an entity extractor enrichment.

For more information about how to import an entity extractor model to create a machine learning enrichment, see [Use imported ML models to find custom terms](/docs/discovery-data?topic=discovery-data-domain-ml).
