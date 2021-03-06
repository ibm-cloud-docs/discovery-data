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


# FileNet P8
{: #connector-filenet-cp4d}

Crawl documents that are stored in FileNet P8.
{:shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{:note}

## What documents are crawled
{: #connector-filenet-cp4d-docs}

- Document level security is supported. When this option is enabled, your users can crawl and query the same content that they can access when they are logged in to FileNet. {{site.data.keyword.discoveryshort}} does not support role-based security when you crawl FileNet P8.

   For more information about document level security, see [Supporting document level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).
- When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index.
- All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

## Data source requirements
{: #connector-filenet-cp4d-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements) for all installed deployments, your FileNet P8 data source must meet the following requirements: 

- The data source can crawl FileNet P8 5.5.0 and the Content Engine Web Services (CEWS) of a FileNet server that is installed on {{site.data.keyword.cp4-automation_notm}}. 
- FileNet P8 5.5.0 and FileNet on {{site.data.keyword.cp4-automation_short}} support the HTTP and HTTPS protocols.

## Prerequisite steps
{: #connector-filenet-cp4d-prereq}

If you want to enable document level security, you must take some steps to set it up. For more information, see [About document level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).

## Connecting to a FileNet P8 data source
{: #connector-filenet-cp4d-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **FileNet P8**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents in FileNet is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule. 

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  Complete the following fields in the *Enter your credentials* section:

    - **Content Engine Web Service URL**: The Content Engine web service URL of the IBM FileNet P8 server. 
    
      When you enter the URL, use the format: `<protocol>://<server>:<port>/wsi/FNCEWS40MTOM`. You can use the HTTP or HTTPS protocol. The `<server>` is the hostname of the server where the Content Platform Engine is deployed and the `<port>` is the HTTP port that the application server uses, or where the Content Platform Engine is deployed.
    - **User**: The username to use to crawl the FileNet P8 server. You can obtain your username from your FileNet administrator.
    - **Password**: The password that is associated with the user.
1.  In the *Specify what you want to crawl* section, enter the name of the object store that you want to use to create, search, retrieve, and store documents in the **ObjectStore Name** field.
1.  In **Crawler Space Type**, select either **Folder** or **Class**.
1.  Complete the following field:

    - **Folder subpath or Subclass name**: The subfolder path that you can specify under RootFolder that crawls all documents that belong to the specified folder or the custom subclass of the `Document` class that crawls all documents that belong to the specified class. Before you specify anything in this field, keep in mind the following items:

      - You can specify multiple crawler spaces by using both the `Class` and `Folder` types and crawl the documents belonging to the folder name and class name.
      - You cannot specify a class outside the object store that you defined.
      - No support is available for specifying a class that is a subclass of a `Custom Object` and `Folder`.
1. After you enter one or more paths, click **Add**.
1.  **Optional**: In the *Security* section, if you want to enable document level security, set the **Enable Document Level Security** switch to `On`.
    
      When set to **On**, your users can crawl the same content that they have access to in FileNet.
    1.  If you want the crawler to extract text from images in documents, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    The processing time increases when this feature is enabled.
    {: note}
1. Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection. 

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
