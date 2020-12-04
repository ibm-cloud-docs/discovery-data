---

copyright:
  years: 2015, 2020
lastupdated: "2020-12-04"

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

# Configuring IBM Cloud data sources
{: #sources}

<!-- V2 c/s help for the *Select a Collection type* page for IBM Cloud. Do not delete. -->

![IBM Cloud only](images/cloudonly.png)</br> 

You can use {{site.data.keyword.discoveryfull}} on the {{site.data.keyword.cloud}} to connect to and crawl documents from remote sources. For information about Cloud Pak for Data data sources, see [Configuring Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types).
{: shortdesc}

You can connect to a data source and pull documents on a schedule into {{site.data.keyword.discoveryshort}} by configuring a collection to associate with that source. You can configure each collection with one data source. {{site.data.keyword.discoveryshort}} pulls documents from the data source using a process called crawling. Crawling is the process of systematically browsing and retrieving documents from the specified start location. {{site.data.keyword.discoveryshort}} only crawls items that you explicitly specify. The first time that a crawler crawls a data source is a full crawl, and every time that the crawler runs after the full crawl, per the crawl schedule, is a refresh, also called a recrawl.

You can use {{site.data.keyword.discoveryshort}} to crawl from the following data sources:

-  [Box](/docs/discovery-data?topic=discovery-data-sources#connectboxpublic)
-  [Salesforce](/docs/discovery-data?topic=discovery-data-sources#connectsfpublic)
-  [Microsoft SharePoint Online](/docs/discovery-data?topic=discovery-data-sources#connectsppublic)
-  [Web Crawl](/docs/discovery-data?topic=discovery-data-sources#connectwebcrawlpublic)
-  [SharePoint 2016 On-Premise](/docs/discovery-data?topic=discovery-data-sources#connectsp_oppublic)
-  [{{site.data.keyword.cloud_notm}} Object Storage](/docs/discovery-data?topic=discovery-data-sources#connectcos)
-  [Uploading data](/docs/discovery-data?topic=discovery-data-collections#upload-data)

You can connect to a data source using the {{site.data.keyword.discoveryshort}} tooling. The {{site.data.keyword.discoveryshort}} tooling provides a simplified method of connection that requires less understanding of the source systems. Consult the following process overview to see which sections to read next:

1.  Read the [Data source requirements](/docs/discovery-data?topic=discovery-data-sources#public-requirements).
2.  Read the requirements for your data source. For the available data sources, see the previous list.
3.  Read the instructions to connect to {{site.data.keyword.discoveryshort}} by using the tooling. For instructions to connect to {{site.data.keyword.discoveryshort}} by using the tooling, see [Creating a collection](/docs/discovery-data?topic=discovery-data-collections#createcollection).

You can use an IBM App Connect default connector to send data from a large set of popular data sources to {{site.data.keyword.discoveryshort}} by creating flows within the App Connect tooling. Note that creating a separate App Connect instance is required to use this App Connect default connector and that any costs that you incur when you use a paid App Connect instance are not included with the cost of using {{site.data.keyword.discoveryshort}}. Additionally, except for indexing, {{site.data.keyword.discoveryshort}} does not support any integration with App Connect that you perform on your own. For information about integrating App Connect with {{site.data.keyword.discoveryshort}} or for integration support or questions, see [How to use IBM App Connect with {{site.data.keyword.discoveryfull}}](https://www.ibm.com/support/knowledgecenter/SS6KM6/com.ibm.appconnect.dev.doc/how-to-guides-for-apps/watson-discovery.html){: external}. For the available data sources that you can use with the App Connect default connector to send data to {{site.data.keyword.discoveryshort}}, see [Connectors A-Z](https://www.ibm.com/cloud/app-connect/connectors/){: external}.

## Data source requirements
{: #public-requirements}

The following requirements and limitations are specific to {{site.data.keyword.discoveryshort}} on {{site.data.keyword.cloud_notm}}:

-  The individual document file size limit for Box, Salesforce, SharePoint Online, SharePoint 2016 On-Premise, {{site.data.keyword.cloud_notm}} Object Storage, and Web Crawl is 10MB, and the file size limit for uploading data is 32MB.
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
Microsoft SharePoint Online                     | Yes                                               | SiteCollections, websites, lists, list items, document libraries
Microsoft SharePoint 2016 On-Premise            | Yes                                               | SiteCollections, websites, lists, list items, document libraries
Web Crawl                                       | No                                                | Websites, website subdirectories
{{site.data.keyword.cloud_notm}} Object Storage | Yes                                               | Buckets, files
{: caption="Table 1. Data sources that support crawling new and modified documents during refresh and objects that can be crawled" caption-side="top"}

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

### Salesforce
{: #connectsfpublic}

When connecting to a Salesforce source, ensure that the instance you plan to connect to is an Enterprise plan or higher.

The following credentials are required to connect to a Salesforce source. If you do not know these credentials, consult your Salesforce administrator:
-  `Username` - The `username` of the source that these credentials connect to.
-  `Password plus service token` - The `password` consists of the Salesforce password and a valid Salesforce security token concatenated. This value is never returned and is only used when creating or modifying credentials.
-  `URL` - The `url` of the source that these credentials connect to.

When identifying the credentials, it might be useful to consult the [Salesforce developer documentation](https://developer.salesforce.com/docs/){: external}.

When you crawl Salesforce, note that Knowledge Articles are only crawled if their **version** is `published` and their languages is `en-us`.

### SharePoint Online
{: #connectsppublic}

When connecting to a Microsoft SharePoint Online source, ensure that the instance that you plan to connect to is an Enterprise (E1) plan or higher.

Except for `site_collection_path`, the following fields are required to connect to a SharePoint Online source. If you do not know what to enter in these fields, contact your SharePoint administrator, or consult the [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}:

-  `Username` - The `username` to connect to the SharePoint Online SiteCollection that you want to crawl. This user must have access to all sites and lists that the user wants to crawl and index. Your `username` input must be a default Azure Active Directory (Azure AD) account, which is formatted as follows: `<username>@<domain>.onmicrosoft.com`. If you do not have an Azure AD username, contact your SharePoint site administrator.
-  `Password` - The `password` to connect to the SharePoint Online SiteCollection that you want to crawl. This value is never returned and is only used when creating or modifying credentials.
-  `Organization URL` - The `organization_url` of the source that you want to crawl. When you enter this input, only enter the domain name of the URL, for example `https://<company>.<domain>.com/`. If you enter a URL that extends beyond the domain name, or `.com/`, the input is invalid.
-  `Site collection path` Optional: - The `site_collection_path` to the source that you want to crawl. For guidance on how to format this input, see the following example: `/sites/test`. If unspecified, the default is `/`, and the root site collection is crawled.

Note the following items when you crawl Microsoft SharePoint Online:

-  To crawl SharePoint, the `username` account does not need `SiteCollection Administrator` permissions.
-  When you crawl SharePoint, you must have the list of SharePoint site collection paths that you want to crawl. {{site.data.keyword.discoveryshort}} does not support folder paths as input.
-  You might want to use the default Azure AD authentication.
-  Because the SharePoint API does not return a unique ID for ListItems, ListItem documents in {{site.data.keyword.discoveryshort}} are overriden when the IDs of different ListItems are the same. To ensure that your ListItems are not overriden and that each has a unique ID, recrawl your collection, or change the configuration settings for your data source so that your ListItems are assigned a unique ID.

To successfully crawl Microsoft SharePoint Online, you must enable legacy authentication and Contribute level permissions. To enable legacy authentication, visit the [Azure portal](https://portal.azure.com/){: external}, or contact your SharePoint administrator. For assistance with enabling Contribute level permissions, you can also contact your SharePoint administrator.
{: important}

If you created a SharePoint Online account after January 2020, two-factor authentication is enabled for your account, by default. To crawl your SharePoint Online collection, you must disable two-factor authentication. To view and change your multifactor authentication status, see [View the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#view-the-status-for-a-user){: external} or [Change the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#change-the-status-for-a-user){: external}.
{: important}

### Web Crawl
{: #connectwebcrawlpublic}

You can use the web crawler to crawl public websites that do not require a username and password and websites that require authentication. If you want to crawl a group of URLs that is comprised of websites that require authentication and websites that do not, consider creating a different collection that has the same authentication type. You can select how often you would like {{site.data.keyword.discoveryshort}} to sync with the websites, and you can select the language and the number of links to follow.

**Authentication Settings**

-  `Basic authentication` - Optional: By default, this option is set to **Off**. When set to **On**, crawls websites that require a username and password. You can specify only one username and password per collection.
   - `Starting URL` - The URL that you want to crawl that requires a username and password. After you add a URL, this URL is applied to `Starting URLs` in **Specify where you want to crawl**.
   - `Username` - The username for authenticating to the starting URL that you specify in `Basic authentication`.
   - `Password` - The password for authenticating to the starting URL that you specify in `Basic authentication`.

**Specify where you want to crawl**

-  `Starting URLs` - Crawls public websites that do not require a username and password, and then click **Add** to add the URL to the URL group. However, you can also enter URLs that require basic authentication in this field. Be sure that the URL contains the same domain of the URL that you entered in `Basic authentication`. For example, if you enter `https://domainname.com` in `Basic authentication`, you can enter other paths from that URL in this field, such as `https://domainname.com/myfolder1/` and `https://domainname.com/myfolder2/`. You can click the edit icon to specify the **Crawl settings**. You can set the **Maximum number of links to follow**, which is the number of consecutive links to follow from the starting URL. The default number of hops is `2`, and the maximum is `20`. You can specify URL paths to exclude from the crawl in the **Exclude URLs where the path includes** field. Separate the paths by using commas. For example, if you specified the URL `https://domainname.com`, you can exclude `https://domainname.com/licenses` and `https://domainname.com/pricing` by entering `/licenses/, /pricing/`.

When you specify a URL to crawl, the final `/` determines the subtree to crawl. For example, if you enter the URL `https://www.example.com/banking/faqs.html`, all URLs that begin with `https://www.example.com/banking/` are crawled, and the input of `https://www.example.com/banking` crawls all URLs that begin with `https://www.example.com/`. If you would like to restrict the crawl to a specific URL, such as `https://www.example.com/banking/faqs.html`, enter that URL in `Starting URLs`, click the edit icon, and then set the **Maximum number of links to follow** to `0`.

The web crawler does not crawl dynamic websites that use JavaScript to render content. You can confirm the use of JavaScript by viewing the source code of the website in your browser.

The number of web pages crawled is limited to 250,000, so the web crawler might not crawl all the specified websites and might reach the maximum number of hops.
{: note}

The crawler has a limit of 10,000 child URLs per URL that is crawled. If the number of child URLs within any crawled URL exceeds 10,000, the crawler cannot process any of the content in the child URLs.
{: note}

### SharePoint 2016 On-Premise
{: #connectsp_oppublic}

<!-- Learn more topic WDS -->
Also known as SharePoint Server 2016, Microsoft SharePoint 2016 is an on-premises data source. To connect to it, you must first install and configure {{site.data.keyword.SecureGatewayfull}}. For more information about installing {{site.data.keyword.SecureGatewayfull}}, see [Installing IBM Secure Gateway for on-premises data](/docs/discovery-data?topic=discovery-data-sources#gatewaypublic).
{: note}

The following fields are required to connect to a SharePoint 2016 data source. If you do not know what to enter in these fields, contact your SharePoint administrator, or consult the [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}:

-  `Username` - The username to connect to the SharePoint 2016 web application that you want to crawl. This user must have access to all sites and lists that they want to crawl and index.
-  `Password` - The password to connect to the SharePoint 2016 web application that you want to crawl. This value is never returned and is only used when creating or modifying credentials.
-  `Web Application URL` - The SharePoint 2016 web application URL, for example `https://sharepointwebapp.com:8443`. If you do not enter a port number, the default is port `80` for HTTP and port `443` for HTTPS.
-  `Domain` - The domain of the SharePoint 2016 account.

Note the following items when you crawl Microsoft SharePoint 2016:

-  To crawl SharePoint 2016, the `Username` account must have `SiteCollection Administrator` permissions.
-  To crawl SharePoint 2016, you must have the list of SharePoint site collection paths that you want to crawl. {{site.data.keyword.discoveryshort}} does not support folder paths as input.
-  The number of gateways that you can create is limited to 50. If you exceed this limit, you will be unable to create any more gateways, and you will see an error message that states, `Failed to update or create the network resource.`.

### IBM Cloud Object Storage
{: #connectcos}

When you connect to an {{site.data.keyword.blockstoragefull}} source, the following credentials are required. You can obtain them from your {{site.data.keyword.blockstoragefull}} administrator:

-  `Endpoint` - The `endpoint` name used to interact with {{site.data.keyword.blockstoragefull}} data.
   Do not enter `http://` or `https://`, as part of the {{site.data.keyword.blockstoragefull}} `endpoint` credential. Otherwise, you might receive an error message indicating that you have invalid or expired credentials. For the proper formatting of endpoints, see the column named Endpoint in the table in [Regional Endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints-region).
-  `Access key id` - `access_key_id` obtained when the {{site.data.keyword.blockstoragefull}} instance was created.
-  `Secret access key` - `secret_access_key` to sign requests obtained when the {{site.data.keyword.blockstoragefull}} instance was created.

IAM authentication is not currently supported for this connector. You need to set up HMAC authentication before you configure this connector. See [Service Credentials](/docs/cloud-object-storage/iam?topic=cloud-object-storage-service-credentials) for instructions.
{: important}

After this information is entered, you can choose how often you want to sync your data and select the buckets you want to sync to.

Other items to note when you crawl {{site.data.keyword.blockstoragefull}}:

-  This connector does not support crawling private endpoints.
-  For more information about {{site.data.keyword.cloud_notm}} Object Storage endpoints, see [Endpoints and storage locations](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints).
-  There is a slight performance issue if all buckets are selected. In this case, a delay is possible, before the documents complete indexing.

## Installing IBM Secure Gateway for on-premises data 
{: #gatewaypublic}

<!-- Learn more topic WDS -->
To connect to an on-premises data source, you first need to download, install, and configure {{site.data.keyword.SecureGatewayfull}}. After you install {{site.data.keyword.SecureGatewayfull}} for your first on-premises data source, you do not need to repeat this process.
{: shortdesc}

You must first download, install, and configure {{site.data.keyword.SecureGatewayfull}} before you can create a [SharePoint 2016 On-Premise](/docs/discovery-data?topic=discovery-data-sources#connectsp_oppublic) collection.
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
