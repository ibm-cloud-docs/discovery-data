---

copyright:
  years: 2015, 2025
lastupdated: "2025-04-07"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Overview of IBM Cloud data sources
{: #sources}



You can use {{site.data.keyword.discoveryfull}} on the {{site.data.keyword.cloud}} to connect to and crawl documents from remote sources.
{: shortdesc}

[IBM Cloud]{: tag-ibm-cloud} **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments. For more information about {{site.data.keyword.icp4dfull_notm}} data sources, see [Overview of Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types).
{: note}

Connect to an external data source so that you can pull documents into {{site.data.keyword.discoveryshort}} on a schedule. {{site.data.keyword.discoveryshort}} pulls documents from the data source by *crawling* the data source. Crawling is the process of systematically browsing and retrieving documents from a starting location that you specify. When the crawler first processes a data source, it performs a full crawl. Each time the crawler runs after the initial crawl, it performs a refresh, where it checks for new and changed files only.

All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.
{: important}

You can use {{site.data.keyword.discoveryshort}} to crawl from the following data sources:

-   [Box](/docs/discovery-data?topic=discovery-data-connector-box-cloud)
-   [IBM Cloud Object Storage](/docs/discovery-data?topic=discovery-data-connector-cos-cloud)
-   [Microsoft SharePoint Online](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cloud)
-   [Microsoft SharePoint On Prem](/docs/discovery-data?topic=discovery-data-connector-sharepoint-onprem-cloud)
-   [Salesforce](/docs/discovery-data?topic=discovery-data-connector-salesforce-cloud)
-   [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cloud)

*Your data source isn't listed?* Check whether {{site.data.keyword.appconserviceshort}} has a connector to the data source. You can use a default connector that is built for {{site.data.keyword.appconnect_notm}} to send data from a data source to {{site.data.keyword.discoveryshort}}. For a list of the data sources supported by {{site.data.keyword.appconnect_notm}} default connectors, see [Connectors A-Z](https://www.ibm.com/cloud/app-connect/connectors/){: external}. For more information about integrating {{site.data.keyword.appconnect_notm}} with {{site.data.keyword.discoveryshort}}, see [How to use IBM App Connect with {{site.data.keyword.discoveryfull}}](https://www.ibm.com/docs/en/app-connect/saas?topic=apps-watson-discovery){: external}.

To use an {{site.data.keyword.appconnect_notm}} connector, you must create a separate {{site.data.keyword.appconnect_notm}} instance. Costs that are incurred from a paid {{site.data.keyword.appconnect_notm}} instance are not included with the cost of using {{site.data.keyword.discoveryshort}}. Except for indexing, {{site.data.keyword.discoveryshort}} does not support any integration with {{site.data.keyword.appconnect_notm}} that you perform on your own.
{: note}

## Data source requirements
{: #public-requirements}

The following requirements and limitations are specific to {{site.data.keyword.discoveryshort}} on {{site.data.keyword.cloud_notm}}:

-   A collection can connect to only one data source.
-   For more information about size limits, which can differ per plan, see the following topics:

    -   [Collection limits](/docs/discovery-data?topic=discovery-data-collections#collections-limits)
    -   [Document limits](/docs/discovery-data?topic=discovery-data-collections#collections-doc-limits)

## Data source connection and data isolation
{: #source_isolation}

When you connect to external data sources, you reduce the data isolation of your service instance because data in transit between the source and the service cannot be isolated. All other data isolation (at-rest, administration, query) remains in full. All in-flight communication among services and data sources is encrypted with TLS v1.2. The private keys for the TLS certificates are encrypted at rest with AES-256-GCM encryption. The service certificates expire every three years and the certificate revocation lists are updated monthly. All credentials are sent over an encrypted connection that uses TLS v1.2 and are encrypted at rest with AES-256 encryption. Connections to data sources use the secure protocols that are supported by the data sources.

## Connecting to data sources with IP restrictions
{: #sources-ip-restrictions}

Some data sources allow crawlers from only a limited number of trusted network addresses or domains to access and process their data. If one of the data sources that you want to connect to limits access in this way, you can add IBM-managed IP addresses to the allowlist of the data source.

Network addresses are subject to change from time to time. You can monitor for updates to these addresses by subscribing to the repo notifications for this page. Click **Edit Topic** and then select **Watching** in the Notifications dialog of the repo.
{: tip}

-   For service instances that are hosted in a US-based data center and that were created on or after 1 May 2020, add the following IP addresses:

    ```text
    150.238.21.0/28
    169.48.255.224/28
    174.36.69.128/28
    ```
    {: screen}

-   For service instances that are hosted in non-US data centers and that were created on or after 21 February 2021, add the following IP addresses:

    ```text
    159.122.203.64/28
    158.175.114.128/28
    158.176.107.48/28
    ```
    {: screen}
    
