---

copyright:
  years: 2019, 2021
lastupdated: "2021-03-24"

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

Click on any collection on the **Manage collections** page to see the options for managing your collection. These tabs are available after collection processing finishes. The tabs contain data that is associated with your collection and options for managing it.
{: shortdesc}

After the processing of a new data collection is finished, you can see a summary of the settings that are applied to your collection from the *Manage collections* tab.

From this tab, you can learn more about the following things:

- **Activity**: Shows the status of a synchronization, the number of documents that were added to the collection, and whether any documents from the data source were skipped or generated errors as the collection was created and why. ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Shows the time of the next scheduled snychronization.
- **Identify fields**: From this page, you can see the fields that the crawler identified in your data as the data collection was synchronized. For more information, see [Identifying fields](/docs/discovery-data?topic=discovery-data-configuring-fields#identify-fields). If you want {{site.data.keyword.discoveryshort}} to recognize fields based on the style of the source document (H1 equals title), you can start a Smart Document Understanding training session from this page. For more information, see [Configuring your collection with Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields).
- **Manage fields**: Review the fields from the source documents that are being indexed and make any necessary changes. You can also break large documents into multiple smaller documents. For more information, see [Managing fields](/docs/discovery-data?topic=discovery-data-configuring-fields#field-settings).
- **Enrichments**: Review the enrichments that are being applied to the documents to determine if you want to add or remove any enrichments. For more information, see [Creating enrichments](/docs/discovery-data?topic=discovery-data-create-enrichments).
- **Processing settings**: Review the data collection configuration settings that were specified when the data source collection was created. You can make adjustments, such as changing the frequency of synchronizations. If you are uploading data, you can indicate whether you want to to extract text from images by changing the optical character recognition (OCR) setting.
- **CSV settings**: Summarizes the configuration settings that are used when a comma-separated value (CSV) file is processed. You can change these settings, such as how the columns are delimited. You can also specify the character to use to escape quotation marks, by specifying either a quotation mark (`"`) or a backslash (`\`).

## Collection usage and sharing
{: #collection-usage}

<!-- c/s help for the *Collection usage and sharing* page. Do not delete. -->

To access the **Collection usage and sharing** page, open the **Projects** page, then:

  - ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: Select **Data usage**, then **Collection usage and sharing**. 
  - ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Select **Data usage and GDPR**, then **Collection usage and sharing**.

Collections can be:

-  Associated with a single project
-  Shared by two or more projects
-  Not associated with any project. Collections not associated with a project can be deleted.

You can share collections across projects. The following is shared:

- The processed data
- Configured connector

If you make any of the following changes to a shared collection, *those changes will be applied to that collection in every project it is shared with*. These changes include:

-  Changing the **Run OCR (Optical Character Recognition)** setting
-  Annotating fields or adding fields using Smart Document Understanding
-  Enabling/disabling fields
-  Changing the setting for Document splitting
-  Changing any of the connector settings

The enrichments and other improvement tools are not included when a collection is shared, because they are set at the project level.
{: important}

For information about the other tabs, see the following topics:

- **GDPR data label** ![IBM Cloud only](images/ibm-cloud.png): For more information about GDPR and labeling data in the {{site.data.keyword.discoveryshort}} tooling, see [European Union General Data Protection Regulation (GDPR)](/docs/discovery-data?topic=discovery-data-information-security#gdpr).
- **API usage** ![Cloud Pak for Data only](images/desktop.png): For more information about monitoring Analyze API usage, see [Monitoring usage](/docs/discovery-data?topic=discovery-data-analyzeapi#api-usage).