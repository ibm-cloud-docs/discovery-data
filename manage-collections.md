---

copyright:
  years: 2019, 2021
lastupdated: "2021-04-13"

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

# Managing data collections
{: #manage-collections}

<!-- c/s help for the *Manage collections* page tabs: Activity, Processing settings, CSV settings. Do not delete. -->

Click any collection on the **Manage collections** page to see the options for managing your collection. These tabs are available after collection processing finishes. The tabs contain data that is associated with your collection and options for managing it.
{: shortdesc}

After the processing of a new data collection is finished, you can see a summary of the settings that are applied to your collection from the *Manage collections* tab.

From this tab, you can learn about the processing settings that are applied to the collection:

- **Activity**: Shows the status of a synchronization and the number of documents that were added to the collection. It also shows whether any documents from the data source were skipped or generated errors as the collection was created and why. ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Shows the time of the next scheduled synchronization.
- **Identify fields**: Shows the fields that the crawler identified in your data as the data collection was synchronized. For more information, see [Identifying fields](/docs/discovery-data?topic=discovery-data-configuring-fields#identify-fields). If you want {{site.data.keyword.discoveryshort}} to recognize fields based on the style of the source document (H1 equals title, for example), you can start a Smart Document Understanding training session. For more information, see [Configuring your collection with Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields).
- **Manage fields**: Review the fields from the source documents that are being indexed and make any necessary changes. You can also break large documents into multiple smaller documents. For more information, see [Managing fields](/docs/discovery-data?topic=discovery-data-configuring-fields#field-settings).
- **Enrichments**: Review the enrichments that are being applied to the documents to determine whether you want to add or remove any enrichments. For more information, see [Applying prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu) and [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain#classifier).
- **Processing settings**: Review the data collection configuration settings that were specified when the data source collection was created. You can make adjustments, such as changing the frequency of synchronizations. If you are uploading data, you can indicate whether you want to extract text from images by changing the optical character recognition (OCR) setting.
- **CSV settings**: Summarizes the configuration settings that are used when a comma-separated value (CSV) file is processed. You can change these settings, such as how the columns are delimited. You can also specify the character to use to escape quotation marks, by specifying either a quotation mark (`"`) or a backslash (`\`).

## Finding where a collection is used
{: #collection-usage}

<!-- c/s help for the *Collection usage and sharing* page. Do not delete. -->

To find out whether a collection is being shared, open the *My Projects* page, and then complete the appropriate step for your deployment:
 
  - ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: Click **Collection usage and sharing**. 
  - ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Click **Data usage and GDPR**, and then review the **Collection usage** page.

Collections can be associated with a single project, shared by two or more projects, or not associated with any project.

When you share collections across multiple projects, the following resources are shared:

- The processed data
- Configured connector

If you make any of the following changes to a shared collection, the changes are applied to the collection in every project where it is shared:

-  Changing the Optical Character Recognition (OCR) setting
-  Annotating fields or adding fields by using Smart Document Understanding
-  Enabling or disabling fields
-  Changing the setting for document splitting
-  Changing any of the connector settings

Enrichments and improvement tool settings are not included when a collection is shared because they are set at the project level.
{: important}

For more information about the other tabs, see the following topics:

- **GDPR data label** ![IBM Cloud only](images/ibm-cloud.png): For more information about GDPR and labeling data, see [European Union General Data Protection Regulation (GDPR)](/docs/discovery-data?topic=discovery-data-information-security#gdpr).
- **API usage** ![Cloud Pak for Data only](images/desktop.png): For more information about monitoring Analyze API usage, see [Monitoring usage](/docs/discovery-data?topic=discovery-data-analyzeapi#api-usage).

## Deleting collections
{: #collection-delete}

Find out whether a collection is being used anywhere before you delete it from the *Collection usage* page. Unshared collections can be deleted directly from this page.

- To delete a single collection from a project, open the *Manage collections* page from the navigation panel, find the collection tile, and then click the delete icon. 

  Decide whether to keep the underlying data and configuration settings. If you choose to keep the data, you can find the collection in the unshared list on the *Collection usage* page. You might need to wait a few minutes before the collection is displayed.
  
  Click **Delete from project**.

- ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: To delete all of the collections in your environment, select the **Environment details** ![Environment details icon](images/env_icon.png) icon, and then choose **Delete environment**.

  *Environment* refers to the {{site.data.keyword.discoveryshort}} instance that you provisioned in {{site.data.keyword.icp4dfull_notm}}.
  {: tip}
