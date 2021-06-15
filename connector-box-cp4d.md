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


# Box
{: #connector-box-cp4d}

Crawl documents that are stored in a Box data source.
{:shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments. For more information about connecting to Box from a managed deployment, see [Box](/docs/discovery-data?topic=discovery-data-connector-box-cloud).
{:note}

## What documents are crawled
{: #connector-box-cp4d-docs}

- Only documents that are supported by {{site.data.keyword.discoveryshort}} in your Box folders are crawled; all others are ignored. For more information, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
- Document level security is supported. When this option is enabled, your users can crawl and query the same content that they can access when they are logged in to Box. For more information, see [Supporting document level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).
- When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index.
- All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.
- Box notes are stored in JSON format, so {{site.data.keyword.discoveryshort}} also ingests any Box notes in the specified folders.

## Data source requirements
{: #connector-box-cp4d-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements) for all installed deployments, your Box data source must meet the following requirement: 

- You must obtain any required service licenses for the data source that you want to connect to. For more information about licenses, contact the system administrator of the data source.

## Prequisite steps
{: #connector-box-cp4d-prereq}

If you want to enable document level security, you must take some steps to set it up. For more information, see [About document level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).

You must create a custom application in Box before you can connect to Box from {{site.data.keyword.discoveryshort}}.

To create a custom application, complete the following steps:

1.  Make sure you have a [Box account](https://www.box.com/){: external}. During this process, you obtain the public key 1 ID and the enterprise ID.

1.  Establish an RSA key pair. You can create one yourself or let Box.com generate the key pair for you.

    1.  To create the key pair yourself, run the following shell commands:

        ```bash
        openssl genrsa 2048 > private-box.pem
        ```
        {: pre}

        ```bash
        openssl rsa -in private-box.pem -pubout -out public-box.pem
        ```
        {: pre}

    1.  Make a copy of `public-box.pem`.

1.  Next, create a custom app that uses *Server Authentication with JWT* as its authentication method. 

    For detailed steps, see [Setup with JWT](https://developer.box.com/guides/applications/custom-apps/jwt-setup/){: external} in the Box Developer Documentation.

    Follow these guidelines when you create the app:

    - During the setup procedure, choose to use the *Server Authentication with JWT* method to verify application identity with a key pair.
    - When you configure the custom app, set the application access level to *App access plus Enterprise access*.
    - Choose the following scopes:

      - *Read all folders stored in Box*
      - *Write all folders stored in Box*
      - *Manage Users*
      - *Manage Enterprise Properties*

    - Enable the following advanced features:

       - *Make API calls using the as-user header*
       - *Generate User Access Tokens*

    - When you add a public key, enter the content of `public-box.pem` that you generated when you created the RSA key pair.
    - Copy the public key 1 ID.

1. Next, you must authorize the app. In the Box admin console, complete the following tasks:

   - In the **App info** pane on the **General** page, copy the **Enterprise ID**.
   - Enter the client ID in the **API Key** field, and authorize your new app. You copied the client ID when you created the app. If you modify the app later, you must reauthorize it.

1. Establish the OAuth2 parameters. Make sure that you complete the following tasks:

   - On the **General** page, ensure that your app name is correct. You can also provide a description of your app or a custom website URL.
   - Under **Public Key Management**, paste your public key into the provided text box, and click **Verify**.
   - After the key is verified, click **Save** to finish setting up your public key.

1. After you receive your client ID, client secret, encoded private key, private key passphrase, key ID, and enterprise ID on the configuration page on [Box Developers](https://developer.box.com/){: external}, download the app settings as a JSON file, or `config.json`.

## Connecting to the Box data source
{: #connector-box-cp4d-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Box**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents in Box is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule. 

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  In the *Enter your credentials* section, click **Select file** and then browse to find and upload the `config.json` file that you created in the prerequisite step.

    You can download the JSON file from the configuration page on the [Box Developer site](https://developer.box.com/){: external}.
1.  **Optional**: In the *Specify what you want to crawl* section, choose a specific user's content or a specific folder with content that you want to crawl. If you don't specify anything, the service crawls all of the content that is available to the custom app.

    - To crawl an entire enterprise, enter `box://app.box.com/`.
    - To crawl a specific folder, enter `box://app.box.com/user/USER'S_ACCOUNT_ID/folder/FOLDER_ID/FolderName`.

      For example: `box://example.app.box.com/user/460250779/folder/158001591642/My Folder`
    - To crawl a specific user, enter `box://app.box.com/user/USER'S_ACCOUNT_ID/`.

1.  **Optional**: If you are using a proxy server to access the data source server, then in the *Proxy settings* section, set the **Enable proxy settings** switch to `On`. Add values to the following fields:
      
    - **Username**: Optional: The username that you use to authenticate, if the proxy server requires authentication. If you do not know your username, you can obtain it from the administrator of the proxy server.
    - **Password**: Optional: The password that you use to authenticate, if the proxy server requires authentication. If you do not know your password, you can obtain it from the administrator of the proxy server.
    - **Proxy server host name or IP address**: The hostname or the IP address of the proxy server.
    - **Proxy server port number**: The network port that you want to connect to on the proxy server.
1.  **Optional**: If you want to activate document level security, in the *Security* section, set the **Enable Document Level Security** switch to `On`. 

    When this option is enabled, your users can crawl and query the same content that they can access when they are logged in to Box. For more information, see [Supporting document level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).

1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    The processing time increases when this feature is enabled.
    {: note}
1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection. 

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.