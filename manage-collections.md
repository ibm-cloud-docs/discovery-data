---

copyright:
  years: 2019, 2023
lastupdated: "2022-12-08"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Managing data collections
{: #manage-collections}

<!-- c/s help for the *Manage collections* page tabs: Activity, Processing settings, CSV settings. Do not delete. -->

After the processing of a new data collection is finished, you can see a summary of the settings that are applied to your collection from the *Manage collections* page.
{: shortdesc}

For more information about how to create a collection, see [Creating collections](/docs/discovery-data?topic=discovery-data-collections).

## Managing data
{: #manage-data}

[IBM Cloud]{: tag-ibm-cloud} **{{site.data.keyword.cloud_notm}} only**

This procedure is available in service instances that are managed by {{site.data.keyword.cloud_notm}} only. The *Manage data* page is not available in installed deployments.
{: note}

After you create a collection and the documents in the collection are indexed, you can see a list of the documents from the *Manage data* page.

1.  Open the *Manage collections* page.
1.  Click to open the collection that you want to change.
1.  Click the **Manage data** tab.

    A list of the documents in the collection is displayed.

1.  **Optional**: You can change the information that is displayed.

    To change the fields that are shown in the view, click the *Settings* icon at the start of the view. Choose a different field for the first and second columns, and then click **Apply**.

    For example, you can change the fields in the view to accomplish the following goals:

    -   Get the document ID for a document that you want to work with by using the API.
    -   Find the parent document for a document. Some file types, such as CSV or JSON files, generate subdocuments when they are added to a collection, for example. And splitting a document turns one document into multiple document segments.
    -   Retrieve the original file name for a document.
    -   Find out how many pages are in a document.

    The custom settings that you apply are not retained. The default field settings are shown the next time that you access the page.
    {: note}

1.  **Optional**: You can delete a document from the collection from this page. For more information, see [Excluding content from query results](/docs/discovery-data?topic=discovery-data-hide-data).

## Changing how a data source is processed
{: #collection-change-processing}

You can change settings that were applied to a collection when it was created. You might want to change the schedule at which an external data source is crawled, for example.

To change how a data source is processed, complete the following steps:

1.  Open the *Manage collections* page.
1.  Click to open the collection that you want to change.
1.  Click the **Processing settings** tab.
1.  Make any changes that you want to make to the processing settings.

    For example, you might want to enable or disable optical character recognition (OCR), which is a feature that extracts text from images. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).

    For more information about changing data synchronization schedules, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).

    [IBM Cloud Pak for Data]{: tag-cp4d} For service instances that are managed by {{site.data.keyword.cloud_notm}}, you can enable or disable the FAQ extraction feature. For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction).

    Other setting options differ by data source type.

1.  Click **Apply changes and reprocess**.

## Finding where a collection is used
{: #collection-usage}

<!-- c/s help for the *Collection usage and sharing* page. Do not delete. -->

To find out whether a collection is being shared, open the *My Projects* page, and then complete the appropriate step for your deployment:

- [IBM Cloud Pak for Data]{: tag-cp4d} Click **Collection usage and sharing**.
- [IBM Cloud]{: tag-ibm-cloud} Click **Data usage and GDPR**, and then review the **Collection usage** page.

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

- **GDPR data label** [IBM Cloud Pak for Data]{: tag-cp4d}: For more information about GDPR and labeling data, see [European Union General Data Protection Regulation (GDPR)](/docs/discovery-data?topic=discovery-data-information-security#gdpr).
- **API usage** [IBM Cloud Pak for Data]{: tag-cp4d} For more information about monitoring Analyze API usage, see [Monitoring usage](/docs/discovery-data?topic=discovery-data-analyzeapi#api-usage).

## Deleting collections
{: #collection-delete}

Find out whether a collection is being used anywhere before you delete it from the *Collection usage* page. Unshared collections can be deleted directly from this page.

-   To delete a single collection from a project, open the *Manage collections* page from the navigation panel, find the collection tile, and then click the delete icon.

    Decide whether to keep the underlying data and configuration settings. If you choose to keep the data, you can find the collection in the unshared list on the *Collection usage* page. You might need to wait a few minutes before the collection is displayed.

    Click **Delete from project**.

-   [IBM Cloud Pak for Data]{: tag-cp4d} To delete all of the collections in your environment, select the **Environment details** ![Environment details icon](images/env_icon.png) icon, and then choose **Delete environment**.

    *Environment* refers to the {{site.data.keyword.discoveryshort}} instance that you provisioned in {{site.data.keyword.icp4dfull_notm}}.
    {: tip}

You cannot delete the *Sample Project* collection.
