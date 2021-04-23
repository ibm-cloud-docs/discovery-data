---

copyright:
  years: 2015, 2021
lastupdated: "2021-04-23"

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

You can connect to a data source and pull documents on a schedule into {{site.data.keyword.discoveryshort}} by configuring a collection to associate with that source. You can configure each collection with one data source. {{site.data.keyword.discoveryshort}} pulls documents from the data source using a process called crawling. Crawling is the process of systematically browsing and retrieving documents from the specified start location. {{site.data.keyword.discoveryshort}} only crawls items that you explicitly specify. The first time that a crawler crawls a data source is a full crawl, and every time that the crawler runs after the full crawl, per the crawl schedule, is a refresh, also called a recrawl.

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

You can connect to a data source using the {{site.data.keyword.discoveryshort}} tooling. The {{site.data.keyword.discoveryshort}} tooling provides a simplified method of connection that requires less understanding of the source systems. Consult the following process overview to see which sections to read next:

1.  Read the [Data source requirements](/docs/discovery-data?topic=discovery-data-sources#public-requirements).
2.  Read the requirements for your data source. For the available data sources, see the previous list.
3.  Read the instructions to connect to {{site.data.keyword.discoveryshort}} by using the tooling. For instructions to connect to {{site.data.keyword.discoveryshort}} by using the tooling, see [Creating a collection](/docs/discovery-data?topic=discovery-data-collections#createcollection).

You can use an IBM App Connect default connector to send data from a large set of popular data sources to {{site.data.keyword.discoveryshort}} by creating flows within the App Connect tooling. Note that creating a separate App Connect instance is required to use this App Connect default connector and that any costs that you incur when you use a paid App Connect instance are not included with the cost of using {{site.data.keyword.discoveryshort}}. Additionally, except for indexing, {{site.data.keyword.discoveryshort}} does not support any integration with App Connect that you perform on your own. For information about integrating App Connect with {{site.data.keyword.discoveryshort}} or for integration support or questions, see [How to use IBM App Connect with {{site.data.keyword.discoveryfull}}](https://www.ibm.com/support/knowledgecenter/SS6KM6/com.ibm.appconnect.dev.doc/how-to-guides-for-apps/watson-discovery.html){: external}. For the available data sources that you can use with the App Connect default connector to send data to {{site.data.keyword.discoveryshort}}, see [Connectors A-Z](https://www.ibm.com/cloud/app-connect/connectors/){: external}.

## FAQ extraction ![IBM Cloud only](images/ibm-cloud.png)
{: #faq-extraction}

The FAQ extraction feature is beta functionality and should not be used in production environments.
{: beta}

When you configure a data source for any project type, you have the option to **Apply FAQ extraction**. This beta feature detects question-and-answer pairs in your documents and automatically extracts the pairs. Your application can use the extracted pairs to provide more precise query results. 

Only apply FAQ extraction to a data source with documents that contain frequently asked questions that follow a consistent style. For example, ensure that the questions in the FAQ end with a question mark. The answer must be grouped with the question that it answers.

To turn on FAQ extraction for your data source, expand the **Syncing FAQ Content?** section and select **Apply FAQ extraction**.

Each question-and-answer pair in an FAQ document is split into a separate document. The question is stored in a `title` field and the answer is stored as a `text` field. A document with 100 question-and-answer pairs is split into 100 documents. If no question-and-answer pairs are detected in a document, only one document is added to the collection. There is a limit of 10,000 pairs per document. After the limit is reached, any remaining pairs that are found are stored in a single document. You can monitor the document count on the **Activity** tab of the **Manage collections** page.

To turn off FAQ extraction, go to the **Processings settings** tab of the **Manage collections** page. After disabling FAQ extraction, reprocess the collection by clicking the **Apply changes and reprocess** button.

If you apply FAQ extraction to a collection, you cannot use the [Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields) tool later to annotate fields.
{: note}

## Data source requirements
{: #public-requirements}

The following requirements and limitations are specific to {{site.data.keyword.discoveryshort}} on {{site.data.keyword.cloud_notm}}:

-  The individual document file size limit for Box, Salesforce, SharePoint Online, SharePoint OnPrem, {{site.data.keyword.cos_full}}, and Web Crawl is 10MB, and the file size limit for uploading data is 32MB.
-  If you crawl Box or Salesforce, a list of available resources is presented when you configure a source, using the {{site.data.keyword.discoveryshort}} tooling.
-  You can configure a collection with a single data source.
-  You must obtain an appropriate level of service license, for example Enterprise, for the data source. For information about the appropriate service level license that you need, contact the source system administrator.
-  {{site.data.keyword.discoveryshort}} source crawls do not delete documents that are stored in a collection. When a source is re-crawled, new documents are added, updated documents are modified to the current version, and deleted documents remain as the version last stored.

View the following table to see the objects that a data source can crawl and which data sources support crawling new and modified documents during a refresh:

Data source                                     | Crawls new and modified documents during refresh? | Compatible objects that can be crawled
----------------------------------------------- | ------------------------------------------------- | --------------------------------------
Box (**Application level** access)              | No                                                | Files, folders
Box (**Enterprise level** access)               | Yes                                               | Files, folders
Salesforce                                      | Yes                                               | Any default and custom objects that you have access to, accounts, contacts, cases, contracts, knowledge articles, attachments
Microsoft SharePoint Online                     | Yes                                               | SiteCollections, websites, lists, list items, document libraries, custom metadata, list item attachments
Microsoft SharePoint OnPrem                     | Yes                                               | SiteCollections, websites, lists, list items, document libraries, custom metadata, list item attachments
Web crawl                                       | No                                                | Websites, website subdirectories
{{site.data.keyword.cos_full_notm}}             | Yes                                               | Buckets, files
{: caption="Table 1. Data sources crawling support" caption-side="top"}

### Box
{: #connectboxpublic}

You must create a new Box custom application to connect to {{site.data.keyword.discoveryshort}}. The Box application that you create requires either Enterprise level or Application level access.

-  If you are not the Box administrator for your organization, [**Application level** access](/docs/discovery-data?topic=discovery-data-sources#applevelboxpublic) is recommended. You must have an administrator approve your application.
-  If you are the Box administrator for your organization, [**Enterprise level** access](/docs/discovery-data?topic=discovery-data-sources#entlevelboxpublic) is recommended.

If you have **Application level** access, new and modified documents are not crawled during a refresh. This functionality is only supported if you have **Enterprise level** access. If you have **Application level** access, you must first have an administrator approve your application.
{: important}

If there is a Box update, the steps to set up Box access might change. For more information, see the [Box developer documentation](https://developer.box.com/){: external}.
{: note}

Complete the following fields to configure a Box collection:
-  `Client ID` - The private key that you specify when you configure your Box app.
-  `Client Secret` - The client secret that you specify when you configure your Box app.
-  `Enterprise ID` - The enterprise ID of the Box account.
-  `Public Key ID` - The public key ID that Box generates.
-  `Private Key` - A part of the key pair that is generated to interact with the Box website.
-  `Passphrase` - The passphrase that is required to decrypt the private key if the private key is an encrypted file.

#### Setting up Application level access
{: #applevelboxpublic}

1.   Navigate to `https://app.box.com/developers/console`. Be sure to use the Box URL of your organization.
1.   Click **Create New App**.
1.   From the **Create a New App** page, select **Enterprise Integration**, and click **Next**.
1.   On the **Authentication Method** page, select **OAuth 2.0 with JWT (Server Authentication)**, and click **Next**.
1.   Name your app, and click **Create App**.
1.   After you create your Box app, click **View Your App**.
1.   While you view your app, select **Application access** as **Application**. You can use your existing managed users as you continue; you are not required to create new ones.
1.   Scroll to the **Application Scopes** section of the page, and select the following checkboxes:
     - **Read and write all folders stored in Box**
     - **Manage User**
1.   Scroll to the **Advanced Features** section, and enable the following options:
     - **Perform Actions as Users**
     - **Generate User Access Tokens**
1.  Click **Save Changes**.

The next few steps require assistance from the administrator of the Box account for your organization. If you are not the administrator, you can identify the administrator by opening the Box developer console and looking under **Account settings** > **Account details** > **Settings**.

1.  Administrator step: Authorize your application client ID at `https://app.box.com/master/settings/openbox` by clicking **Authorize New App**.
1.  Administrator step: Type the **client ID** from `https://app.box.com/developers/console` into the **API key** field, and then click **Authorize**.
1.  Administrator step: Retrieve a developer token for the application by navigating to `https://app.box.com/developers/console`, scrolling to the **Developer Token** section, and generating your token.
1.  Now that the administrator authorized the application, navigate to `https://developer.box.com/reference#page-create-an-enterprise-user`, and create an app user by using the API reference page.

   The following is a `curl` example to create an app user:

   ```bash
    curl https://api.box.com/2.0/users -H "Authorization: Bearer ACCESS_TOKEN" -d '{"name": "NedStark", "is_platform_access_only": true}' -X POST
   ```
   {: pre}

1.  Copy the newly generated **id** field contents, and provide them to the non-administrator who is connecting the Box application to {{site.data.keyword.discoveryshort}}.
1.  After the app user is created, you must share the folders that you want to crawl with the app user, and you must give the app user `Viewer` permissions for those folders, which requires the app user login name from the previous `curl` command response. Example:`"login":"AppUser_737729_jmUo@boxdevedition.com"`.
1.  Return to the Box developer console `https://app.box.com/developers/console`, and scroll to the **Add and Manage Public Keys** section.
1.  Click **Generate the public/private keypair**, download your key pair file, and open the file.
1.  In the key pair file, cut and paste the following fields into the {{site.data.keyword.discoveryshort}} tooling:
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret`
    -  `public_key_id`
    -  `private_key`
    -  `passphrase`

#### Setting up Enterprise level access
{: #entlevelboxpublic}

1.  Navigate to `https://app.box.com/developers/console`. Be sure to use the Box URL of your organization.
1.  Click **Create New App**.
1.  From the **Create a New App** page, select **Enterprise Integration**, and click **Next**.
1.  On the **Authentication Method** page, select **OAuth 2.0 with JWT (Server Authentication)**, and click **Next**.
1.  Name your app, and click **Create App**.
1.  After you create your Box app, click **View Your App**.
1.  While you view your app, select **Application access** as **Enterprise**. You can use your existing managed users as you continue; you are not required to create new ones.
1.  Scroll to the **Application Scopes** section of the page, and select the following checkboxes:
    - **Read and write all folders stored in Box**
    - **Manage Users**
    - **Manage Enterprise Properties**
1.  Scroll to the **Advanced Features** section, and enable the following options:
    - **Perform Actions as Users**
    - **Generate User Access Tokens**
1.  Click **Save Changes**.

If you change your Box app settings, `Reauthorize` your app so that the changes take effect.
{: tip}

The next few steps require assistance from the administrator of the Box account for your organization. If you are not the administrator, you can identify the administrator by opening the Box developer console and looking under **Account settings** > **Account details** > **Settings**.

1.  Administrator step: Authorize your application client ID by navigating to **Admin console** > **Enterprise settings** > **Apps** and scrolling to **Custom applications**. Example URL:`https://app.box.com/main/settings/openbox`.
1.  Administrator step: Type the **client ID** from `https://app.box.com/developers/console` into the **API key** field, and then click **Authorize**.
1.  Return to the Box developer console `https://app.box.com/developers/console`, and scroll to the **Add and Manage Public Keys** section. Click **Generate the public/private keypair**, download your key pair file, and open the file.
1.  From the key pair file, cut and paste the following fields into the {{site.data.keyword.discoveryshort}} tooling:
    -  `client_id`
    -  `enterprise_id`
    -  `client_secret`
    -  `public_key_id`
    -  `private_key`
    -  `passphrase`

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

<!--## Connecting to data sources with IP restrictions
{: #sources-ip-restrictions}

If the data source that you want to crawl is configured to allow crawlers from only a limited number of IP addresses or domains to process the data, you can add IBM-owned IP addresses to the allowlist for the site.

- The following IP addresses can be specified for services instances that are hosted in a US-based data center and were created on or after 1 May 2020:

  150.238.21.0/28
  169.48.255.224/28
  174.36.69.128/28

- For a list of IP addresses that can be specified for services instances that were created before 1 May 2020 (US) and before 21 February 2021 (non-US), see the [network addresses](https://cloud.ibm.com/docs/cloud-foundry-public?topic=cloud-foundry-public-network-address) that are listed for Cloud Foundry. For instances that are hosted in the US, use the list of IP addresses that are specified for the **Dallas** data center. For non-US instances, use the IP addresses that are specified for the **London** data center.-->
