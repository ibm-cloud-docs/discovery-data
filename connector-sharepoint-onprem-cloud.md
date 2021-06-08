---

copyright:
  years: 2015, 2021
lastupdated: "2021-06-07"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:beta: .beta}
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

# Microsoft SharePoint OnPrem
{: #connector-sharepoint-onprem-cloud}

Crawl documents that are stored in a Microsoft SharePoint data source that is hosted on premises.
{: shortdesc}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments. For more information about {{site.data.keyword.icp4dfull_notm}} data sources, see [Configuring Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types).
{: note}

## What documents are crawled
{: #connector-sharepoint-onprem-cloud-objects}

During the initial crawl of the content, documents from all of the objects that can be accessed from the site collection path that you specify are crawled and added to your collection. Custom metadata that is associated with the SharePoint content is crawled also. You can crawl one site collection path per collection. You cannot crawl *Personal SiteCollections*.

During subsequent scheduled recrawls, only new and modified documents are crawled and any changes are reflected in your collection. Documents that are deleted from the external data source are not deleted from the collection.

All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

The following table illustrates the objects that {{site.data.keyword.discoveryshort}} can crawl.

| Data source | Objects that are crawled |
|-------------|--------------------------|
| Microsoft SharePoint OnPrem | SiteCollections, Sites, SubSites, Lists, List Items, Document Libraries, List Item Attachments |
{: caption="Table 1. Data sources crawling support" caption-side="top"}

## Data source requirements
{: #connector-sharepoint-onprem-cloud-reqs}

- You can connect to a SharePoint 2013, 2016, or 2019 on-premises data source.
- The user ID must have `SiteCollection Administrator` permission and be able to access all of the sites and lists that they want to crawl.

## What you need before you begin
{: #connector-sharepoint-onprem-cloud-prereqs}

You must have the following information ready. If you don't know it, ask your SharePoint administrator to provide the information or consult the [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}:

- **Username**: The username to use to connect to the SharePoint OnPrem web application that you want to crawl. For example, `siteadmin01`.
- **Password**: The password to connect to the SharePoint OnPrem web application that you want to crawl. 

  This value is never returned and is only used when credentials are created or modified.
- **Web Application URL**: The SharePoint web application URL. For example, `https://sharepointwebapp.com:8443`. 

  If you do not enter a port number, the default value of `80` is used for an HTTP URL and `443` for HTTPS.
- **Domain**: The domain name of the SharePoint OnPrem account. For example, `sharepoint.mycointernal`.

## Prerequisite step
{: #connector-sharepoint-onprem-cloud-prereq-task}

Before you can connect to a SharePoint OnPrem data source, you must install and configure {{site.data.keyword.SecureGatewayfull}}. 

For more information, see [Installing IBM Secure Gateway for on-premises data](/docs/discovery-data?topic=discovery-data-sources#gatewaypublic).

## Connecting to the data source
{: #connector-sharepoint-onprem-cloud-task}

To configure the Microsoft SharePoint OnPrem data source, complete the following steps in {{site.data.keyword.discoveryshort}}:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **SharePoint OnPrem**, and then click **Next**.
1.  Add values to the following fields:

    - Username
    - Password
    - Web Application URL
    - Domain

    Click **Next**.
1.  Name the collection.
1.  If the language of the documents on the site is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  If you want to look for and extract question-and-answer pairs, select **Apply FAQ extraction**.

    For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction).

1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    The processing time increases when this feature is enabled.
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection. The Activity page shows the results after the data source is crawled and the data is processed.