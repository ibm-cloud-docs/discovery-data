---

copyright:
  years: 2015, 2021
lastupdated: "2021-05-07"

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

# Configuring IBM Cloud data sources
{: #sources}

<!-- V2 c/s help for the *Select a Collection type* page for IBM Cloud. Do not delete. -->

You can use {{site.data.keyword.discoveryfull}} on the {{site.data.keyword.cloud}} to connect to and crawl documents from remote sources.
{: shortdesc}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments. For information about {{site.data.keyword.icp4dfull_notm}} data sources, see [Configuring Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types).
{: note}

Connect to an external data source so that you can pull documents into {{site.data.keyword.discoveryshort}} on a schedule. {{site.data.keyword.discoveryshort}} pulls documents from the data source by *crawling* the data source. Crawling is the process of systematically browsing and retrieving documents from a starting location that you specify. When the crawler first processes a data source, it performs a full crawl. Each time the crawler runs after the initial crawl, it performs a refresh, where it checks for new and changed files only.

All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.
{: important}

You can use {{site.data.keyword.discoveryshort}} to crawl from the following data sources:

-  [Box](/docs/discovery-data?topic=discovery-data-sources#connectboxpublic)
-  [IBM Cloud Object Storage](/docs/discovery-data?topic=discovery-data-sources#connectcos)
-  [Microsoft SharePoint Online](/docs/discovery-data?topic=discovery-data-sources#connectsppublic)
-  [Microsoft SharePoint OnPrem](/docs/discovery-data?topic=discovery-data-sources#connectsp_oppublic)
-  [Salesforce](/docs/discovery-data?topic=discovery-data-sources#connectsfpublic)
-  [Web crawl](/docs/discovery-data?topic=discovery-data-sources#connectwebcrawlpublic)
-  [Uploading data](/docs/discovery-data?topic=discovery-data-upload-data)

You cannot crawl the supported data sources from a {{site.data.keyword.discoveryshort}} service instance that is hosted in the Seoul data center.
{: note}

If the external data source that you want to use is not listed, check whether {{site.data.keyword.appconserviceshort}} has a connector to the data source. You can use a default connector built for {{site.data.keyword.appconnect_notm}} to send data from a data sources to {{site.data.keyword.discoveryshort}}. To use an {{site.data.keyword.appconnect_notm}} connector, you must create a separate {{site.data.keyword.appconnect_notm}} instance. Any costs that you incur when you use a paid {{site.data.keyword.appconnect_notm}} instance are not included with the cost of using {{site.data.keyword.discoveryshort}}. Additionally, except for indexing, {{site.data.keyword.discoveryshort}} does not support any integration with {{site.data.keyword.appconnect_notm}} that you perform on your own. For a list of the data sources supported by {{site.data.keyword.appconnect_notm}} default connectors, see [Connectors A-Z](https://www.ibm.com/cloud/app-connect/connectors/){: external}. For more information about integrating {{site.data.keyword.appconnect_notm}} with {{site.data.keyword.discoveryshort}}, see [How to use IBM App Connect with {{site.data.keyword.discoveryfull}}](https://www.ibm.com/support/knowledgecenter/SS6KM6/com.ibm.appconnect.dev.doc/how-to-guides-for-apps/watson-discovery.html){: external}.

## Data source requirements
{: #public-requirements}

The following requirements and limitations are specific to {{site.data.keyword.discoveryshort}} on {{site.data.keyword.cloud_notm}}:

- A collection can connect to only one data source.
- A single {{site.data.keyword.discoveryshort}} service instance can have up to 100 collections that connect to external data sources.
- The individual document file size limit is 10 MB.
- You must obtain any required service licenses for the data source that you want to connect to. For more information about licenses, contact the system administrator of the data source.
- Crawls do not delete documents that are stored in a collection. When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents remain as the version last stored.

View the following table to see the objects that a data source can crawl and which data sources support crawling new and modified documents during a refresh:

| Data source | Supports scheduled document refreshes? | Objects that are crawled |
|-------------|----------------------------------------|--------------------------|
| Box (**App access**) | No | Files, folders |
| Box (**Enterprise access**)  | Yes (New and modified documents only) | Yes | Files, folders |
| Salesforce | Yes (New and modified documents only) | Any default and custom objects that you have access to, accounts, contacts, cases, contracts, knowledge articles, attachments |
| Microsoft SharePoint Online | Yes (New and modified documents only) | SiteCollections, websites, lists, list items, document libraries, custom metadata, list item attachments
| Microsoft SharePoint OnPrem | Yes (New and modified documents only) | SiteCollections, websites, lists, list items, document libraries, custom metadata, list item attachments |
| Web crawl | Yes (Full recrawl) | Websites, website subdirectories |
| {{site.data.keyword.cos_full_notm}} | Yes (New and modified documents only) | Buckets, files |
{: caption="Table 1. Data sources crawling support" caption-side="top"}

## FAQ extraction ![IBM Cloud only](images/ibm-cloud.png)
{: #faq-extraction}

The FAQ extraction feature is beta functionality and should not be used in production environments.
{: beta}

When you configure a data source for any project type, you have the option to **Apply FAQ extraction**. This beta feature detects question-and-answer pairs in your documents and automatically extracts the pairs. Your application can use the extracted pairs to provide more precise query results.

Only apply FAQ extraction to a data source with documents that contain frequently asked questions that follow a consistent style. For example, ensure that the questions in the FAQ end with a question mark. The answer must be grouped with the question that it answers.

To turn on FAQ extraction for your data source, expand the **Syncing FAQ Content?** section and select **Apply FAQ extraction**.

Each question-and-answer pair in an FAQ document is split into a separate document. The question is stored in a `title` field and the answer is stored as a `text` field. A document with 100 question-and-answer pairs is split into 100 documents. If no question-and-answer pairs are detected in a document, only one document is added to the collection. There is a limit of 10,000 pairs per document. After the limit is reached, any remaining pairs that are found are stored in a single document. You can monitor the document count on the **Activity** tab of the **Manage collections** page.

To turn off FAQ extraction, go to the **Processings settings** tab of the **Manage collections** page. After disabling FAQ extraction, reprocess the collection by clicking **Apply changes and reprocess**.

Remember these notes:

- If you apply FAQ extraction to a collection, you cannot use the [Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields) tool later to annotate fields.
- If you delete a question-and-answer pair from a webpage that you crawled previously, the question-and-answer pair that was already indexed in your collection remains in the index.

To learn more about FAQ extraction, see the [Turn your FAQ pages into conversational AI](https://medium.com/ibm-data-ai/turn-your-faq-pages-into-conversational-ai-8ac7ae7ec793) blog post on Medium.

### Box
{: #connectboxpublic}

You must create a custom application in Box before you can connect to Box from {{site.data.keyword.discoveryshort}}.

- [Creating a custom app in Box](#boxpublic-customapp)
- [Connecting to the Box data source](#boxpublic-setup)

#### Creating a custom app in Box
{: #boxpublic-customapp}

In Box, create a custom app that uses *Server Authentication with JWT* as its authentication method. 

For detailed steps, see [Setup with JWT](https://developer.box.com/guides/applications/custom-apps/jwt-setup/){: external} in the Box Developer Documentation.

Follow these guidelines:

- During the setup procedure, choose to use the *Server Authentication with JWT* method to verify application identity with a key pair.
- When you configure the custom app, you can choose to use one of the application access levels:

  - App access only
  - App access plus Enterprise access

  Refreshing documents on a schedule is supported only when you choose **App access plus Enterprise access**. If you set up the connection with **App access**, new and modified documents are not crawled during a refresh.
  {: important}

  - If you are an administrator, configure **App access plus Enterprise access**. Otherwise, you can configure the app to have **App access**. However, you must get application approval from a Box administrator.
  
  - For both application access levels, specify the following settings:

    - Choose the following scopes:

      - *Read all folders stored in Box*
      - *Write all folders stored in Box*
      - *Manage Users*

      **For apps with Enterprise access only**: Add this extra scope:

      - *Manage Enterprise Properties*
    - Enable the following advanced features:

       - *Make API calls using the as-user header*
       - *Generate User Access Tokens*

- Get the custom app authorized by an administrator.

  For more information, see [App approval](https://developer.box.com/guides/applications/custom-apps/app-approval/){: external} in the Box Developer Documentation.
- After the app is created, authorized, and authentication is configured, download the app settings as a JSON file from the dev console.

  You will provide the following information from this file when it is requested later:

    -  `client_id`
    -  `enterprise_id`
    -  `client_secret`
    -  `public_key_id`
    -  `private_key`
    -  `passphrase`

### Connecting to the Box data source
{: #boxpublic-setup}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **Create collection**.
1.  Click **Box**, and then click **Next**.
1.  Refer to the values from the Box app settings JSON file that you downloaded during the previous procedure to fill in the following fields:

    - `Client ID` - The private key that you specify when you configure your Box app.
    - `Client Secret` - The client secret that you specify when you configure your Box app.
    - `Enterprise ID` - The enterprise ID of the Box account.
    - `Public Key ID` - The public key ID that Box generates.
    - `Private Key` - A part of the key pair that is generated to interact with the Box website.
    - `Passphrase` - The passphrase that is required to decrypt the private key if the private key is an encrypted file.
1.  Click **Next**.
1.  Apply any configuration settings that you want to use.

Box notes are stored in JSON format, so {{site.data.keyword.discoveryshort}} ingests any Box notes in the specified folders.
{: note}

### IBM Cloud Object Storage
{: #connectcos}

When you connect to an {{site.data.keyword.cos_full}} source, the following credentials are required. You can obtain them from your {{site.data.keyword.cos_full_notm}} administrator:

-  `Endpoint` - The `endpoint` name used to interact with {{site.data.keyword.cos_full_notm}} data.
   Do not enter `http://` or `https://`, as part of the {{site.data.keyword.cos_full_notm}} `endpoint` credential. Otherwise, you might receive an error message indicating that you have invalid or expired credentials. For the proper formatting of endpoints, see the column named Endpoint in the table in [Regional Endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints-region).
-  `Access key id` - `access_key_id` obtained when the {{site.data.keyword.cos_full_notm}} instance was created.
-  `Secret access key` - `secret_access_key` to sign requests obtained when the {{site.data.keyword.cos_full_notm}} instance was created.

IAM authentication is not currently supported for this connector. You need to set up HMAC authentication before you configure this connector. See [Service Credentials](/docs/cloud-object-storage/iam?topic=cloud-object-storage-service-credentials) for instructions.
{: important}

After this information is entered, you can choose how often you want to sync your data and select the buckets you want to sync to.

Other items to note when you crawl {{site.data.keyword.cos_full_notm}}:

-  This connector does not support crawling private endpoints.
-  For more information about {{site.data.keyword.cos_full_notm}} endpoints, see [Endpoints and storage locations](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints).
-  There is a slight performance issue if all buckets are selected. In this case, a delay is possible, before the documents complete indexing.

### Microsoft SharePoint Online
{: #connectsppublic}

When connecting to a Microsoft SharePoint Online source, ensure that the instance that you plan to connect to is an Enterprise (E1) plan or higher.

Except for `site_collection_path`, the following fields are required to connect to a SharePoint Online source. If you do not know what to enter in these fields, contact your SharePoint administrator, or consult the [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}:

-  `Username` - The `username` to connect to the SharePoint Online SiteCollection that you want to crawl. This user must have access to all sites and lists that the user wants to crawl and index. Your `username` input must be a default Azure Active Directory (Azure AD) account, which is formatted as follows: `<username>@<domain>.onmicrosoft.com`. If you do not have an Azure AD username, contact your SharePoint site administrator.
-  `Password` - The `password` to connect to the SharePoint Online SiteCollection that you want to crawl. This value is never returned and is only used when creating or modifying credentials.
-  `Organization URL` - The `organization_url` of the source that you want to crawl. When you enter this input, only enter the domain name of the URL, for example `https://<company>.<domain>.com/`. If you enter a URL that extends beyond the domain name, or `.com/`, the input is invalid. Replace `<company>` and `<domain>` with the corresponding parts of the organization URL that you want to crawl.
-  `Site collection path` Optional: - The `site_collection_path` to the source that you want to crawl. For example, if your organization URL is `https://<company>.<domain>.com/sites/test`, the `/sites/test` segment is the input to enter in this field. You cannot enter the full organization URL in this field, and you cannot specify any input that has the extension `.aspx`, such as URLs to document libaries, lists, and subsites. For example, the following URL to a list is invalid input: `https://..com/Lists//AllItems.aspx`. In addition, there is a limit of one site collection path per collection. If you leave this field blank, the default is `/`, and the root site collection is crawled.

Note the following items when you crawl Microsoft SharePoint Online:

-  To crawl SharePoint, the `username` account does not need `SiteCollection Administrator` permissions.
-  When you crawl SharePoint, you must have the list of SharePoint site collection paths that you want to crawl. {{site.data.keyword.discoveryshort}} does not support folder paths as input.
-  You must use the default Azure Active Directory authentication.
-  Because the SharePoint API does not return a unique ID for ListItems, ListItem documents in {{site.data.keyword.discoveryshort}} are overridden when the IDs of different ListItems are the same. To ensure that your ListItems are not overridden and that each has a unique ID, recrawl your collection, or change the configuration settings for your data source so that your ListItems are assigned a unique ID.
-  SharePoint Online cannot crawl `Personal SiteCollections`.
-  If you created a collection that had multiple site collection paths prior to the limit, you cannot see all of your crawl paths. The site collection path that is used is the one that you entered before you clicked **Next** to create your collection.

To successfully crawl Microsoft SharePoint Online, you must enable legacy authentication and Contribute level permissions. To enable legacy authentication, visit the [Azure portal](https://portal.azure.com/){: external}, or contact your SharePoint administrator. For assistance with enabling Contribute level permissions, you can also contact your SharePoint administrator.
{: important}

If you created a SharePoint Online account after January 2020, two-factor authentication is enabled for your account, by default. To crawl your SharePoint Online collection, you must disable two-factor authentication. To view and change your multifactor authentication status, see [View the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#view-the-status-for-a-user){: external} or [Change the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#change-the-status-for-a-user){: external}.
{: important}

### Microsoft SharePoint OnPrem
{: #connectsp_oppublic}

<!-- Learn more topic WDS -->
To connect to SharePoint OnPrem, you must first install and configure {{site.data.keyword.SecureGatewayfull}}. For more information about installing {{site.data.keyword.SecureGatewayfull}}, see [Installing IBM Secure Gateway for on-premises data](/docs/discovery-data?topic=discovery-data-sources#gatewaypublic).
{: note}

You can use this connector to crawl a SharePoint 2013, 2016, or 2019 on-premises data source. Complete the following fields to connect to the data source. If you do not know what to enter in these fields, contact your SharePoint administrator, or consult the [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}:

-  `Username` - The username to connect to the SharePoint OnPrem web application that you want to crawl. This user must have access to all sites and lists that they want to crawl and index.
-  `Password` - The password to connect to the SharePoint OnPrem web application that you want to crawl. This value is never returned and is only used when creating or modifying credentials.
-  `Web Application URL` - The SharePoint OnPrem web application URL, for example `https://sharepointwebapp.com:8443`. If you do not enter a port number, the default is port `80` for HTTP and port `443` for HTTPS.
-  `Domain` - The domain of the SharePoint OnPrem account.

Note the following items when you crawl Microsoft SharePoint OnPrem:

-  To crawl SharePoint OnPrem, the `Username` account must have `SiteCollection Administrator` permissions.
-  To crawl SharePoint OnPrem, you must have the list of SharePoint site collection paths that you want to crawl. {{site.data.keyword.discoveryshort}} does not support folder paths as input.
-  The number of gateways that you can create is limited to 50. If you exceed this limit, you will be unable to create any more gateways, and you will see an error message that states, `Failed to update or create the network resource.`
-  SharePoint OnPrem cannot crawl `Personal SiteCollections`.

### Salesforce
{: #connectsfpublic}

When connecting to a Salesforce source, ensure that the instance you plan to connect to is an Enterprise plan or higher.

The following credentials are required to connect to a Salesforce source. If you do not know these credentials, consult your Salesforce administrator:
-  `Username` - The `username` of the source that these credentials connect to.
-  `Password plus service token` - The `password` consists of the Salesforce password and a valid Salesforce security token concatenated. This value is never returned and is only used when creating or modifying credentials.
-  `URL` - The `url` of the source that these credentials connect to.

When identifying the credentials, it might be useful to consult the [Salesforce developer documentation](https://developer.salesforce.com/docs/){: external}.

When you crawl Salesforce, note that Knowledge Articles are only crawled if their **version** is `published` and their languages is `en-us`.

### Web crawl
{: #connectwebcrawlpublic}

Add a web crawl collection to crawl a website, analyze its page content, and store meaningful information. Specify one or more base web page URLs and configure how many linked pages for the web crawl to follow. You can configure how often to synchronize with the website, so you control how up to date the data in your collection is.

You can connect to the following types of web content:

- Public websites
- Private company websites or other sites that require authentication
- Websites that are behind a corporate firewall

The web crawler does not crawl dynamic websites that use JavaScript to render content. You can confirm the use of JavaScript by viewing the source code of the website in your browser.
{: note}

If you want to crawl a group of URLs that includes some websites that require authentication and some that don't, consider creating a different collection for each authentication type.

To configure the web crawl collection, complete the following steps:

1.  Specify the URL of the website that you want to crawl.

    - If the site you want to crawl requires a login, set **Basic authentication** to `On`, add the URL of the page to the **Starting URL** field, and then click **Add**.

      Add a username and password with access to the site, and then click **Save credentials**. You can specify only one set of credentials per collection.

      For example, you can specify `https://cloud.ibm.com` as the starting URL and add your IBMid as the credentials.
      
      If you want to start the crawl from a specific section of the site, specify it in the **Starting URLs** field. The domain name of the subsection must match the domain in the URL you specified earlier.

      For example, you might change the starting URL to `https://cloud.ibm.com/unifiedsupport/supportcenter`.
    - For any public web pages that you want to crawl, add the URL for the root page of the website to the **Starting URLs** field, and then click **Add**.

      You can add more than one starting page for public websites.

      The final forward slash (`/`) in the URL determines the subtree to crawl. If you specify `https://www.example.com/banking/faqs.html`, all URLs that begin with `https://www.example.com/banking/` are crawled, for example. If you specify `https://www.example.com/banking` all URLs that begin with `https://www.example.com/` are crawled.

      By default, the number of consecutive links that the crawl follows from the starting URL is `2`. To change the number of hops or to list website sections to exclude from the crawl, click the edit icon. 
      
      - The maximum number of hops allowed is `20`. 
      - To specify URL paths to exclude, add the site path. For example, if the starting URL is `https://example.com`, you can exclude `https://example.com/licenses` and `https://example.com/pricing` by entering `/licenses/, /pricing/`. 
      - If you want to restrict the crawl to a single page, add the URL to the **Starting URLs** field. For example, `https://www.example.com/banking/faqs.html`. Click the edit icon to set the **Maximum number of links to follow** to `0`.

      The number of web pages that are crawled is limited to 250,000, so the web crawler might not crawl all the specified websites.

      The number of child URLs per URL that are crawled is limited to 10,000. If the number of child URLs within any crawled URL exceeds 10,000, the crawler cannot process any of the content in the child URLs.

    - To connect to a website that is hosted behind a firewall, set up an {{site.data.keyword.SecureGatewayfull}} connection first.
    
      Valuable content is often stored on your company's internal website. Typically, such intranet websites are accessible only from a computer that is connected to your office network or through a VPN connection. You can establish a persistent and more secure connection between the web crawler and this type of internal site by using {{site.data.keyword.SecureGateway}}.
    
      Expand *More connection settings*, and then set **Connect to on-premise network** to `On`. For more information about how to set up the connection, see [Installing IBM Secure Gateway for on-premises data](#gatewaypublic).

1.  If you want to look for and extract question and answer pairs, select **Apply FAQ extraction**.

    For more information, see [FAQ extraction](#faq-extraction).

1.  If you want the web crawl to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    The processing time increases when this feature is enabled.
    {: note}

1.  Click **Finish**.

## Installing IBM Secure Gateway for on-premises data 
{: #gatewaypublic}

<!-- Learn more topic WDS -->
To connect to an on-premises data source, you first need to download, install, and configure {{site.data.keyword.SecureGatewayfull}}. After you install {{site.data.keyword.SecureGatewayfull}} for your first on-premises data source, you do not need to repeat this process.
{: shortdesc}

For more information, see [About Secure Gateway](/docs/SecureGateway?topic=SecureGateway-about-sg){: external}.

You must first download, install, and configure {{site.data.keyword.SecureGatewayfull}} before you can create a [SharePoint OnPrem](/docs/discovery-data?topic=discovery-data-sources#connectsp_oppublic) collection.
{: note}

To install {{site.data.keyword.SecureGatewayfull}}, complete the following steps:

1.  From the **My projects** page in {{site.data.keyword.discoveryshort}}, click **New project**, and select a project type.
1.  Select the data source that you want to connect to. When you select an on-premises data source, click **Manage connection**.
1.  On the **Download and install Secure Gateway client** page, download the appropriate version of {{site.data.keyword.SecureGatewayfull}}.
1.  After you complete the download, click **Download Secure Gateway and Continue**. When prompted, enter the **Gateway ID** and **Token** that are displayed. For more information about installation, see [Installing the client](/docs/SecureGateway?topic=SecureGateway-client-install).
1.  On the machine running the Secure Gateway Client, open the Secure Gateway dashboard at `http://localhost:9003`.
1.  Click **add ACL** on the dashboard, and add the endpoint URL of each SharePoint collection to the **Allow access** list. For example, Hostname: `mycompany.sharepoint.com` and port: `80`.
1.  Return to {{site.data.keyword.discoveryshort}}, and click **Continue**. If the connection is successful, a `Connection successful` message is displayed. If the connection is unsuccessful, open the {{site.data.keyword.SecureGatewayfull}} dashboard, and verify that the endpoints on the **Allow access** list are correct.

After the connection is successful, you can begin entering the credentials for your on-premises data source.

## Data source connection and data isolation
{: #source_isolation}

[Connecting to external data sources](/docs/discovery-data?topic=discovery-data-sources) reduces the data isolation of your service instance because data in transit between the source and the service cannot be isolated. All other isolation (at-rest, administration, query) remains in full. All in-flight communication between and within services and data sources is encrypted using TLS v1.2. The private keys for the TLS certificates are encrypted at rest using AES-256-GCM, the service certificates expire every three years, and the certificate revocation lists are updated monthly. All credentials are sent over an encrypted connection using TLS v1.2 and encrypted at rest using AES-256. Connections to those data sources use whatever secure protocols are supported by those data sources.

## Viewing collections connected to a gateway
{: #gateway-connection}

You can view a list of collections that are connected to a particular gateway. Complete the following steps to view collections that share a particular gateway:

1. From the **My projects** page, click **Data usage and GDPR**.
1. Click **On-premise connections**. If there are any collections that share a common gateway, those collections appear in **Connected collections**. If no collections share a gateway, you see an indicator stating that `No collections use this connection.`.

## Connecting to data sources with IP restrictions
{: #sources-ip-restrictions}

Some data sources allow crawlers from only a limited number of trusted network addresses or domains to access and process their data. If one of the data sources that you want to connect to limits access in this way, you can add IBM-managed IP addresses to the allowlist of the data source.

Network addresses are subject to change from time to time. You can monitor for updates to these addresses by subscribing to the repo notifications for this page. Click **Edit Topic** and then select **Watching** in the Notifications dialog of the repo.
{: tip}

- For service instances that are hosted in a US-based data center and that were created on or after 1 May 2020, add the following IP addresses:

  ```
  150.238.21.0/28
  169.48.255.224/28
  174.36.69.128/28
  ```
  {: screen}

- For service instances that are hosted in non-US data centers and that were created on or after 21 February 2021, add the following IP addresses:

  ```
  159.122.203.64/28
  158.175.114.128/28
  158.176.107.48/28
  ```
  {: screen}

- For a list of IP addresses that you can add to an allowlist for services instances that were created before 1 May 2020 (US) and before 21 February 2021 (non-US), see the [network addresses](https://cloud.ibm.com/docs/cloud-foundry-public?topic=cloud-foundry-public-network-address) that are listed for Cloud Foundry. 

  - Refer to the **Dallas** data center IP addresses for all US-hosted service instances. 
  - Refer to the **London** data center IP addresses for all service instances that are hosted outside the US.
