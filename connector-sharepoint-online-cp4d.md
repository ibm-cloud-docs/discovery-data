---

copyright:
  years: 2019, 2021
lastupdated: "2021-06-15"

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
{:external: target="_blank" .external}


# SharePoint Online
{: #connector-sharepoint-online-cp4d}

Crawl documents that are stored in an online Microsoft SharePoint data source.
{:shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments. For more information about connecting to an online Sharepoint site from a managed deployment, see [Sharepoint Online](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cloud).
{:note}

## What documents are crawled
{: #connector-sharepoint-online-cp4d-docs}

- Crawling non-root site collections is not supported. You can crawl root site collections only.
- Only documents that are supported by {{site.data.keyword.discoveryshort}} are crawled; all others are ignored. For more information, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
- Document level security is supported. When this option is enabled, your users can crawl and query the same content that they can access when they are logged in to SharePoint. For more information, see [Supporting document level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).
- When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index.
- All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

## Data source requirements
{: #connector-sharepoint-online-cp4d-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements) for all installed deployments, your SharePoint Online data source must meet the following requirements:

- You must have site collection administrator permission.
- You must obtain any required service licenses for the data source that you want to connect to. For more information about licenses, contact the system administrator of the data source.

For more information about SharePoint Online, see [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}.

## Prerequisite steps
{: #connector-sharepoint-online-cp4d-prereq}

If you want to enable document level security, you must take some steps to set it up. For more information, see [About document level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls). Also, you must egister your application with SharePoint.

### Registering with SharePoint Online
{: #connector-sharepoint-online-cp4d-register}

If you plan to enable document level security, you must register your app with SharePoint Online. 

To register your app, complete the following steps:

1.  Log in to the Microsoft Azure Portal using the administrator account that you plan to connect to. The username has the syntax `<admin_user>@<domain>.onmicrosoft.com`. 
1.  Follow the instructions to register your app on the Azure Portal from the Microsoft documentation. For more information, see [Register an application with the Microsoft identity platform](https://docs.microsoft.com/en-us/graph/auth-register-app-v2){: external}. Set the client type as a public client.
1.  Make a note of the Azure application (client) ID that is assigned to your app when you register it. 
1.  Check that the required APIs and API permissions are configured.

    For more information about configuring the list of statically requested permissions for an application, see [Using the admin consent endpoint](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent#using-the-admin-consent-endpoint){: external}. 
    
The following table lists the permissions to set for the required APIs:

| API  | Permissions | Type   |                           
| --------------- | ------------------------------- | ------------- |
| Microsoft Graph (Groups) | `Group.Read.All` or `Group.ReadWrite.All` | Delegated |
| Microsoft Graph (Directories) | `Directory.AccessAsUser.All` or `Directory.Read.All` or `Directory.ReadWrite.All` | Delegated | 
| SharePoint Online | `User.Read.All` or `User.ReadWrite.All` | Delegated |
{: caption="Project type use cases" caption-side="top"}

For more information on how to register an app or how to grant permissions, see [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}.

## Connecting to a SharePoint Online data source
{: #connector-sharepoint-online-cp4d-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Sharepoint Online**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents in SharePoint is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule. 

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1. In the *Enter your credentials* section, complete the following fields:

    - **Username**: The username of the SharePoint user with access to all sites and lists that need to be crawled and indexed, for example `<crawl_username>@<company_name>.onmicrosoft.com`.
    - **Password**: The password of the SharePoint user. 
    
      This value is never returned and is used only when you create or modify credentials.
1. In *Specify what you want to crawl* section, add values to the following fields:

    - **Site Collection Url**: The SharePoint web service URL. For example, `https://<organization_name>.com`.
    - **Site Collection Name**: Specify the name that the site collection uses. Get the name from the site collection settings. 
1.  **Optional**: If you are using a proxy server to access the data source server, then in the *Proxy settings* section, set the **Enable proxy settings** switch to `On`. Add values to the following fields:

    - **Username**: Optional: The proxy server username to authenticate, if the proxy server requires authentication. If you do not know your username, you can obtain it from the administrator of your proxy server.
    - **Password**: Optional: The proxy server password to authenticate, if the proxy server requires authentication. If you do not know your password, you can obtain it from the administrator of your proxy server.
    - **Proxy server host name or IP address**: The hostname or the IP address of the proxy server.
    - **Proxy server port number**: The network port that you want to connect to on the proxy server.
1.  **Optional**: If you want to activate document level security, in the *Security* section, set the **Enable Document Level Security** switch to `On`. 

    When this option is enabled, your users can crawl and query the same content that they can access when they are logged in to SharePoint. For more information, see [Supporting document level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).
    
    When you enable this option, you must add the Azure ID that was assigned to the application upon registration to the **Application ID** field.
    
    To enable document level security, you must register your application with SharePoint. For more information, see [Registering with SharePoint Online](#connector-sharepoint-online-cp4d-register).
1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    The processing time increases when this feature is enabled.
    {: note}
1. Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection. 

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.