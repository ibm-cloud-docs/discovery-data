---

copyright:
  years: 2019
lastupdated: "2019-08-02"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}


# Creating a new collection
{: #collections}

<!-- Help for the *Collections* and *Select a Collection type* screens in WD ICP4D -->

You can create a new {{site.data.keyword.discovery-data_short}} collection or access your existing collections on the **Collections** screen.
{: shortdesc}

A collection is a set of documents you have uploaded or crawled. You can enrich, train, and query collections.

To create a new collection:

1. Click the **Collections** ![Collections](images/collection_icon.png) icon on the left.
1. Click **Create new collection**.
1. Choose the [collection type](/docs/services/discovery-data?topic=discovery-data-collection-types#collection-types):
    - **Salesforce** 
    - **SharePoint Online** 
    - **SharePoint OnPrem** 
    - **Box** 
    - **Web crawl** 
    - **Upload your own data** (no crawl or authentication information required)
1. Name your collection, and choose the language of that collection. (See [supported languages](/docs/services/discovery-data?topic=discovery-data-language-support#supported-languages) for the list).
1. Select the crawl schedule. See [Configuring collection types](/docs/services/discovery-data?topic=discovery-data-collection-types#collection-types) for available options and details.
1. Configure the authentication. See [Configuring collection types](/docs/services/discovery-data?topic=discovery-data-collection-types#collection-types) for detailed information about configuring each type.
1. Click **Create collection** to start crawling your data source. The [Collection overview](/docs/services/discovery-data?topic=discovery-data-collection-overview#collection-overview) opens and updates as documents are added to the collection. The crawl syncs the data initially and updates periodically at the frequency specified. 

The number of collections you can create is dependent upon your hardware configuration. {{site.data.keyword.discovery-data_short}} supports a maximum of 256 collections per instance/installation; however, that number is dependent upon many factors, including memory.
{: note}

To access an existing collection:

1. Click the **Collections** ![Collections](images/collection_icon.png) icon on the left. Existing collections display the document count and last updated date.
1. Select the collection you need. The [Collection overview](/docs/services/discovery-data?topic=discovery-data-collection-overview#collection-overview) displays.

On the top right of any screen, click the **Help** ![Help](images/help_icon.png) icon to open the documentation or the **Environment details** ![Env](images/env_icon.png) icon to view the storage space available and number of documents and collections in your environment. Clicking **Delete environment** deletes all the collections in your environment. Click **{{site.data.keyword.icp4dfull}}** in the upper left to open the **IBM Cloud Pak for Data** hub. 
{: tip}


## Configuring collection types
{: #collection-types}

<!-- Help for the Create Collection (SF, SP1&2, Box, WebCrawl, upload screen in WD ICP4D -->

{{site.data.keyword.discovery-data_short}} enables you to connect to and crawl documents from remote sources or upload documents.
{: shortdesc}

Each collection you [create](/docs/services/discovery-data?topic=discovery-data-collections#collections) can be configured with one data source. {{site.data.keyword.discovery-data_short}} pulls documents from that data source, using a process called crawling. Crawling is the process of systematically browsing and retrieving documents from the specified start location. {{site.data.keyword.discovery-data_short}} only crawls items that you explicitly specify. 

You can configure the following types of collection types:

-  [Box](/docs/services/discovery-data?topic=discovery-data-connectbox#connectbox)
-  [Salesforce](/docs/services/discovery-data?topic=discovery-data-connectsf#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery-data?topic=discovery-data-connectsp#connectsp)
-  [Microsoft SharePoint OnPrem](/docs/services/discovery-data?topic=discovery-data-connectsp_op#connectsp_op)
-  [Web Crawl](/docs/services/discovery-data?topic=discovery-data-connectwebcrawl#connectwebcrawl)
-  [Upload your own data](/docs/services/discovery-data?topic=discovery-data-upload-data#upload-data)

When you use a connector to create a collection and then set a crawl schedule, the initial crawl starts immediately. The frequency you choose determines when the next crawl starts in relation to the first. You can schedule crawls to update:
    
-  Hourly: runs every hour
-  Daily: runs every day at the same time as the initial crawl
-  Weekly: runs every week on the same day and time as the initial crawl
-  Monthly: runs every 30 days at the same time of day as the initial crawl
    
Example crawl status:
    
```json
"crawl_status" : {
  "source_crawl" : {
  "status" : "completed",
  "next_crawl" : "2019-02-10T05:00:00-05:00"
}
```

If you modify crawl settings on the **Sync settings** screen and then click **Save collection**, the crawl will restart immediately. See the [Collection overview](/docs/services/discovery-data?topic=discovery-data-collection-overview#collection-overview) screen for the collection status. Click the **Recrawl collection** button if the crawl does not start. 
{: note}

{{site.data.keyword.discovery-data_short}} can ingest the following file types; it ignores all other document types:
   
   - PDF
   - Microsoft Word (doc; docx)
   - Microsoft PowerPoint (ppt; pptx)
   - Microsoft Excel (xls; xlsx)
   - TXT\*
   - CSV \*
   - JSON\*
   - HTML\* 
   - PNG\*\*
   - TIFF\*\*
   - JPG\*\*
   - ZIP\*\*\*
   - GZIP\*\*\*
   - TAR\*\*\*
    
\* JSON, HTML, TXT, and CSV documents are supported by {{site.data.keyword.discovery-data_short}}, but you cannot customize fields within these files, using the Smart Document Understanding editor. CSV files must use commas (`,`) or semicolons (`;`) as delimiters; other delimiters are not supported. If your CSV file includes values containing either commas or semicolons, surround those values in double quotation marks so they are not separated. If header rows are present, the values within them are processed in the same manner as values in all other rows. 

\*\* Individual image files (PNG, TIFF, JPG) are scanned, and the text (if any) is extracted. PNG, TIFF, and JPEG images embedded in PDF, Word, PowerPoint, and Excel files are also scanned, and the text (if any) is extracted.

\*\*\*Files within compressed archive files (ZIP, GZIP, TAR) are extracted. {{site.data.keyword.discovery-data_short}} ingests the supported file types within them; it ignores all other file types. 

The following general requirements apply to all connectors:

-  The individual file size limit is 32 MB per file, including compressed archive files (ZIP, CZIP, TAR). When uncompressed, the individual files within compressed files cannot exceed 32 MB per file.
-  Each collection can only support one data source.
-  Connectors are available, only via the Tooling. 
-  [Document level security](/docs/services/discovery-data?topic=discovery-data-configuredls#configuredls) is supported with Box, SharePoint Online, and SharePoint OnPrem (2013, 2016, and 2019) connectors. 
-  You need the credentials and file locations (or URLs) for each data source, which a developer/system administrator of the data source typically provides. 
-  You need to manually provide the resources to crawl. Auto discovery is not supported. 
-  {{site.data.keyword.discovery-data_short}} source crawls do not delete documents that are stored in a collection. When a source is re-crawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the index during refresh.


## Crawling data sources
{: #data-sources}

The following sections introduce the data sources you can crawl, pre-authentication information, instructions to create a collection in each data source, and data source documentation for more information not covered here.
{:shortdesc}


### Box
{: #connectbox}

You can use this option to crawl Box. Only documents supported by {{site.data.keyword.discovery-data_short}} in your Box folders are crawled; all others are ignored.
{: shortdesc}

Before you begin, make sure you have a Box account at [Box](https://www.box.com/){: external}. Before you can crawl Box files and folders, you need to create an RSA key pair and then create and authorize a Box developer app on the [Box developer site](https://developer.box.com/){: external}.  During this process, you obtain the Public Key 1 ID and the Enterprise ID, which you need to use the Box connector. After creating your app, you need to edit it by establishing the OAuth2 parameters.

Before you create a Box developer app, you need to establish an RSA key pair. To do so:

1. Run the following shell commands:

   ```bash
   openssl genrsa 2048 > private-box.pem
   ```

   ```bash
   openssl rsa -in private-box.pem -pubout -out public-box.pem
   ```

1. Make a copy of `public-box.pem`. If you create an RSA key pair with a passphrase, you must install unlimited strength JCE Policy files (`local_policy.jar` and `US_export_policy.jar`). You can download these unlimited strength JCE Policy files from Unrestricted SDK JCE policy files. Copy these files to the persistent volume in the folder `config/certs/jvm/`, for example `config/certs/jvm/local_policy.jar` and `config/certs/jvm/US_export_policy.jar`. The certificates are imported into the JVM trust store when the container starts.

Next, create an app on the Box developer site:

1. Log in to [Box Developers](https://developer.box.com/){: external}, and create a new Enterprise Integration App.
1. Select OAuth 2.0 with JWT (Server Authentication), and create the app. 
1. View the App, and select Configuration.
1. Copy the Client ID and Client Secret. You need these items when configuring the crawler.
1. Select Enterprise as Application Access.
1. Enable all options of Application Scopes.
1. Enable Perform Actions as Users and Generate User Access Tokens options in Advanced Features.
1. Click Save Changes.
1. Click Add a Public Key and enter the content of `public-box.pem`.
1. Copy the Public Key 1 ID. You need this item when configuring the crawler.

Next, you need to authorize the app. Follow these steps:

1. Go to Admin Console.
1. Select any department, check that you are managing a team, and then click Get Started.
1. On the Admin Console, click Business Settings.
1. On the Account info tab, copy the Enterprise ID. You need this item when configuring the crawler.
1. On the Apps tab, click Authorize New App.
1. Enter the Client ID as API Key, and click Authorize. If you modify the app, you have to authorize it again.

Finally, you need to establish the OAuth2 parameters:

1. **General Information** - Ensure that your application name is correct and that the support e-mail is accurate. The support e-mail is generally defaulted to the one used to create the application. You can also provide a description of your application or a custom website URL.
1. **OAuth2 Parameters** - Set the following options:

    - `client_id` and `client_secret` - The first two items listed are your `client_id` and `client_secret`. These two items are used to authenticate, when using the Box connector. If you need to reset the `client_secret` field, you can erase what is in the provided text box and save your configuration, and your `client_secret` is reset.

    - `Authentication Type` - Select Server Authentication (OAuth2.0 with JWT).

    - `User Access` - Select All Users for the application to request authorization for access.

    - `Scopes - Content` - Check the Read and write all files and folders stored in Box option, which ensures that users authenticate to have read permissions on the files contained in your application.

    - `Scopes - Enterprise` - Check the Manage users and Manage app users options. Leave all other options unchecked.

    - `Scopes - Advanced Features` - Select the Perform actions on behalf of users and Generate access tokens for users options. Checking these options also ensures that the Managing users and App users options are checked for the `Scopes - Enterprise` parameter.

1. **Public Key Management** - Authorization to access your application requires a private and public key pair. The Add Public Key button redirects you to a screen that prompts you for your public key. Paste your public key into the provided text box, and click the Verify button. After the key is verified, click Save to finish setting up your public key. For information about authentication, see [JWT Application Setup](https://developer.box.com/docs/setting-up-a-jwt-app){: external}.


After selecting the **collection type** of **Box** and entering the **General** information:

1. Under **Authentication**, enter the:
    - **Client ID** - The private key specified by the Box App configuration.
    - **Client Secret** - The client secret specified by the Box App configuration.
    - **Private Key Path** - The path to the location of the private key that is part of the key pair generated for communication with box.com. The private key must be in DER or PEM format with either a .der or .pem extension. If the private key is encrypted, you must install the unlimited strength JCE Policy files (JAR files) previously mentioned to support AES256 encoding. Next, copy the private key to the persistent volume, named `wex-userdata`, which is mounted on gateway or ingestion pods. To mount the private key, complete the following.
        1. Log on to your {{site.data.keyword.discovery-data_short}} cluster, using `clouctl`.

        1. Find the ingestion pod by entering `kubectl get pods| grep ingestion`.

        1. Copy the files to the `/mnt` directory on the ingestion pod or the gateway pod. The copied private key files apply to all the gateway and ingestion pods. The default number of ingestion pods is 1.
    - **Private Key Passphrase** - (Optional) The passphrase required to decrypt the key if the private key is an encrypted file.
    - **Key ID** - The public key ID generated by Box.
    - **Enterprise ID** - The Enterprise ID of the Box account.
    - **Box Folder or User URL to crawl** - (Optional) Enables crawling a specific user content or folder content. If unspecified, it crawls all content. You can crawl different types of URLs, such as the following:
        - To crawl an entire enterprise, enter `box://app.box.com/`.
        - To crawl a specific folder, enter `box://app.box.com/user/USER_ID/folder/FOLDER_ID/FolderName`.
        - To crawl a specific user, enter `box://app.box.com/user/USER_ID/`.
    - **Enable Document Level Security** - This toggle is `off` by default. This option must be enabled to activate document level security. For more information, see [Configuring document level security](/docs/services/discovery-data?topic=discovery-data-configuredls#configuredls).
1. Click the **Create collection** button.

For more information about Box, see [Box developer documentation](https://developer.box.com/){: external}.


### Salesforce
{: #connectsf}

Use this option to crawl Salesforce. Only documents supported by {{site.data.keyword.discovery-data_short}} in your Salesforce folders are crawled; all others are ignored.
{: shortdesc}

Before crawling to Salesforce, you need to generate Java™ SOAP binding libraries. The following links explain how to generate the libraries. Create two libraries from Partner WSDL and Metadata WSDL.

- [Generate or Obtain the Web Service WSDL](https://developer.salesforce.com/docs/atlas.en-us.210.0.api.meta/api/sforce_api_quickstart_steps_generate_wsdl.htm){: external}
- [Import the WSDL File Into Your Development Platform](https://developer.salesforce.com/docs/atlas.en-us.210.0.api.meta/api/sforce_api_quickstart_steps_import_wsdl.htm){: external}

The following JAR files must be mounted and available in the local filesystem:

- `force-partner.jar` (from Partner WSDL)
- `force-metadata.jar` (from Metadata WSDL)
- `force-wsc.jar` (from Force Wsc)
- `commons-beanutils.jar` (from Apache Commons BeanUtils)

Use the `wex-userdata` PVC for copying the Salesforce JAR files. To copy and mount the JAR files, complete the following:

1. Log on to the {{site.data.keyword.discovery-data_short}} cluster, using `clouctl`.
1. Find the ingestion pod by entering `kubectl get pods| grep ingestion`.
1. Copy the files to the `/mnt` directory in the ingestion pod or the gateway pod. The copied JAR files apply to all the gateway and ingestion pods. The default number of ingestion pods is 1.

After selecting the **collection type** of **Salesforce** and entering the **General** information:

1. Under **Authentication**, enter the:
    - **Username** - The username to call the Salesforce API.
    - **Password** - The password of the specified user.
    - **Security Token** - The security token of the user to call Salesforce API.
    - **JARs location** - The path to the prerequisite JAR libraries. The folder that contains the JAR libraries must be mounted so it is available. 
    - **Object Types to crawl** - Specifies the object types to crawl. The default behavior is to crawl all object types. For custom object names, append `__c` to match the Salesforce API convention for custom object names. For example, regarding MyCustomObject, specify `MyCustomObject__c`. Do not specify comment objects, such as FeedComment, CaseComment, IdeaComment without FeedItem, Case, Idea, respectively. If you specify a tag object, you must also specify its parent, for example AccountTag without Account.
1. Click the **Create collection** button.

Copy the JAR files and private keys to the `ingestion-pod`.
{: important}

For more information about Salesforce, see [Salesforce developer documentation](https://developer.salesforce.com/docs/){: external}.


### SharePoint Online
{: #connectsp}

Use this option to crawl SharePoint Online. Only documents supported by {{site.data.keyword.discovery-data_short}} in your SharePoint folders are crawled; all others are ignored.
{: shortdesc}

Before you begin, be sure to obtain site collection administrator permission. Non-root site collection crawling is not supported. You can only crawl root site collections.

After selecting the **collection type** of **SharePoint Online** and entering the **General** information:

1. Under **Authentication**, enter the:
    -  **Username** - The username of the SharePoint user with  access to all sites and lists that need to be crawled and indexed.
    -  **Password** - The password of the SharePoint user. This value is never returned and is only used when creating or modifying credentials.
    -  **Site Collection URL** - The SharePoint web service URL. For example, https://wss.com/. 
    -  **Site Collection Name** - The name you must obtain from site collection settings. The name the site collection uses.
    -  **Enable Document Level Security** - By default, this toggle is `off`. You must enable this option to activate document level security and supply the application ID. For more information, see [Configuring document level security](/docs/services/discovery-data?topic=discovery-data-configuredls#configuredls).
        - **Application ID** - The Azure ID assigned to the application, upon registration. Obtain the Application ID from the SharePoint administrator. If you are configuring document level security in SharePoint Online, see [Registering with SharePoint Online](/docs/services/discovery-data?topic=discovery-data-register-sp#register-sp) for instructions.
1. Click the **Create collection** button.

#### Registering with SharePoint Online
{: #register-sp}

When you enable document level security, you need to register your app with SharePoint Online. You can register your app by logging in to the Microsoft Azure Portal, using your administrator account associated with your SharePoint Online collection in {{site.data.keyword.discovery-data_short}}. The user name is in the form of `<admin_user>@<domain>.onmicrosoft.com`. For additional steps regarding registering your app on the Azure Portal, see [Register an application with the Microsoft identity platform](https://docs.microsoft.com/en-us/graph/auth-register-app-v2){: external}. 

While registering your app, you receive an Azure application (client) ID, which you need to create and query a collection with document level security enabled. Make sure you note the application ID after you obtain it.
{: important}

Before you enter your application ID, check to make sure you add the required APIs and the permissions associated with each API. For more instructions about adding permissions, see [To configure the list of statically requested permissions for an application](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent#using-the-admin-consent-endpoint){: external} in the Using the admin consent endpoint section of the SharePoint documentation. Also, check the following table to make sure you add and apply one of the following permissions in each row. Make sure to grant the permissions after you add them by clicking the "Grant admin consent for <insert organization name>" button at the bottom of the API permissions page:

| API  | Permissions | Type   |                           
| --------------- | ------------------------------- | ------------- |
| Microsoft Graph (Groups) | `Group.Read.All` or `Group.ReadWrite.All` | Delegated |
| Microsoft Graph (Directories) | `Directory.AccessAsUser.All` or `Directory.Read.All` or `Directory.ReadWrite.All` | Delegated | 
| SharePoint Online | `User.Read.All` or `User.ReadWrite.All` | Delegated |

After you register your app:

1. In the Azure Portal, set the client type to treat it as a public client. You can set it by navigating to Authentication, then Advanced settings, and finally Default client type and setting it to Yes.
1. Enter your application ID in the **Application ID** field in {{site.data.keyword.discovery-data_short}} to enable document level security. Using the application ID you generated in this procedure, finish creating your collection, as described in [SharePoint Online](/docs/services/discovery-data?topic=discovery-data-connectsp#connectsp).

For more details on how to register an app and/or grant permissions, see [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}.


### SharePoint OnPrem
{: #connectsp_op}

Use this option to crawl SharePoint OnPrem 2013, 2016, or 2019. Only documents supported by {{site.data.keyword.discovery-data_short}} in your SharePoint folders are crawled; all others are ignored.
{: shortdesc}

Before you begin, you need to have full read access for the web application.

After selecting the **collection type** of **SharePoint OnPrem** and entering the **General** information:

1. Under **Authentication**, enter the:
    -  **Username** - The username of the SharePoint user with  access to all sites and lists that need to be crawled and indexed.
    -  **Password** - The password of the SharePoint user. This value is never returned and is only used when creating or modifying credentials.
    -  **Web Application URL** - The SharePoint web service URL. For example, https://wss.com/.
    -  **Enable SAML authentication** - This toggle is `off` by default. Enables you to use SAML claims-based authentication. The default is NTLM authentication.
        - **Identity Provider endpoint** - The URL of the Identity Provider endpoint, for example `https://adfs.server.example.com/adfs/services/trust/2005/UsernameMixed`.
        - **Relying Party endpoint** - (Optional) The URL of the Relying Party Trust endpoint. If unspecified, the following value is used: `https://<sharepoint_server>:<port>/_trust/`.
        - **Relying Party Trust identifier** - The URL of the Relying Party Trust identifier. If unspecified, the following value is used: `https://<sharepoint_server>:<port>/_trust/`. This feature is available in the 2013, 2016, and 2019 versions.
    - **Enable Document Level Security** - This toggle is `off` by default. When toggled `on`, enables search time and document level security. When you enable this option, you need to obtain the following information from the LDAP administrator. For more information, see [Configuring document level security](/docs/services/discovery-data?topic=discovery-data-configuredls#configuredls).
        - **LDAP server URL** - The LDAP server URL to connect to.
        - **LDAP binding username** - Username used to bind to the directory service. In most cases, this username is a Distinguished Name (the log-on name might sometimes work with Active Directory, though unlike the general Windows log on, it is case-sensitive. But it is recommended to use the DN, which always works). 
        - **LDAP binding user password** - Password used to bind to the directory service.
        - **LDAP base DN** - Starting point for searching user entries in LDAP (e.g., CN=Users,DC=example,DC=com).
        - **LDAP user filter** - User filter to search user entries in LDAP. If empty, default value used is `(userPrincipalName={0})`.
1. Click the **Create collection** button.

Before adding users so they can query, using document level security, you need to authorize your app by connecting to the LDAP in your app and handling it. For more information about configuring a connection to your LDAP server in your app, see [Connecting to your LDAP server](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/admin/ldap.html).

For more information about SharePoint OnPrem, see [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}.


### Web Crawl
{: #connectwebcrawl}

Use this option to crawl public websites that do not require a password. The web content is processed as HTML.
{: shortdesc}

The Web Crawl has the following properties:

**Start URLs** - The URLs where the crawler has to start crawling. By default, the Web Crawl enables subtree crawling and URLs to be crawled only from the path supplied in the seed. The starting URL in the Web Crawl has two limitations, as to what it crawls to:

   1. The same host as the start URL.
   1. The same subtree, in which "subtree" means the only crawl items where the beginning URL matches the beginning of the starting URL. Here, "beginning" means everything up to and including the last slash (`/`) in the starting URL.

**Advanced Configuration**
- **Code page to use** - The field used to enter the character encoding.

If you enter invalid information in the **Code page to use** field, the crawl slows down because there is too much load on the cluster. Three simultaneous Web Crawls is the limit you can ingest, without affecting performance.
{: note}

The default max hop limit is 16. After selecting the **collection type** of **Web crawl** and entering the **General** information:

1. Under **Configuration**, enter the first URLs you would like to crawl. Use the full URL, for example: `https://ibm.com`.
1. Click the **Add** button to add URLs.
1. Click the **Create collection** button.

After the crawl begins, you are directed to the [Collection overview](/docs/services/discovery-data?topic=discovery-data-collection-overview#collection-overview), which updates as documents are added to the collection.

If you are crawling Chinese language websites, enter `UTF-8` as the character set in the **Code page to use** field.
{: tip}


### Upload data
{: #upload-data}

Use this option to upload data you have stored locally. Only documents supported by {{site.data.keyword.discovery-data_short}} are crawled; all others are ignored.
{: shortdesc}

See [Supported document types](/docs/services/discovery-data?topic=discovery-data-collections#collections) for the list of available data sources you can use to create collections. After the upload begins, you are directed to the [Collection overview](/docs/services/discovery-data?topic=discovery-data-collection-overview#collection-overview), which updates as documents are added to the collection.


## Configuring document level security
{: #configuredls}

Document level security enables you to leverage the security settings from your source documents to control the search results returned to different users, and it is supported in the Box, SharePoint OnPrem, and SharePoint Online data sources. To enable document level security, you need to configure these components:

- Enable document level security for your collection
  See [Enable Document Level Security for SharePoint OnPrem](/docs/services/discovery-data?topic=discovery-data-connectsp_op#connectsp_op) for a description of the feature in the SharePoint OnPrem data source. Similarly, see [Enable Document Level Security for SharePoint Online](/docs/services/discovery-data?topic=discovery-data-connectsp#connectsp) for a description of the feature in this data source.
- Configure document level security parameters for your [SharePoint Online collection](/docs/services/discovery-data?topic=discovery-data-connectsp#connectsp) and your [SharePoint OnPrem collection](/docs/services/discovery-data?topic=discovery-data-connectsp_op#connectsp_op)
  Document level security configuration options are visible when document level security is enabled in your collection configuration.
- Create {{site.data.keyword.discovery-data_short}} users that match the users available on the source system
- Associate users with your {{site.data.keyword.discovery-data_short}} instance

### Creating users for document level security
{: #createusersdls}

You need to create users that match the users available on the source system that {{site.data.keyword.discovery-data_short}} is connecting to, so that they can query with document level security turned on. As an administrator, log in to {{site.data.keyword.discovery-data_short}}. Then, create users that match the users available on your source or connected to the LDAP server used on your source system:

  - To create users individually, see [Managing users](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/admin/users.html).
    For each user who you want to access query results, you need to add users, following this procedure. The username must match the username that the source uses.
    {: note}
  - To connect to an LDAP server that the source is using, see [Connecting to your LDAP server](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/admin/ldap.html).

Next, you need to associate the users you created with a {{site.data.keyword.discovery-data_short}} instance. To associate users with an instance:

1. Click the main-menu icon in the upper-left corner, and click **My instances** > **Provisioned instances**.
1. Hover over the instance you want to add users to. When you hover over your chosen instance, an expandable menu icon appears on the right side of the instance.
1. Click the expandable menu icon, and select **Manage Access**.
1. Click **Add user**.
1. Add the users you want from the drop-down list by clicking **Add user**, select the desired user from the list, assign their role as **User**, and click **Add**.

When querying collections that have document level security enabled, no results are returned if the users associated with your {{site.data.keyword.discovery-data_short}} instance are not present in the source system. For more information about querying these collections, see [Querying with document level security enabled](/docs/services/discovery-data?topic=discovery-data-querydls#querydls).
{: important}


## Collection overview
{: #collection-overview}

<!-- Help for the Collection overview screen in WD ICP4D -->

{{site.data.keyword.discovery-data_short}} provides details about each collection in the Collection overview.
{: shortdesc}

Collection details include:

-  Number of documents 
-  Collection status
    -  A collection is finished processing when the status is `Synching complete` or `Upload complete`. If processing fails, click either the **Recrawl collection** or **Reprocess collection** button. The button displayed will vary depending on the type of collection.
    -  If the collection status is `Synching ...`, and you click the **Recrawl collection** button, the current crawl will stop and a new full crawl will begin. It is recommended that you wait until the status is `Synching complete` before starting a recrawl.
-  Details (language, creation date, last update)
-  Fields identified in the collection (`text` by default). To configure additional fields, click **Data settings** ![datasettings](images/datasettings_icon.png) on the upper right to open the [**Smart Document Understanding**](/docs/services/discovery-data?topic=discovery-data-configuring-fields#configuring-fields) editor.

