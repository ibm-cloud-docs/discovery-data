---

copyright:
  years: 2018, 2024
lastupdated: "2024-08-16"

keywords: IBM, activity tracker, event, security, IBM Cloud Activity Tracker

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}



# Activity tracking events for {{site.data.keyword.discoveryshort}}
{: #at_events}



{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.discoveryshort}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.



As of 28 March 2024, the {{site.data.keyword.at_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.at_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Activity tracking events are the same for both services. For information about migrating from {{site.data.keyword.at_full_notm}} to {{site.data.keyword.logs_full_notm}} and running the services in parallel, see [migration planning](/docs/cloud-logs?topic=cloud-logs-migration-intro).
{: important}























## Viewing activity tracking events for {{site.data.keyword.discoveryshort}}
{: #at-viewing}



You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.





### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}



For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)








## List of events
{: #at_actions}

The following table lists the {{site.data.keyword.discoveryshort}} actions that generate an event.

| Action                           | Description                        |
|----------------------------------|------------------------------------|
| `discovery.analyze-api.read`     | Process text by using the Analyze API. |
| `discovery.autocompletion.read`    | Suggest complete queries based on documents. |
| `discovery.collection-notices.read` | Get notices for a collection. |
| `discovery.collection-training-status.read` | Get the training status of a single-collection training. |
| `discovery.collections.read`       | Read collection annotations. |
| `discovery.content-miner-csv.create`      | Import a CSV file to a Content Mining project. |
| `discovery.content-miner-csv.delete`      | Delete a CSV file from a Content Mining project. |
| `discovery.content-miner-csv.read`        | Get a CSV file from a Content Mining project. |
| `discovery.content-miner-export.create`   | Create a set of exported documents from a Content Mining project. |
| `discovery.content-miner-export.download` | Download exported documents from a Content Mining project. |
| `discovery.content-miner-export.search`   | List sets of exported documents from a Content Mining project. |
| `discovery.content-miner-report.create`   | Create a report from a Content Mining project. |
| `discovery.content-miner-report.delete`   | Delete a report from a Content Mining project. |
| `discovery.content-miner-report.read`     | Get report content from a Content Mining project. |
| `discovery.content-miner-report.update`   | Update report content from a Content Mining project. |
| `discovery.credential.create`      | Create a credential. |
| `discovery.credential.delete`      | Delete a credential. |
| `discovery.credential.read`        | Get a credential, Salesforce objects, or a list of Cloud Object Storage buckets. |
| `discovery.credential.update`      | Update a credential. |
| `discovery.curations.create`       | Create a curated query. |
| `discovery.curations.delete`       | Delete specified curation. |
| `discovery.curations.read`         | List currently configured curation queries. |
| `discovery.curations.update`       | Update existing curated results documents for a specified query. |
| `discovery.dataset.create`         | Create a data set. |
| `discovery.dataset.update`         | Update a data set. |
| `discovery.dataset-notices.read` | Get notices for a data set. |
| `discovery.dictionary.create`      | Create a dictionary. |
| `discovery.dictionary.delete`      | Delete a dictionary. |
| `discovery.dictionary.read`        | Read a dictionary. |
| `discovery.dictionary.update`      | Update a dictionary. |
| `discovery.document.add`           | Add one document. |
| `discovery.document.create`        | Create a document. |
| `discovery.document.delete`        | Delete a document by ID. |
| `discovery.document.read`          | Download a PDF version of a document. |
| `discovery.document.update`        | Update one document by ingesting new or modified content for a document given a document ID, or by changing the label for a specified document ID. |
| `discovery.document-annotation.read` | Read document annotations. |
| `discovery.document-results.read`  | Search collections for relevant documents. |
| `discovery.enrichment.create` | Create an enrichment. |
| `discovery.enrichment.delete` | Delete an enrichment. |
| `discovery.enrichment.read` | Read an enrichment. |
| `discovery.enrichment.update` | Update an enrichment. |
| `discovery.entity-extractor.create` | Create an entity extractor. |
| `discovery.entity-extractor.delete` | Delete an entity extractor. |
| `discovery.entity-extractor.read` | Read an entity extractor. |
| `discovery.entity-extractor.update` | Update an entity extractor. |
| `discovery.entity-extractor.download` | Download an entity extractor model or labeled data. |
| `discovery.event.create`           | Add a click event to a query. |
| `discovery.expansions.create` | Add synonyms to a collection. |
| `discovery.expansions.delete` | Delete synonyms from a collection. |
| `discovery.expansions.read`   | Get synonyms for a collection. |
| `discovery.fields.read`            | Get fields for a collection. |
| `discovery.label.create`           | Create a collection label. |
| `discovery.label.delete`           | Delete one or multiple documents from one or multiple collections based on a label. |
| `discovery.label.read`             | Read a collection label. |
| `discovery.label.update`           | Update a collection label. |
| `discovery.logs.read`              | Get logs for a collection. |
| `discovery.metric.read`            | Request a metric. |
| `discovery.model.export`           | Export a model. |
| `discovery.model.import`           | Import a model. |
| `discovery.multi-collection-training-status.read` | Get the training status of a multi-collection training. |
| `discovery.notices.read`           | Get notices for a collection. |
| `discovery.page.read`              | Read document pages. |
| `discovery.page-annotation.add`    | Add document page annotation. |
| `discovery.page-prediction.read`   | Read document page predictions. |
| `discovery.page-view.read`         | Read document page view. |
| `discovery.project.create` | Create a project. |
| `discovery.project.delete` | Delete a project. |
| `discovery.project-notices.read` | Get notices for a project. |
| `discovery.sentence-labeling.create` | Create a sentence labeling workspace. |
| `discovery.sentence-labeling.delete` | Delete a sentence labeling workspace. |
| `discovery.sentence-labeling.read` | Read a sentence labeling workspace. |
| `discovery.sentence-labeling.update` | Update a sentence labeling workspace. |
| `discovery.sentence-labeling.download` | Download a sentence classifier model or labeled data. |
| `discovery.stopwords.create` | Add stopwords to a collection. |
| `discovery.stopwords.delete` | Delete stopwords from a collection. |
| `discovery.stopwords.read`   | Get stopwords for a collection. |
| `discovery.table-annotation.read`  | Read document page table annotations. |
| `discovery.table-cell.read`        | Read document page table cell. |
| `discovery.user-data.delete`       | Delete all data associated with a customer ID. |
{: caption="Table 1. Actions that generate events" caption-side="top"}




