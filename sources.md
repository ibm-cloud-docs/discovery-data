---

copyright:
  years: 2015, 2023
lastupdated: "2022-09-19"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Overview of IBM Cloud data sources
{: #sources}

<!-- V2 c/s help for the *Select a Collection type* page for IBM Cloud. Do not delete. -->

You can use {{site.data.keyword.discoveryfull}} on the {{site.data.keyword.cloud}} to connect to and crawl documents from remote sources.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} **{{site.data.keyword.cloud_notm}} only**

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

*Your data source isn't listed?* Check whether {{site.data.keyword.appconserviceshort}} has a connector to the data source. You can use a default connector that is built for {{site.data.keyword.appconnect_notm}} to send data from a data source to {{site.data.keyword.discoveryshort}}. For a list of the data sources supported by {{site.data.keyword.appconnect_notm}} default connectors, see [Connectors A-Z](https://www.ibm.com/cloud/app-connect/connectors/){: external}. For more information about integrating {{site.data.keyword.appconnect_notm}} with {{site.data.keyword.discoveryshort}}, see [How to use IBM App Connect with {{site.data.keyword.discoveryfull}}](https://www.ibm.com/support/knowledgecenter/SS6KM6/com.ibm.appconnect.dev.doc/how-to-guides-for-apps/watson-discovery.html){: external}.

To use an {{site.data.keyword.appconnect_notm}} connector, you must create a separate {{site.data.keyword.appconnect_notm}} instance. Costs that are incurred from a paid {{site.data.keyword.appconnect_notm}} instance are not included with the cost of using {{site.data.keyword.discoveryshort}}. Except for indexing, {{site.data.keyword.discoveryshort}} does not support any integration with {{site.data.keyword.appconnect_notm}} that you perform on your own.
{: note}

