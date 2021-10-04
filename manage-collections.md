---

copyright:
  years: 2019, 2021
lastupdated: "2021-10-04"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Managing data collections
{: #manage-collections}

<!-- c/s help for the *Manage collections* page tabs: Activity, Processing settings, CSV settings. Do not delete. -->

After the processing of a new data collection is finished, you can see a summary of the settings that are applied to your collection from the *Manage collections* page.
{: shortdesc}

From this page, you can access the following tabs:

- **Activity**: Shows the status of a synchronization and the number of documents that were added to the collection. It also shows whether any documents from the data source were skipped or generated errors as the collection was created and why. ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Shows the time of the next scheduled synchronization.
- **Identify fields**: To teach {{site.data.keyword.discoveryshort}} to recognize fields based on the structure of the source document (H1 equals title, for example), apply a Smart Document Understanding model or use the Smart Document Understanding tool to train a model by annotating documents. For more information, see [Using Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields).
- **Manage fields**: Review the fields from the source documents that are being indexed and make any necessary changes. For more information, see [preventing content from being returned](/docs/discovery-data?topic=discovery-data-hide-data). You can also break large documents into multiple smaller documents. For more information, see [Split documents to make query results more succinct](/docs/discovery-data?topic=discovery-data-split-documents).
- **Enrichments**: Review the enrichments that are being applied to the documents to determine whether you want to add or remove any enrichments. For more information, see [Applying prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu) and [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain#classifier).
- **Processing settings**: Review the data collection configuration settings that were specified when the data source collection was created. You can make adjustments, such as changing the frequency of synchronizations. If you are uploading data, you can indicate whether you want to extract text from images by changing the optical character recognition (OCR) setting.
- **CSV settings**: Summarizes the configuration settings that are used when a comma-separated value (CSV) file is processed. You can change these settings, such as how the columns are delimited. You can also specify the character to use to escape quotation marks, by specifying either a quotation mark (`"`) or a backslash (`\`).

For more information about how to create a collection, see [Creating collections](/docs/discovery-data?topic=discovery-data-collections).

## Changing how a data source is processed
{: #collection-change-processing}

You can change settings that were applied to a collection when it was created. You might want to change the schedule at which an external data source is crawled, for example. Or you might want to apply or remove a process, such as optical character recognition (OCR), after using the collection for a while.

To change how a data source is processed, complete the following steps:

1.  Open the *Manage collections* page.
1.  Click to open the collection that you want to change.
1.  Click the **Processing settings** tab.
1.  Make any changes that you want to make to the processing settings.

    The setting options differ by data source type.

    For more information about changing data synchronization schedules, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  Click **Apply changes and reprocess**.

## Finding where a collection is used
{: #collection-usage}

<!-- c/s help for the *Collection usage and sharing* page. Do not delete. -->

To find out whether a collection is being shared, open the *My Projects* page, and then complete the appropriate step for your deployment:

- ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: Click **Collection usage and sharing**.
- ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Click **Data usage and GDPR**, and then review the **Collection usage** page.

Collections can be associated with a single project, shared by two or more projects, or not associated with any project.

## Reusing data from a collection
{: #manage-collections-reuse}

When you share collections across multiple projects, the following resources are shared:

- The processed data
- Configured connector

If you make any of the following changes to a shared collection, the changes are applied to the collection in every project where it is shared:

- Changing the Optical Character Recognition (OCR) setting
- Annotating fields or adding fields by using Smart Document Understanding
- Enabling or disabling fields
- Changing the setting for document splitting
- Changing any of the connector settings

Enrichments and improvement tool settings are not included when a collection is shared because they are set at the project level.
{: important}

For more information about the other tabs, see the following topics:

- **GDPR data label** ![IBM Cloud only](images/ibm-cloud.png): For more information about GDPR and labeling data, see [European Union General Data Protection Regulation (GDPR)](/docs/discovery-data?topic=discovery-data-information-security#gdpr).
- **API usage** ![Cloud Pak for Data only](images/desktop.png): For more information about monitoring Analyze API usage, see [Monitoring usage](/docs/discovery-data?topic=discovery-data-analyzeapi#api-usage).

## Deleting collections
{: #collection-delete}

Find out whether a collection is being used anywhere before you delete it from the *Collection usage* page. Unshared collections can be deleted directly from this page.

-   To delete a single collection from a project, open the *Manage collections* page from the navigation panel, find the collection tile, and then click the delete icon.

    Decide whether to keep the underlying data and configuration settings. If you choose to keep the data, you can find the collection in the unshared list on the *Collection usage* page. You might need to wait a few minutes before the collection is displayed.

    Click **Delete from project**.

-   ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: To delete all of the collections in your environment, select the **Environment details** ![Environment details icon](images/env_icon.png) icon, and then choose **Delete environment**.

    *Environment* refers to the {{site.data.keyword.discoveryshort}} instance that you provisioned in {{site.data.keyword.icp4dfull_notm}}.
    {: tip}
