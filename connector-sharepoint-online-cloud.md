---

copyright:
  years: 2015, 2021
lastupdated: "2021-06-04"

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

# Microsoft SharePoint Online
{: #connector-sharepoint-online-cloud}

Crawl documents that are stored in a Microsoft SharePoint Online data source.
{: shortdesc}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments. For more information about {{site.data.keyword.icp4dfull_notm}} data sources, see [Configuring Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types).
{: note}

## What documents are crawled
{: #connector-sharepoint-online-cloud-objects}

During the initial crawl of the content, documents from all of the objects that can be accessed from the site collection path that you specify are crawled and added to your collection. Custom metadata that is associated with the SharePoint content is crawled also. You can crawl one site collection path per collection. You cannot crawl *Personal SiteCollections*.

During subsequent scheduled recrawls, only new and modified documents are crawled and any changes are reflected in your collection. Documents that are deleted from the external data source are not deleted from the collection.

All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

The following table illustrates the objects that {{site.data.keyword.discoveryshort}} can crawl.

| Data source | Objects that are crawled |
|-------------|----------------------------------------|--------------------------|
| Microsoft SharePoint Online | SiteCollections, Sites, SubSites, Lists, List Items, Document Libraries, List Item Attachments |
{: caption="Table 1. Data sources crawling support" caption-side="top"}

## Data source requirements
{: #connector-sharepoint-online-cloud-reqs}

- The Site Collection that you connect to must be part of an Enterprise (E1) plan or higher.
- You must have an Azure Active Directory user ID with the format `<username>@<domain>.onmicrosoft.com` that has permission to access all of the objects that you want to crawl. The user ID does not need `SiteCollection Administrator` permission.
- Unless you created your SharePoint Online account before January 2020, two-factor authentication is enabled for the account by default. You must disable two-factor authentication.

    To view and change your multifactor authentication status, see [View the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#view-the-status-for-a-user){: external} or [Change the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#change-the-status-for-a-user){: external}.
- The crawl user account must have legacy authentication and `Contribute` level permissions enabled.

  To enable legacy authentication, go to the [Azure portal](https://portal.azure.com/){: external} or contact your SharePoint administrator.

## What you need before you begin
{: #connector-sharepoint-online-cloud-prereqs}

You must have the following information ready. If you don't know it, ask your SharePoint administrator to provide the information or consult the [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}:

- **Username**: The username of the user account to use to connect to the SharePoint Online SiteCollection that you want to crawl.
  For example, `<janedoe>@exampledomain.onmicrosoft.com`.
- **Password**: The password to connect to the SharePoint Online SiteCollection that you want to crawl. 

  This value is never returned and is only used when credentials are created or modified.
- **Organization URL**: The root URL of the source that you want to crawl. Specify the domain name of the URL, for example `https://<company>.<domain>.com`.
- **Site collection path**: The `site_collection_path` to the section of the site where you want to start the crawl. 

  For example, if the content that you want to crawl is available from `https://<company>.<domain>.com/sites/test`, then you can specify `https://<company>.<domain>.com` as the Organization URL and `/sites/test` as the Site collection path. 

  - You cannot specify folder paths as input.
  - You cannot specify a path to an Active Server Page Extended (ASPX) file, such as URLs to document libraries, lists, and subsites.
  - If you don't specify a path, the default value of `/` is used, and the root site collection is crawled.

## Connecting to the data source
{: #connector-sharepoint-online-cloud-task}

To configure the Microsoft SharePoint Online data source, complete the following steps in {{site.data.keyword.discoveryshort}}:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **SharePoint Online**, and then click **Next**.
1.  Add values to the following fields:

    - Username
    - Password
    - Organization URL
    - Site collection path

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