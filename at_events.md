---

copyright:
  years: 2021, 2024
lastupdated: "2024-01-15"

keywords: IBM, activity tracker, event, security, IBM Cloud Activity Tracker

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Activity Tracker events
{: #at_events}

As a security officer, auditor, or manager, you can use the Activity Tracker service to track how users and applications interact with the {{site.data.keyword.discoveryshort}} service in {{site.data.keyword.cloud}}.
{: shortdesc}

[IBM Cloud]{: tag-ibm-cloud}

This information applies only to managed deployments.
{: note}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the [getting started tutorial for {{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started){: external}.

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

## Viewing events
{: #at_ui}

Events that are generated by an instance of the {{site.data.keyword.discoveryshort}} service are automatically forwarded to the {{site.data.keyword.at_full_notm}} service instance that is available in the same location.

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the same location where your service instance is available.

To open the {{site.data.keyword.cloud_notm}} dashboard, click the user icon in the page header, and then click **{{site.data.keyword.cloud_notm}} dashboard**. ![User avatar icon](images/user--avatar.svg)

For more information about how to open {{site.data.keyword.at_full_notm}} from the dashboard, see [Navigating to the UI](/docs/activity-tracker?topic=activity-tracker-launch){: external}.

