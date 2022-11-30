---

copyright:
  years: 2019, 2022
lastupdated: "2022-10-17"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Box
{: #connector-box-cp4d}

Crawl documents that are stored in a Box data source.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments. For more information about connecting to Box from a managed deployment, see [Box](/docs/discovery-data?topic=discovery-data-connector-box-cloud).
{: note}

## What documents are crawled
{: #connector-box-cp4d-docs}

- Only documents that are supported by {{site.data.keyword.discoveryshort}} in your Box folders are crawled; all others are ignored. For more information, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
- Document-level security is supported only for connectors that are configured to use the *App + Enterprise Access* as the Box application's app access level. When this option is enabled, your users can crawl and query the same content that they can access when they are logged in to Box. For more information, see [Supporting document-level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).
- When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index.
- All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.
- Box notes are stored in JSON format, so {{site.data.keyword.discoveryshort}} also ingests any Box notes in the specified folders.

## Data source requirements
{: #connector-box-cp4d-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements) for all installed deployments, your Box data source must meet the following requirement:

- You must obtain any required service licenses for the data source that you want to connect to. For more information about licenses, contact the system administrator of the data source.

## Prerequisite steps
{: #connector-box-cp4d-prereq}

If you want to enable document-level security, you must take some steps to set it up. For more information, see [About document-level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).

You must create a custom application in Box before you can connect to Box from {{site.data.keyword.discoveryshort}}. Anyone can create the custom app, but only a Box administrator can authorize it.

To create a custom application, complete the following steps:

1.  Make sure you have a [Box account](https://www.box.com/){: external}. During this process, you get the configuration file and the client ID.

1.  Next, create a custom app that uses *Server Authentication with JWT* as its authentication method.

    For detailed steps, see [Setup with JWT](https://developer.box.com/guides/authentication/jwt/jwt-setup/){: external} in the Box Developer Documentation.

    Follow these guidelines when you create the app:

    1.  During the setup procedure, choose to use the *Server Authentication with JWT* method to verify application identity with a key pair.
    1.  Choose the appropriate access level for the Box content that you want to crawl:

        -   Box files that are shared with managed users: **App access plus Enterprise access**
        -   Box files which are shared with the service account: **App access only**
        -   Box files which are shared with the service account and its app users: **App access only**

        Support for configuring the Box level access with App access only was added with the 4.6 release.
        {: note}

    1.  Configure the access level by following the appropriate steps for your app access level type:

        -   **App access plus Enterprise access**

            Choose the following application scopes:

            -   *Read all folders stored in Box*
            -   *Write all folders stored in Box*
            -   *Manage Users*

            Enable the following advanced feature:

            -   *Generate User Access Tokens*

        -   **App access only**

            To crawl files that are shared with only the service account, complete the following steps:
            
            1.  Choose the following application scopes:

                -   *Read all folders stored in Box*
                -   *Write all folders stored in Box*

            1.  Share the target Box folders and files with the service account by completing the following steps:

                1.  From the General Settings page, copy the email for the service account ID.
                1.  When logged in as a managed user, share the folder or files that you want the connector to be able to crawl.
                1.  Add the service account ID email as the person to invite to share the files.

                For more information, see [the Box documentation](https://developer.box.com/guides/getting-started/user-types/service-account/#folder-tree-and-collaboration){: external}.

            To crawl files that are shared with the service account and its app users, complete the following steps:
            
            1.  Choose the following application scopes:

                -   *Read all folders stored in Box*
                -   *Write all folders stored in Box*
                -  *Manage Users*

            1.  Enable the following advanced feature:

                -   *Generate User Access Tokens*

            1.  Share the target Box folders and files with the appropriate app users. 
            
                For more information, see [the Box documentation](https://developer.box.com/guides/getting-started/user-types/app-users/#creation){: external}.

1. Create keys for authentication. Make sure that you complete the following tasks:

   1.  From the *General settings* page, click **Add a Public Key**.
   1.  Save the downloaded configuration file that is generated for the private key.
   1.  Click **Save Changes**.
   1.  From the *Configuration* page, copy the *Client ID* value.

1. Next, you must ask a Box administrator to authorize the app. In the Box admin console, complete the following tasks:

   1.  In the **Apps > Custom Apps Manager** page, click **Add App**.
   1.  Enter the client ID, and then click **Next**.

       For more information, see [Custom App Approval](https://developer.box.com/guides/authorization/custom-app-approval/){: external}.

1. Box administrator step: From the Box admin console, check that the app information is accurate, and then click **Authorize**.

## Connecting to the Box data source
{: #connector-box-cp4d-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Box**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents in Box is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**. Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  In the *Enter your credentials* section, click **Select file** and then browse to find the configuration file that was generated and downloaded when you added the public key as part of the prerequisite steps.

    You can download a configuration file again from the configuration page on the [Box Developer site](https://developer.box.com/){: external}.
1.  **Optional**. In the *Specify what you want to crawl* section, choose a specific user's content or a specific folder with content that you want to crawl. If you don't specify anything, the service crawls all of the content that is available to the custom app.

    - To crawl an entire enterprise, enter `box://app.box.com/`.
    - To crawl a specific folder, enter `box://app.box.com/user/USER'S_ACCOUNT_ID/folder/FOLDER_ID/FolderName`.

      For example, `box://example.app.box.com/user/460250779/folder/158001591642/My Folder`
    - To crawl a specific user, enter `box://app.box.com/user/USER'S_ACCOUNT_ID/`.

1.  **Optional**: If you are using a proxy server to access the data source server, then in the *Proxy settings* section, set the **Enable proxy settings** switch to `On`. Add values to the following fields:

    Username
    :   Optional. The username that you use to authenticate, if the proxy server requires authentication. If you do not know your username, you can obtain it from the administrator of the proxy server.

    Password
    :   Optional. The password that you use to authenticate, if the proxy server requires authentication. If you do not know your password, you can obtain it from the administrator of the proxy server.

    Proxy server host name or IP address
    :   The hostname or the IP address of the proxy server.

    Proxy server port number
    :   The network port that you want to connect to on the proxy server.
1.  **Optional**. If you want to activate document-level security, in the *Security* section, set the **Enable Document Level Security** switch to `On`.

    When this option is enabled, your users can crawl and query the same content that they can access when they are logged in to Box. For more information, see [Supporting document-level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).

1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.