## Data source requirements
{: #public-requirements}

The following requirements and limitations are specific to {{site.data.keyword.discoveryshort}} on {{site.data.keyword.cloud_notm}}:

-   A collection can connect to only one data source.
-   For more information about size limits, which can differ per plan, see the following topics:

    -   [Collection limits](/docs/discovery-data?topic=discovery-data-collections#collections-limits)
    -   [Document limits](/docs/discovery-data?topic=discovery-data-collections#collections-doc-limits)

## FAQ extraction [IBM Cloud Pak for Data]{: tag-cp4d}
{: #faq-extraction}

The FAQ extraction feature is a beta feature and is not meant for use in production environments. The feature is not supported with Chinese-language collections.
{: beta}

When you configure a data source for any project type, you can enable the **Apply FAQ extraction** feature. This beta feature detects question-and-answer pairs in your documents and automatically extracts the pairs. Your application can use the extracted pairs to provide more precise query results.

Apply FAQ extraction only to a data source with documents that contain frequently asked questions that follow a consistent style. For example, ensure that the questions in the FAQ end with a question mark. The answer must be grouped with the question that it answers. 

FAQ extraction works best with HTML files that are generated from web crawls. It is less effective with crawls that return PDF files.
{: tip}

To turn on FAQ extraction for your data source, expand the *Syncing FAQ Content?* section, and then select **Apply FAQ extraction**.

Each question-and-answer pair in an FAQ document is split into a separate document. The question is stored in a `title` field and the answer is stored as a `text` field. A document with 100 question-and-answer pairs is split into 100 documents. If no question-and-answer pairs are detected in a document, only one document is added to the collection. A maximum of 10,000 pairs per document are allowed. After the limit is reached, any remaining pairs that are found are stored in a single document. You can monitor the document count on the **Activity** tab of the **Manage collections** page.

Remember these notes:

-   If you apply FAQ extraction to a collection, you cannot use the [Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields) tool later to annotate fields.
-   If you delete a question-and-answer pair from a webpage that you crawled previously, the question-and-answer pair that was already indexed in your collection remains in the index.

To learn more about FAQ extraction, see the [Turn your FAQ pages into conversational AI](https://medium.com/ibm-data-ai/turn-your-faq-pages-into-conversational-ai-8ac7ae7ec793){: external} blog post on Medium.

### Disabling FAQ extraction
{: #faq-extraction-diable}

To turn off FAQ extraction, complete the following steps:

1.  Go to the **Processings settings** tab of the **Manage collections** page.
1.  Set the **FAQ extraction** switcher to Off.
1.  Reprocess the collection by clicking **Apply changes and reprocess**.

Currently, when you disable FAQ extraction on collections that contain HTML or TXT files, the question-and-answer pair documents that were generated by FAQ extraction are not deleted. This limitation applies to HTML files that are added to a collection from web crawls, for example. You can find and delete the extraneous documents from the *Manage data* page. For more information, see [Excluding content from query results](/docs/discovery-data?topic=discovery-data-hide-data). To find all of the question-and-answer pair documents that were generated from a single web page, check for documents with the same `segment_metadata.parent_id` field value.
{: important}

## Installing IBM Secure Gateway for on-premises data
{: #gatewaypublic}

<!-- Learn more topic WDS -->
To connect to an on-premises data source, you first need to download, install, and configure {{site.data.keyword.SecureGatewayfull}}.
{: shortdesc}

After you install the client for one on-premises data source, you can reuse it for other data sources in the project.

The number of gateways that you can create is limited to 50.

For more information, see [About Secure Gateway](/docs/SecureGateway?topic=SecureGateway-about-sg){: external}.

You can use the IBM Secure Gateway with the following connectors only:

-   [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cloud#connector-web-cloud-prereq-task)
-   [Microsoft SharePoint On Prem](/docs/discovery-data?topic=discovery-data-connector-sharepoint-onprem-cloud#connector-sharepoint-onprem-cloud-prereq-task)

To install {{site.data.keyword.SecureGatewayfull}}, complete the following steps:

1.  From the data source configuration page, click **Manage connection**.
1.  On the *Download and install Secure Gateway client* page, download the appropriate version of {{site.data.keyword.SecureGatewayfull}}.
1.  After you complete the download, click **Download Secure Gateway and Continue**.
1.  When prompted, enter the **Gateway ID** and **Token** that are displayed.

    For more information, see [Installing the client](/docs/SecureGateway?topic=SecureGateway-client-install).
1.  On the machine where the Secure Gateway Client is running, open the Secure Gateway dashboard at `http://localhost:9003`.
1.  Click **add ACL** on the dashboard, and add the URL of the data source that you want to access to the **Allow access** list.

    For example, hostname: `mycompany.sharepoint.com` or `mycompanywebsite.com` and port: `80`.
1.  Return to {{site.data.keyword.discoveryshort}}, and click **Continue**.

    -   If the connection is successful, a `Connection successful` message is displayed.
    -   If the connection is unsuccessful, open the {{site.data.keyword.SecureGatewayfull}} dashboard, and verify that the endpoints on the **Allow access** list are correct.

## Data source connection and data isolation
{: #source_isolation}

When you connect to external data sources, you reduce the data isolation of your service instance because data in transit between the source and the service cannot be isolated. All other data isolation (at-rest, administration, query) remains in full. All in-flight communication among services and data sources is encrypted with TLS v1.2. The private keys for the TLS certificates are encrypted at rest with AES-256-GCM encryption. The service certificates expire every three years and the certificate revocation lists are updated monthly. All credentials are sent over an encrypted connection that uses TLS v1.2 and are encrypted at rest with AES-256 encryption. Connections to data sources use the secure protocols that are supported by the data sources.

## Viewing collections that are connected to a gateway
{: #gateway-connection}

You can view a list of collections that are connected to a particular gateway. Complete the following steps to view collections that share a particular gateway:

1.  From the **My projects** page, click **Data usage and GDPR**.
1.  Click **On premises**.

    Collections that share a common gateway are displayed in the *Connected collections* list.

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

-   For a list of IP addresses that you can add to an allowlist for services instances that were created before 1 May 2020 (US) and before 21 February 2021 (non-US), see the [network addresses](https://cloud.ibm.com/docs/cloud-foundry-public?topic=cloud-foundry-public-network-address) that are listed for Cloud Foundry.

    -   Refer to the **Dallas** data center IP addresses for all US-hosted service instances.
    -   Refer to the **London** data center IP addresses for all service instances that are hosted outside the US.
