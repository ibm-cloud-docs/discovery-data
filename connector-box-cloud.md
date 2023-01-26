---

copyright:
  years: 2015, 2023
lastupdated: "2022-07-21"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Box
{: #connector-box-cloud}

Crawl documents that are stored in a Box data source.
{: shortdesc}

[IBM Cloud]{: tag-ibm-cloud} **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments. For more information about connecting to Box from an installed deployment, see [Box](/docs/discovery-data?topic=discovery-data-connector-box-cp4d).
{: note}

## What documents are crawled
{: #connector-box-cloud-objects}

During the initial crawl of the content, documents from all of the folders that can be accessed from your Box application are crawled and added to your collection. Box notes are stored in JSON format, so {{site.data.keyword.discoveryshort}} also ingests any Box notes in the specified folders.

The following table illustrates the objects that {{site.data.keyword.discoveryshort}} can crawl.

| Data source | Supports scheduled document refreshes? | Objects that are crawled |
|-------------|----------------------------------------|--------------------------|
| Box (**App access**) | No | Files, folders |
| Box (**Enterprise access**)  | Yes (New and modified documents only) | Files, folders |
{: caption="Table 1. Data sources crawling support" caption-side="top"}

Documents that are deleted from Box are not deleted from the collection.

All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

## Data source requirements
{: #connector-box-cloud-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-sources#public-requirements) for all managed deployments, your Box data source must meet the following requirement:

You must obtain any required service licenses for the data source that you want to connect to. For more information about licenses, contact the system administrator of the data source.

## Prerequisite step
{: #connector-box-cloud-prereq-task}

You must create a custom application in Box before you can connect to Box from {{site.data.keyword.discoveryshort}}.

1.  In Box, create a custom app that uses *Server Authentication with JWT* as its authentication method.

    For detailed steps, see [Setup with JWT](https://developer.box.com/guides/authentication/jwt/jwt-setup/){: external} in the Box Developer Documentation.

Follow these guidelines when you create the app:

-   During the setup procedure, choose to use the *Server Authentication with JWT* method to verify application identity with a key pair.
-   When you configure the custom app, you can choose to use one of the application access levels:

    -   App access only
    -   App access plus Enterprise access

    Refreshing documents on a schedule is supported only when you choose **App access plus Enterprise access**. If you set up the connection with **App access**, new and modified documents are not crawled during a refresh.
    {: important}

    -   If you are an administrator, configure **App access plus Enterprise access**. Otherwise, you can configure the app to have **App access**. However, you must get application approval from a Box administrator.

    -   For both application access levels, specify the following settings:

    -   Choose the following scopes:

        -   *Read all folders stored in Box*
        -   *Write all folders stored in Box*
        -   *Manage Users*

        **For apps with Enterprise access only**: Add this extra scope:

        - *Manage Enterprise Properties*
    -   Enable the following advanced features:

        -   *Make API calls using the as-user header*
        -   *Generate User Access Tokens*

-   Get the custom app authorized by an administrator.

    For more information, see [App approval](https://developer.box.com/guides/authorization/custom-app-approval/){: external} in the Box Developer Documentation.
-   After the app is created, authorized, and authentication is configured, download the app settings as a JSON file from the dev console.

    You provide the following information from this file when it is requested later:

    -   `client_id`
    -   `enterprise_id`
    -   `client_secret`
    -   `public_key_id`
    -   `private_key`
    -   `passphrase`

## Connecting to the Box data source
{: ##connector-box-cloud-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Box**, and then click **Next**.
1.  Refer to the values from the Box app settings JSON file that you downloaded during the previous procedure to complete the following fields:

    Client ID
    :   The private key that you specify when you configure your Box app.
    
    Client Secret
    :   The client secret that you specify when you configure your Box app.
    
    Enterprise ID
    :   The enterprise ID of the Box account.
    
    Public Key ID
    :   The public key ID that Box generates.
    
    Private Key
    :   A part of the key pair that is generated to interact with the Box website.
    
    Passphrase
    :   The passphrase that is required to decrypt the private key if the private key is an encrypted file.

1.  Click **Next**.
1.  Name the collection.
1.  If the language of the documents in Box is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  Choose the folders that you want to crawl.
1.  If you want to look for and extract question-and-answer pairs, select **Apply FAQ extraction**.

    For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction).

1.  If you want the web crawl to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
