---

copyright:
  years: 2015, 2025
lastupdated: "2025-04-07"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Microsoft SharePoint On Prem
{: #connector-sharepoint-onprem-cloud}

Crawl documents that are stored in a Microsoft SharePoint data source that is hosted on premises.
{: shortdesc}

[IBM Cloud]{: tag-ibm-cloud} **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments. For more information about connecting to an on-premises SharePoint data source from an installed deployment, see [SharePoint On Prem](/docs/discovery-data?topic=discovery-data-connector-sharepoint-onprem-cp4d).
{: note}

## What documents are crawled
{: #connector-sharepoint-onprem-cloud-objects}

During the initial crawl of the content, documents from all of the objects that can be accessed from the site collection path that you specify are crawled and added to your collection. Custom metadata that is associated with the SharePoint content is crawled also. You can crawl one site collection path per collection. You cannot crawl *Personal SiteCollections*.

During subsequent scheduled recrawls, only new and modified documents are crawled and any changes are reflected in your collection. Documents that are deleted from the external data source are not deleted from the collection.

All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

The following table illustrates the objects that {{site.data.keyword.discoveryshort}} can crawl.

| Data source | Objects that are crawled |
|-------------|--------------------------|
| Microsoft SharePoint On Prem | SiteCollections, Sites, SubSites, Lists, List Items, Document Libraries, List Item Attachments |
{: caption="Data sources crawling support" caption-side="top"}

## Data source requirements
{: #connector-sharepoint-onprem-cloud-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-sources#public-requirements) for all managed deployments, your SharePoint On Prem data source must meet the following requirements:

- You can connect to a SharePoint 2013, 2016, or 2019 on-premises data source.
- The user ID must have `SiteCollection Administrator` permission and be able to access all of the sites and lists that they want to crawl.
- The crawler supports Windows New Technology LAN Manager (NTLM) v1 authentication only. It does not support NTLM v2 or Security Assertion Markup Language (SAML) authentication.

## What you need before you begin
{: #connector-sharepoint-onprem-cloud-prereqs}

You must have the following information ready. If you don't know it, ask your SharePoint administrator to provide the information or consult the [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}:

Username
:   The username to use to connect to the SharePoint On Prem web application that you want to crawl. For example, `siteadmin01`.

Password
:   The password to connect to the SharePoint On Prem web application that you want to crawl. This value is never returned and is only used when credentials are created or modified.

Web Application URL
:   The SharePoint web application URL. For example, `https://sharepointwebapp.com:8443`. If you do not enter a port number, the default value of `80` is used for an HTTP URL and `443` for HTTPS.

Domain
:   The domain name of the SharePoint On Prem account. For example, `sharepoint.mycointernal`.

## Limitations
{: #connector-sharepoint-limitation}

{{site.data.keyword.discoveryshort}} can connect only to SharePoint on-prem servers that {{site.data.keyword.cloud_notm}} is able to access without any gateways.

## Connecting to the data source
{: #connector-sharepoint-onprem-cloud-task}

To configure the Microsoft SharePoint On Prem data source, complete the following steps in {{site.data.keyword.discoveryshort}}:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click the link next to the **Need to connect to a data source**? field, click **SharePoint On Prem**, and then click **Next**.
1.  Add values to the following fields:

    -   Username
    -   Password
    -   Web Application URL
    -   Domain

    Click **Next**.
1.  Name the collection.
1.  If the language of the documents on the site is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).

1.  If you want to limit the types of files to add to the collection, you can list the file extensions for file types to either include or exclude.

    When you choose to list extensions for file types to exclude, you must add at least one file extension.
    {: important}

    For a list of supported file types, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).

1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
