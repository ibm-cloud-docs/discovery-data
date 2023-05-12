---

copyright:
  years: 2020, 2023
lastupdated: "2023-05-12"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Choosing a deployment solution
{: #cloud-v-data}

{{site.data.keyword.discoveryshort}} is available both as a service that is hosted by {{site.data.keyword.cloud_notm}} and as a service that you install on {{site.data.keyword.icp4dfull_notm}}. Learn about these deployment solutions and how they differ.
{: shortdesc}

The product user interface and APIs are mostly equivalent regardless of whether you use the managed or installed version of the service. The few differences between the two solutions include:

-   How you deploy and set up the service
-   The underlying technology that is used to crawl data sources
-   Limits for things like the maximum number of documents and enrichments or file sizes
-   Who to contact for support and how you share product feedback

Although the documentation that describes how to use the product is the same (what you're reading now), more documentation about how to install and administer the service in {{site.data.keyword.icp4dfull_notm}} is available from the [{{site.data.keyword.icp4dfull_notm}} product documentation](https://www.ibm.com/docs/cloud-paks/cp-data){: external} that is hosted in IBM Documentation.

To keep up with product changes, check the following topics periodically:

-   [IBM Cloud Pak for Data]{: tag-cp4d} [Release notes for {{site.data.keyword.icp4dfull_notm}} service instances](/docs/discovery-data?topic=discovery-data-release-notes-data)
-   [IBM Cloud]{: tag-ibm-cloud} [Release notes for {{site.data.keyword.cloud_notm}} service instances](/docs/discovery-data?topic=discovery-data-release-notes)

## Comparing features
{: #cloud-v-data-comparison}

The following table describes the feature support differences between the two deployment types.

The features that are listed in the {{site.data.keyword.cloud_notm}} column apply to service instances that are deployed from {{site.data.keyword.icp4dfull_notm}} as a Service also.
{: note}

| Feature | {{site.data.keyword.cloud_notm}} | {{site.data.keyword.icp4dfull_notm}} |
|---------|----------------------------------|--------------------------------------|
| Crawl the local file system, Window file system, databases, LDAP directories, FileNet P8, and HCL Notes | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Schedule crawls with more precision | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Apply document-level security to crawled collections | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Enable JavaScript execution for web pages that you want to crawl | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Crawl {{site.data.keyword.cos_full_notm}} | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Preview .pdf files that are crawled from external data sources | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Build custom crawlers | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Use {{site.data.keyword.appconnect_notm}} to crawl other external data sources | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Apply answer finding to search queries |  ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Optical Character Recognition v2 | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Patterns enrichment | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| App switcher menu where you can get service instance information and usage statistics | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Import and apply UIMA text analysis models created in Watson Explorer Content Analytics Studio | | ![checkmark icon](../../icons/checkmark-icon.svg) |
| Monitor usage with activity tracker events | ![checkmark icon](../../icons/checkmark-icon.svg) | |
| Monitor usage of the Analyze API from the product user interface | | ![checkmark icon](../../icons/checkmark-icon.svg) |
{: row-headers}
{: class="comparison-table"}
{: caption="Feature support details" caption-side="top"}
{: summary="This table has row and column headers. The row headers identify features. The column headers identify the different deployment types of the product. To understand which features are supported by a deployment type, go to the row that describes the feature, and then find the column for the deployment type that you are interested in."}
