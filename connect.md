---

copyright:
  years: 2019
lastupdated: "2019-08-28"

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
{:external: target="_blank" .external}


# Creating collections
{: #collections}

<!-- Help for the *Collections* and *Select a Collection type* screens in WD ICP4D -->

A collection is a set of documents you upload or crawl. You create a {{site.data.keyword.discovery-data_short}} collection on the **Collections** page. You can also enrich, train, and query collections from the **Collections** page.
{: shortdesc}


## Creating a collection
{: #createcollection}

By using collections, {{site.data.keyword.discovery-data_short}} pulls documents from a data source, using a process called crawling. Crawling is the process of systematically browsing and retrieving documents from a specified start location. {{site.data.keyword.discovery-data_short}} only crawls items that you explicitly specify.

1. Click the **Collections** ![Collections icon](images/collection_icon.png) icon on the left.
1. Click **Create new collection**.
1. Choose a collection type.
1. Name your collection, and choose the language of that collection. For a list of supported languages, see [Language support](/docs/services/discovery-data?topic=discovery-data-language-support#supported-languages).
1. Select the crawl schedule. For available options and details, see [Crawl schedule options](/docs/services/discovery-data?topic=discovery-data-crawlschedule#crawlschedule).
1. [Configure the data sources](/docs/services/discovery-data?topic=discovery-data-data-sources#data-sources).
1. Click **Create collection**, which starts the crawling process. The **Overview** tab opens and updates as documents are added to the collection. The crawl syncs the data initially and updates periodically at the specified frequency.

The number of collections you can create depends on your hardware configuration. {{site.data.keyword.discovery-data_short}} supports a maximum of 256 collections per instance and installation, but that number depends on many factors, including memory.
{: note}

If you want to access an existing collection, complete the following steps:

1. Click the **Collections** ![Collections icon](images/collection_icon.png) icon on the left. Existing collections display the document count and last updated date.
1. Select the collection you need. The **Overview** tab displays.


### Tips
{: #collectiontips}

- To open the documentation, click the **Help** ![Help icon](images/help_icon.png) icon on the top right of any screen.
- To view the available storage space and the number of documents and collections in your environment, click the **Environment details** ![Environment details icon](images/env_icon.png) icon.
- To delete all the collections in your environment, click **Delete environment**.
- To open the **IBM Cloud Pak for Data** hub, click **{{site.data.keyword.icp4dfull}}** in the upper left.


## Configuring data sources
{: #collection-types}

<!-- Help for the Create Collection (SF, SP1&2, Box, WebCrawl, upload screen in WD ICP4D -->

In {{site.data.keyword.discovery-data_short}}, you can crawl documents you upload or connect to from a remote data source. The following sections introduce supported data sources, pre-authentication information, instructions about how to configure a collection, and links to third-party documentation for more information.
{:shortdesc}

Depending on your data source, the steps to configure a collection vary. See the section for your data source to learn what you must do to configure the authentication for a {{site.data.keyword.discovery-data_short}} collection. 

You can configure the following data sources:

-  [Box](/docs/services/discovery-data?topic=discovery-data-connectbox#connectbox)
-  [Salesforce](/docs/services/discovery-data?topic=discovery-data-connectsf#connectsf)
-  [Microsoft SharePoint Online](/docs/services/discovery-data?topic=discovery-data-connectsp#connectsp)
-  [Microsoft SharePoint OnPrem](/docs/services/discovery-data?topic=discovery-data-connectsp_op#connectsp_op)
-  [Web crawl](/docs/services/discovery-data?topic=discovery-data-connectwebcrawl#connectwebcrawl)
-  [Database](/docs/services/discovery-data?topic=discovery-data-databaseconnect#databaseconnect)
-  [Windows File System](/docs/services/discovery-data?topic=discovery-data-windowsfilesystemconnect#windowsfilesystemconnect)
-  [Upload your own data](/docs/services/discovery-data?topic=discovery-data-upload-data#upload-data)


### Crawl schedule options
{: #crawlschedule}

When you create a collection, the initial crawl starts immediately. The frequency you choose for the crawl schedule determines when the next crawl starts in relation to the first. You can schedule crawls to update at the following intervals:
    
-  Hourly: runs every hour
-  Daily: runs every day at the same time as the initial crawl
-  Weekly: runs every week on the same day and time as the initial crawl
-  Monthly: runs every 30 days at the same time as the initial crawl
    
Example crawl status:
    
```json
"crawl_status" : {
  "source_crawl" : {
  "status" : "completed",
  "next_crawl" : "2019-02-10T05:00:00-05:00"
}
```
{: codeblock}

If you modify crawl settings on the **Sync settings** page and then click **Save collection**, the crawl restarts immediately. To view the collection status, see the **Overview** tab. 
{: note}


### Connector and file type requirements
{: #connectorrequirements}

A connector is a component that provides data connectivity and extraction capabilities for external data sources. In {{site.data.keyword.discovery-data_short}}, you establish a connector during the process of creating a collection for a data source.

The following general requirements apply to all connectors:

-  The individual file size limit is 32 MB per file, which includes compressed archive files (ZIP, CZIP, TAR). When uncompressed, the individual files within compressed files cannot exceed 32 MB per file.
-  Each collection can support only one data source.
-  Connectors are not available when you use the API. 
-  [Document level security](/docs/services/discovery-data?topic=discovery-data-configuredls#configuredls) is supported for the following connectors: Box, SharePoint Online, SharePoint OnPrem (2013, 2016, and 2019), and Windows File System (Windows Server 2012 R2, 2016, and 2019). 
-  You need the credentials and file locations, or URLs, for each data source, which a developer or system administrator of the data source typically provides. 
-  You need to manually provide the resources to crawl. Auto discovery is not supported. 
-  Crawls do not delete documents that are stored in a collection. When a source is re-crawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the index during refresh.
-  Depending on the type of installation (default or high availability), the number of collections you can ingest simultaneously varies. A default installation includes 1 ingestion pod, which allows three collections to be processed simultaneously. A high availability installation includes 2 ingestion pods, which can process six collections simultaneously.

     If you are running a default installation and you want to process more than three collections simultaneously, you must increase the number of ingestion pods by running the following commands:

     ```bash
     kubectl edit statefulset <ingestion-statefulset>
     kubectl scale statefulset release-name-watson-discovery-ingestion --replicas=<number-of-replicas>
     ```
     {: pre}

     In a default installation, the maximum number of simultaneous collections performing crawls or uploads is three. If you start a fourth, that collection does not start to process until the prior three finish.
     {: note}

     Each `number-of-replicas` allows 3 simultaneous crawls, so `number-of-replicas=2` increases the replicas to 6, and `number-of -replicas=3` increases them to 9.


### Supported file types
{: #supportedfiletypes}

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
    
\* JSON, HTML, TXT, and CSV documents are supported by {{site.data.keyword.discovery-data_short}}, but you cannot customize fields within these files using the Smart Document Understanding editor. 

\*\* Individual image files (PNG, TIFF, JPG) are scanned, and any text is extracted. PNG, TIFF, and JPEG images embedded in PDF, Word, PowerPoint, and Excel files are also scanned, and any text is extracted.

\*\*\*Files within compressed archive files (ZIP, GZIP, TAR) are extracted. {{site.data.keyword.discovery-data_short}} ingests the supported file types within them; it ignores all other file types.


### Box
{: #connectbox}

You can use this option to crawl Box. Only documents supported by {{site.data.keyword.discovery-data_short}} in your Box folders are crawled; all others are ignored.
{: shortdesc}


#### Creating an app on Box
{: #boxappcreate}

1. Make sure you have a [Box account](https://www.box.com/){: external}. During this process, you obtain the public key 1 ID and the enterprise ID, which you need to enter later in {{site.data.keyword.discovery-data_short}} to configure a Box collection.

1. Establish an RSA key pair.

   1. Run the following shell commands:

     ```bash
     openssl genrsa 2048 > private-box.pem
     ```
     {: pre}

     ```bash
     openssl rsa -in private-box.pem -pubout -out public-box.pem
     ```
     {: pre}

   1. Make a copy of `public-box.pem`. 
   
      If you create an RSA key pair with a passphrase, you must install unlimited strength JCE Policy files, or JAR files (`local_policy.jar` and `US_export_policy.jar`). You can download these unlimited strength JCE Policy files from Unrestricted SDK JCE policy files. Copy these files to the persistent volume in the folder `config/certs/jvm/`, for example `config/certs/jvm/local_policy.jar` and `config/certs/jvm/US_export_policy.jar`. The certificates are imported into the JVM trust store when the container starts.
      {: note}

1. Next, create an app on the Box developer site. Log in to your [Box Developers account](https://developer.box.com/){: external}, and create a new enterprise integration app. After you log in to your Box account, make sure you complete the following tasks:

   - In **Authentication Method**, click **OAuth 2.0 with JWT (Server Authentication)**. 
   - Copy the client ID and client secret. You need this information later when configuring a {{site.data.keyword.discovery-data_short}} Box collection.
   - In **User Access**, select **All Users** for the application to request authorization for access.
   - In **Application Access**, click **Enterprise**.
   - In **Application Scopes**, select all the check boxes. Selecting the **Read and write all files and folders stored in Box** check box ensures that users must authenticate to have read permissions in the files contained in your application.
   - In **Advanced Features**, set **Perform Actions as Users** and **Generate User Access Tokens** to on. Setting these switches to on ensures that the **Managing users** and **App users** options are checked for **Scopes - Enterprise**.
   - When you add a public key, enter the content of `public-box.pem` that you generated when you created the RSA key pair.
   - Copy the public key 1 ID. You need this information later when configuring a {{site.data.keyword.discovery-data_short}} Box collection.

1. Next, you must authorize the app. In the Box admin console, complete the following tasks:

   - In the **App info** pane on the **General** page, copy the **Enterprise ID**, which you must enter later in {{site.data.keyword.discovery-data_short}} when you configure a Box collection.
   - Enter the client ID in the **API Key** field, and authorize your new app. You copied the client ID when you created the app. If you modify the app later, you must reauthorize it.

1. Establish the OAuth2 parameters. Make sure that you complete the following tasks:

   - On the **General** page, ensure that your app name is correct. You can also provide a description of your app or a custom website URL.
   - Under **Public Key Management**, paste your public key into the provided text box, and click **Verify**.
   - After the key is verified, click **Save** to finish setting up your public key.

For more information about setting up your application, see [JWT Application Setup](https://developer.box.com/docs/setting-up-a-jwt-app){: external}.

The field names and functions in Box might change. Consult the [Box developer documentation](https://developer.box.com/){: external} for updates.
{: note}


#### Configuring a Box collection
{: #configurebox}

In {{site.data.keyword.discovery-data_short}}, after you select **Box** as the collection type, enter the following information:

1. Complete the **Authentication** fields:
    - **Client ID** - The private key specified while you configure your Box app.
    - **Client Secret** - The client secret specified while you configure your Box app.
    - **Private Key Path** - The path to the location of the private key that is part of the key pair generated for communication with the Box website. The private key must be in DER or PEM format with either a .der or .pem extension. If the private key is encrypted, you must install the unlimited strength JCE Policy files (JAR files) previously mentioned to support AES256 encoding. Next, copy the private key to the persistent volume, named `wex-userdata`, which is mounted on gateway or ingestion pods. Mount the private key by completing the following steps:

        1. Log on to your {{site.data.keyword.discovery-data_short}} cluster, using `clouctl`.
        1. Find the ingestion pod by entering `kubectl get pods| grep ingestion`.
        1. Copy the files to the `/mnt` directory on the ingestion pod or the gateway pod. The copied private key files apply to all the gateway and ingestion pods. The default number of ingestion pods is 1.

    - **Private Key Passphrase** - Optional: The passphrase required to decrypt the key if the private key is an encrypted file.
    - **Key ID** - The public key ID generated by Box.
    - **Enterprise ID** - The Enterprise ID of the Box account.
    - **Box Folder or User URL to crawl** - Optional: Enables crawling a specific user content or folder content. If unspecified, it crawls all content. You can crawl different types of URLs. See the following examples of URLs that you can specify to crawl user or folder content:

        - To crawl an entire enterprise, enter `box://app.box.com/`.
        - To crawl a specific folder, enter `box://app.box.com/user/USER_ID/folder/FOLDER_ID/FolderName`.
        - To crawl a specific user, enter `box://app.box.com/user/USER_ID/`.

    - **Enable Document Level Security** - By default, this switch is set to **off**. You must enable this option to activate document level security. When enabled, this option ensures that users can crawl and query content they have access to when logged in to Box. For more information, see [About document level security](/docs/services/discovery-data?topic=discovery-data-configuredls#configuredls).
1. Click **Create collection**.


### Salesforce
{: #connectsf}

Use this option to crawl Salesforce. Only documents supported by {{site.data.keyword.discovery-data_short}} in your Salesforce folders are crawled; all others are ignored.
{: shortdesc}


#### Downloading and copying JAR files to your cluster
{: #download-copy-files}

For information about downloading the JAR files, see the following links:

   - [Generate or Obtain the Web Service WSDL](https://developer.salesforce.com/docs/atlas.en-us.210.0.api.meta/api/sforce_api_quickstart_steps_generate_wsdl.htm){: external}
   - [Import the WSDL File Into Your Development Platform](https://developer.salesforce.com/docs/atlas.en-us.210.0.api.meta/api/sforce_api_quickstart_steps_import_wsdl.htm){: external}
   - [Download Apache Commons BeanUtils](https://commons.apache.org/proper/commons-beanutils/download_beanutils.cgi){: external}
   - [Apache Commons BeanUtils](https://mvnrepository.com/artifact/commons-beanutils/commons-beanutils){: external}

1. Download the following JAR files:

   - `force-partner.jar` (from partner WSDL)
   - `force-metadata.jar` (from metadata WSDL)
   - `force-wsc.jar` (from Force.com Web Service Connector (WSC))
   - `commons-beanutils.jar` (from Apache Commons BeanUtils)

1. In the local filesystem, mount and make available the downloaded JAR files.
1. Create a directory called `wex-userdata`, and copy the JAR files to that directory.
1. Log on to the {{site.data.keyword.discovery-data_short}} cluster, using `clouctl`.
1. Find the ingestion pod by entering `kubectl get pods| grep ingestion`.
1. Copy the JAR files to the `/mnt` directory in the ingestion pod or the gateway pod in your cluster. The copied JAR files apply to all the gateway and ingestion pods. The default number of ingestion pods is 1.


#### Configuring a Salesforce collection
{: #configuresf}

In {{site.data.keyword.discovery-data_short}}, after you select **Salesforce** as the collection type, enter the following information:

1. Complete the **Authentication** fields:
    - **Username** - The user name to call the Salesforce API.
    - **Password** - The password of the specified user.
    - **Security Token** - The security token of the user to call Salesforce API.
    - **JARs location** - The path to the prerequisite JAR libraries. The folder that contains the JAR libraries must be mounted so it is available. 
    - **Object Types to crawl** - Specifies the object types to crawl. The default behavior is to crawl all object types. For custom object names, append `__c` to match the Salesforce API convention for custom object names. For example, regarding MyCustomObject, specify `MyCustomObject__c`. Do not specify comment objects, such as FeedComment, CaseComment, IdeaComment without FeedItem, Case, Idea, respectively. If you specify a tag object, you must also specify its parent. For example, do not specify the AccountTag object without the Account object.
1. Click **Create collection**.

For more information about Salesforce, see [Salesforce developer documentation](https://developer.salesforce.com/docs/){: external}.


### SharePoint Online
{: #connectsp}

Use this option to crawl SharePoint Online. Only documents supported by {{site.data.keyword.discovery-data_short}} in your SharePoint folders are crawled; all others are ignored.
{: shortdesc}


#### Prerequisites
{: #spprerequisites}

Before you begin, be sure to obtain site collection administrator permission. Non-root site collection crawling is not supported. You can only crawl root site collections.


#### Configuring a SharePoint Online collection
{: #configuresp}

In {{site.data.keyword.discovery-data_short}}, after you select **Sharepoint Online** as the collection type, enter the following information:

1. Complete the **Authentication** fields:
    -  **Username** - The user name of the SharePoint user with  access to all sites and lists that need to be crawled and indexed.
    -  **Password** - The password of the SharePoint user. This value is never returned and is used only when creating or modifying credentials.
    -  **Site Collection URL** - The SharePoint web service URL. For example, `http://www.example.com/`. 
    -  **Site Collection Name** - The name you must obtain from site collection settings. The name the site collection uses.
    -  **Enable Document Level Security** - By default, this switch is set to **off**. You must enable this option to activate document level security, and after enabling it, you must supply the application ID. When enabled, this option ensures that users can crawl and query content they have access to. For more information, see [About document level security](/docs/services/discovery-data?topic=discovery-data-configuredls#configuredls).
        - **Application ID** - The Azure ID assigned to the application, upon registration. Obtain the Application ID from the SharePoint administrator. If you are configuring document level security in SharePoint Online, see [App registration with SharePoint Online](/docs/services/discovery-data?topic=discovery-data-register-sp#register-sp) for instructions.
1. Click **Create collection**.


#### App registration with SharePoint Online
{: #register-sp}

When you enable document level security, you must register your app with SharePoint Online. You can register your app by logging in to the Microsoft Azure Portal, using your administrator account associated with your SharePoint Online collection in {{site.data.keyword.discovery-data_short}}. The user name is in the form of `<admin_user>@<domain>.onmicrosoft.com`. For additional steps regarding registering your app on the Azure Portal, see [Register an application with the Microsoft identity platform](https://docs.microsoft.com/en-us/graph/auth-register-app-v2){: external}. 

While registering your app, you receive an Azure application (client) ID, which you need to create and query a collection with document level security enabled. Make sure you note the application ID after you obtain it.
{: important}

Before you enter your application ID, check to make sure you add the required APIs and the permissions associated with each API. For information about configuring the list of statically requested permissions for an application, see [Using the admin consent endpoint](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent#using-the-admin-consent-endpoint){: external}. Also, check the following table to make sure you add and apply one of the permissions in each row:

| API  | Permissions | Type   |                           
| --------------- | ------------------------------- | ------------- |
| Microsoft Graph (Groups) | `Group.Read.All` or `Group.ReadWrite.All` | Delegated |
| Microsoft Graph (Directories) | `Directory.AccessAsUser.All` or `Directory.Read.All` or `Directory.ReadWrite.All` | Delegated | 
| SharePoint Online | `User.Read.All` or `User.ReadWrite.All` | Delegated |

After you register your app, check to make sure you completed the following steps:

- In the Azure Portal, the client type is set to be treated as a public client.
- Your application ID is entered in the **Application ID** field in {{site.data.keyword.discovery-data_short}} so that document level security is enabled.

Using the application ID you generated in this procedure, you can finish creating your collection, as described in [Configuring a SharePoint Online collection](/docs/services/discovery-data?topic=discovery-data-configuresp#configuresp).

For more details on how to register an app or how to grant permissions, see [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}.


### SharePoint OnPrem
{: #connectsp_op}

Use this option to crawl SharePoint OnPrem 2013, 2016, or 2019. Only documents supported by {{site.data.keyword.discovery-data_short}} in your SharePoint folders are crawled; all others are ignored.
{: shortdesc}


#### Prerequisites
{: #sp_opprerequisites}

Before you begin, you need to have full read access for the web application.


#### Configuring a SharePoint OnPrem collection
{: #configuresp_op}

In {{site.data.keyword.discovery-data_short}}, after you select **Sharepoint OnPrem** as the collection type, enter the following information:

1. Complete the **Authentication** fields:
    -  **Username** - The user name of the SharePoint user with access to all sites and lists that need to be crawled and indexed.
    -  **Password** - The password of the SharePoint user. This value is never returned and is only used when creating or modifying credentials.
    -  **Web Application URL** - The SharePoint web service URL. For example, `http://www.example.com/`.
    -  **Enable SAML authentication** - By default, this switch is set to **off**. When set to **on**, you can use SAML claims-based authentication. The default is NTLM authentication.
        - **Identity Provider endpoint** - The URL of the Identity Provider endpoint, for example `https://adfs.server.example.com/adfs/services/trust/2005/UsernameMixed`.
        - **Relying Party endpoint** - Optional: The URL of the Relying Party Trust endpoint. If unspecified, the following value is used: `https://<sharepoint_server>:<port>/_trust/`.
        - **Relying Party Trust identifier** - The URL of the Relying Party Trust identifier. If unspecified, the following value is used: `https://<sharepoint_server>:<port>/_trust/`. This feature is available in the 2013, 2016, and 2019 versions.
    - **Enable Document Level Security** - By default, this switch is set to **off** by default. When set to **on**, it enables search time and document level security. When you enable this option, you need to obtain the following information from the LDAP administrator. For more information, see [About document level security](/docs/services/discovery-data?topic=discovery-data-configuredls#configuredls):
        - **LDAP server URL** - The LDAP server URL to connect to.
        - **LDAP binding username** - User name used to bind to the directory service. In most cases, this user name is a distinguished name (DN). The logon name might sometimes work with Active Directory. But unlike the general Windows logon, it is case-sensitive. It is recommended to use the DN, which always works. 
        - **LDAP binding user password** - Password used to bind to the directory service.
        - **LDAP base DN** - Starting point for searching user entries in LDAP, for example `CN=Users,DC=example,DC=com`.
        - **LDAP user filter** - User filter to search user entries in LDAP. If unspecified, the default value used is `(userPrincipalName={0})`.

          Before adding users so they can query using document level security, you need to authorize your app by connecting to the LDAP in your app and handling it. For more information about configuring a connection to your LDAP server in your app, see [Connecting to your LDAP server](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/admin/ldap.html).
          {: important}

1. Click **Create collection**.

For more information about SharePoint OnPrem, see [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}.


### Web crawl
{: #connectwebcrawl}

Use this option to crawl public websites that do not require a password. The web content is processed as HTML, and the default maximum hop limit is 16.
{: shortdesc}


#### Configuring a web crawl collection
{: #configurewebcrawl}

In {{site.data.keyword.discovery-data_short}}, after you select **Web crawl** as the collection type, enter the following information:

1. Complete the following field in **Configuration**:
    -  **Start URLs** - The URLs where the crawler begins crawling. By default, the web crawl enables subtree crawling and URLs to be crawled only from the path supplied in the seed. Use the full URL, for example `http://www.example.com/`. The start URL in the web crawl has two limitations as to what is crawled:
       - It crawls the same domain name as the start URL.
       - It crawls all URL content up to and including the last slash (`/`) in **Start URLs**. If your start URL has a subtree, the web crawl does not crawl that subtree, unless you specify its URL in **Start URLs**.

1. Click the **Add** button to add one or more start URLs.
1. If applicable, complete the following **Advanced Configuration** field:
    -  **Code page to use** - The field used to enter the character encoding. If unspecified, the default value used is `UTF-8`.

       If you are crawling Chinese websites, enter `UTF-8` as the character set in the **Code page to use** field.
       {: tip}

1. Click **Create collection**.

After the crawl begins, the **Overview** tab opens and updates as documents are added to the collection.


### Database
{: #databaseconnect}

Use this option to crawl documents from IBM Db2, Microsoft SQL Server, Postgresql, Oracle, and other databases that support JDBC. {{site.data.keyword.discovery-data_short}} supports the following data source versions:

- IBM Db2: 10.5, 11.1, 11.5
- Microsoft SQL Server: 2012, 2014, 2016, 2017
- Oracle Database: 11g, 12c, 18c, 19c
- Postgres: 9.4, 9.5, 9.6, 10, 11

Only documents supported by {{site.data.keyword.discovery-data_short}} are crawled; all others are ignored.
{: shortdesc}


#### Copying Database JAR files
{: #copydatabasefiles}

Before you create a Database collection, complete the following steps:

1. Copy the Oracle DB, Postgres, MSSQL, Db2, or JDBC JAR files associated with the database you want to crawl.
1. Log on to your {{site.data.keyword.discovery-data_short}} cluster, using `clouctl`.
1. Find the ingestion pod by entering `kubectl get pods| grep ingestion`.
1. Copy the files to the `/mnt` directory on the ingestion pod or the gateway pod. The default number of ingestion pods is 1.


#### Configuring a Database collection
{: #configuredatabase}

In {{site.data.keyword.discovery-data_short}}, after you select **Database** as the collection type, enter the following information:

1. Complete the **Authentication** fields:
    -  **JDBC Driver Type** - The default is **DB2**. Lists the four databases that {{site.data.keyword.discovery-data_short}} supports: Db2, Microsoft SQL Server, Postgresql, and Oracle. If you want to crawl from another database that is not listed, select **OTHER**.
    -  **JDBC Driver Classname** - The JDBC driver class name you obtain from the database you select. Depending on the database you select in **JDBC Driver Type**, this field is autofilled, except if you select **OTHER**.
    -  **JDBC Driver Classpath** - The file path where you copy the JAR files from and the location of the JDBC driver. You must mount the folder that contains the JAR file so that it is available. See the following list for examples of driver classpaths:
       - Db2 - `/mnt/jdbc/db2jcc4.jar`
       - Oracle - `/mnt/jdbc/ojdbc8.jar`
       - SQL Server - `/mnt/jdbc/mssql-jdbc-7.2.2.jre8.jar`
       - Postgresql - `/mnt/jdbc/postgresql-42.2.6.jar`
    -  **Database URL** - The main URL to the database you select. See the following list for examples of database URLs:
       - Db2 - `jdbc:db2://localhost:50000/sample`
       - Oracle - `jdbc:oracle:thin:@localhost:1521:sample`
       - SQL Server - `jdbc:sqlserver://localhost:1433;DatabaseName=sample`
       - Postgresql - `jdbc:postgresql://localhost/sample`
    -  **User** - Your user name that you obtain from the database you selected. You use this user name to crawl the source. Your user name is different from database to database.
    -  **Password** - Your password that you obtain from the database you selected. Your password is associated with your user name. Your password is different from database to database.
    -  **Schema Name** - The schema you want to crawl data from. You obtain the schema name from the database you are crawling.
    -  **Table Name** - The table within a schema you want to crawl data from. You obtain the table name from the database you are crawling.
1. Click **Create collection**.


### Windows File System
{: #windowsfilesystemconnect}

Use this option to crawl Windows file systems from the {{site.data.keyword.discovery-data_short}} server. The Windows File System connector supports the Windows Server 2012 R2, 2016, and 2019 versions. Only documents supported by {{site.data.keyword.discovery-data_short}} are crawled; all others are ignored.
{: shortdesc}


#### Installing the agent server
{: #agentinstall}

Before configuring a Windows File System collection, you must install the agent server on a remote Windows file server or on a remote Windows server. If you install the agent server on a remote Windows server, the remote Windows server must be able to mount one or more file servers so that the agent can crawl remote Windows file systems. The agent server is a Windows service that retrieves data from data source servers and sends data to {{site.data.keyword.discovery-data_short}}. The Windows agent can crawl remote Windows file systems, the agent local drives, and shared network folders.
{: shortdesc}

1. Log in to {{site.data.keyword.discovery-data_short}} as an admin, and navigate to **Windows File System**.
1. Under **Download & install Windows Agent**, click **Download Windows Installer**. Clicking this link downloads the .zip file to run the agent installer.
1. Follow the prompts. While the installer runs, you receive the host name, user name, password, agent authentication port number, and port number that you enter later in Windows File System on {{site.data.keyword.discovery-data_short}}, so note them when you receive them. Also during installation, a check box appears that, when checked, enables you to create a user account; when unchecked, it assigns you administrative permissions.
1. Extract all files in the `WindowsAgentServer.zip`.
1. Double-click the `install.exe` file, or enter `install.exe` in a command window. You can choose one of the following methods to run the installation program:

   - Console installation - To run the installation program in text mode from a console, complete the following steps:
     1. Change to the agent directory.
     1. Enter the following command:
         ```bash
         install.exe -i console
         ```
         {: pre}

        The screens are rendered in text and prompt you for the same information as the graphical installation.

        After you enter the command, a process runs in the background for several seconds before the console installation program displays.
        {: note}

   - Silent installation - To install the product silently, complete the following steps:
     1. Change to the `Agent/responseFiles` directory.
     1. Edit the `DistributedFileSystemCrawler.properties` template response file to provide information about your environment. To run the installation program, change to the agent directory, and specify the name of the file that you edited. See the following example:
         ```bash
         install.exe -i silent -f responseFiles/DistributedFileSystemCrawler.properties
         ```
         {: pre}

      If you copy a template file to another location to edit, specify the fully qualified path for the file when you run the installation program. If the response file path includes a space, enclose the path in double quotation marks (`"`). See the following example:
      ```bash
      install.exe -i silent -f "c:\My Documents\DistributedFileSystemCrawler.properties"
      ```
      {: pre}

1. Specify installation options by entering or verifying the fully qualified host name of the computer you are installing the agent server on.

   You cannot specify an IPv6 address as the host name of the server.
   {: important}

1. Enter a user name and password of an account that can be used to authorize access to the agent server. When you configure the agent for Windows File System in the administration console, you must specify this user name and password. If the user name does not exist, you can select the check box to create the account. 

   To crawl a domain in a secure collection, the user name must be an existing domain user that has permission to access the files to be crawled. To specify a domain user, use the format `<username>@<domain name>`. The agent installation program does not create the domain user.
   {: important}

1. Click **Install** to use the default settings for all other installation options and to start installing the software.
1. Optional: If you want to change the default settings, click **Advanced Options**, instead of clicking **Install**. Use the following guidelines when you specify advanced installation options:

   - You can change the paths for the installation directory and data directory.
   - The agent server uses three TCP/IP ports for authenticating connections to the server, transferring data between the file systems and {{site.data.keyword.discovery-data_short}}, and monitoring the agent server. The default port numbers are `8397` and `8398`. If those values conflict with other port assignments in your system, change the port numbers.

1. On the summary page, review the options that you selected, and click **Install** to start installing the software.
1. Restart your computer.


#### Configuring shared directories on the agent server
{: #shareddirectories}

After the software is installed, you must set up shared network directories that the Windows File System agent can access. To define a new file system share, you export a local or remote network directory. You can also list the shares that are already defined or delete a share that you previously defined.
{: shortdesc}

1. Export a local directory from the server where the agent is installed:
   ```bash
   esagent --addshare <d:><\example>
   ```
   {: pre}

   Where `d:` represents the drive letter you want to use and where `\example` represents the path to the local directory.
1. Export a remote network directory that is accessible from the server where the agent is installed:
   ```bash
   esagent --addshare <\\files.example.com\data>
   ```
   {: pre}

   Where `\\files.example.com\data` represents the host name or IP address of the remote server or the path to the remote directory. 
1. List shares that are defined on the server where the agent is installed:
   ```bash
   esagent --lsshare
   ```
   {: pre}

1. Delete a share that is defined on the server where the agent is installed:
   ```bash
   esagent --rmshare \\files.example.com\data
   ```
   {: pre}


#### Server status commands
{: #serverstatuscommands}

After you install the agent server, you can enter commands to start, stop, and see the status of the server. Use the following commands to start or stop the agent server. Stopping the agent server also stops the crawler. For example, if the crawler stops unexpectedly, you can close connections and release resources for that crawler.

Enter the following command to start the server:

```bash
esagent start
```
{: pre}

Enter the following command to stop the server:

```bash
esagent stop
```
{: pre}

Enter the following command to get the status of the agent server:

```bash
esagent getStatus
```
{: pre}

The output of the `getStatus` command is an XML file in the following output:

```bash
<AgentStatus>
  <SpaceStatus>
    <SpaceId>012</SpaceId>
    <RootFolder>E:\\Projects\Analytics\\data\test1</RootFolder>
    <ConnectionNumber>9</ConnectionNumber>
    <StartTime>1244709336093</StartTime>
    <LastTime>1244709385843</LastTime>
    <IdlePeriod>219</IdlePeriod>
  </SpaceStatus>
  <SpaceStatus>
    <SpaceId>013</SpaceId>
    <RootFolder>E:\\Projects\Analytics\\data\test2</RootFolder>
    <ConnectionNumber>10</ConnectionNumber>
    <StartTime>1244709336093</StartTime>
    <LastTime>1244709385843</LastTime>
    <IdlePeriod>219</IdlePeriod>
  </SpaceStatus>
  ```
  {: screen}


#### Configuring a Windows File System collection
{: #configurewindowsfilesystem}

In {{site.data.keyword.discovery-data_short}}, after you select **Windows File System** as the collection type, enter the following information:
 
1. Complete the **Authentication** fields:
    -  **Host** - The host name that Windows agent is installed on. You obtain the host name when you install the agent server.
    -  **User** - The user name to connect the agent server, which you obtain when you install the agent server. Enables {{site.data.keyword.discovery-data_short}} to connect to the shared network folders and crawl content.
    -  **Password** - The password of the specified user, which you obtain when you install the agent server. Enables {{site.data.keyword.discovery-data_short}} to connect to the shared network folders and crawl content.
    -  **Agent Authentication Port** - The default port value is `8397`. The port for authenticating, which you obtain when you install the agent server.
    -  **Port** - The default port value is `8398`. The port for transferring data, which you obtain when you install the agent server.
    -  **Enable Document Level Security** - By default, this switch is set to **off**. You must enable this option to activate document level security. When enabled, this option ensures that users can crawl and query content they have access to. For more information about Document Level Security, see [About document level security](/docs/services/discovery-data?topic=discovery-data-configuredls#configuredls).
         - **LDAP server URL** - The LDAP server URL to connect to.
         - **LDAP binding username** - User name used to bind to the directory service. In most cases, this user name is a DN. The logon name might sometimes work with Active Directory. But unlike the general Windows logon, it is case-sensitive. It is recommended to use the DN, which always works.
         - **LDAP binding user password** - Password used to bind to the directory service.
         - **LDAP base DN** - Starting point for searching user entries in LDAP, for example `CN=Users,DC=example,DC=com`. 
         - **LDAP user filter** - User filter to search user entries in LDAP. If empty, default value used is `(userPrincipalName={0})`.
1. Complete the following field in **Configuration**:
    - **Path** - The file path that you need to enter to crawl documents from. You can enter multiple file paths.
1. After entering the path, click **Add** to the right of the field to add one or more file paths.
1. Click **Create collection**.

When you specify a file path in **Path**, the letter case in this path must be the same as the letter case in the file path you specified when you configured the shared directories on the agent server. For example, if you configure the shared directories on the agent server as `C:\Foo\Test`, you must enter `C:\Foo\Test` as the file path in **Path** when you create a collection in Windows File System. If you do not match the letter case in both file paths exactly, you receive an error message, and your collection does not generate.
{: important}

The remote agent server and the file servers to be crawled must belong to the same Windows domain. A crawler can gather access control list (ACL) data from a single Windows domain.
{: important}


### Upload data
{: #upload-data}

Use this option to upload data you stored locally. Only documents supported by {{site.data.keyword.discovery-data_short}} are crawled; all others are ignored.
{: shortdesc}

See [Configuring data sources](/docs/services/discovery-data?topic=discovery-data-data-sources#data-sources) for the list of supported data sources you can use to create collections. After the upload begins, the **Overview** tab opens and updates as documents are added to the collection.


## Collection overview
{: #collection-overview}

<!-- Help for the Collection overview screen in WD ICP4D -->

{{site.data.keyword.discovery-data_short}} provides details about each collection in the **Overview** tab.
{: shortdesc}

Collection details include the following information:

-  Number of documents 
-  Collection status
    -  A collection is finished processing when the status is `Syncing complete` or `Upload complete`. If processing fails, click either the **Recrawl collection** or **Reprocess collection** button. The button displayed varies, depending on the type of collection.
    -  If the collection status is `Syncing ...`, and you click the **Recrawl collection** button, the current crawl stops, and a new full crawl begins. It is recommended that you wait until the status is `Syncing complete` before starting a recrawl.
-  Details (language, creation date, last update)
-  Fields identified in the collection (`text` by default). To configure additional fields, click **Data settings** ![Data Settings icon](images/datasettings_icon.png) on the upper right to open the [**Smart Document Understanding**](/docs/services/discovery-data?topic=discovery-data-configuring-fields#configuring-fields) editor. 


## About document level security
{: #configuredls}

Document level security enables you to leverage the security settings from your source documents to control the search results returned to different users, and it is supported in the Box, SharePoint OnPrem, SharePoint Online, and Windows File System data sources.

To enable document level security, you must configure these components:

- Enable document level security for your collection.
  - For a description of the feature in the SharePoint OnPrem data source, see [Enable Document Level Security for SharePoint OnPrem](/docs/services/discovery-data?topic=discovery-data-configuresp_op#configuresp_op).
  - For a description of the feature in SharePoint Online, see [Enable Document Level Security for SharePoint Online](/docs/services/discovery-data?topic=discovery-data-configuresp#configuresp).
  - For a description of the feature in Windows File System and the information required to configure a collection, consult [Enable Document Level Security for Windows File System](/docs/services/discovery-data?topic=discovery-data-configurewindowsfilesystem#configurewindowsfilesystem).
- Configure document level security parameters for your [SharePoint Online collection](/docs/services/discovery-data?topic=discovery-data-configuresp#configuresp), [SharePoint OnPrem collection](/docs/services/discovery-data?topic=discovery-data-configuresp_op#configuresp_op), or [Windows File System collection](/docs/services/discovery-data?topic=discovery-data-configurewindowsfilesystem#configurewindowsfilesystem).
  Document level security configuration options are visible when document level security is enabled in your collection configuration.
- Create {{site.data.keyword.discovery-data_short}} users that match the users available on the source system.
- Associate users with your {{site.data.keyword.discovery-data_short}} instance.

{{site.data.keyword.discovery-data_short}} only supports pre-filtering. Pre-filtering involves replicating the document's source ACL at crawl time into the index and relying on the search engine to compare user credentials to the replicated document ACLs. {{site.data.keyword.discovery-data_short}} performs the best when documents are pre-filtered and when you control which documents you add to the index. However, it is difficult to model all of the security policies of the various back-end sources in the index and implement comparison logic uniformly. Also, pre-filtering is not as responsive to any changes that might occur in the source ACLs after the most recent crawl.
{: note}


### Creating users for document level security
{: #createusersdls}

You must create users that match the users available on the source system that {{site.data.keyword.discovery-data_short}} is connecting to so that they can query with document level security turned on.
{: shortdesc}

1. As an administrator, log in to {{site.data.keyword.discovery-data_short}}.
1. Create users who match the users available on your source or who are connected to the LDAP server used on your source system.

   - To create users individually, see [Managing users](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/admin/users.html). For each user who you want to access query results, you need to add users, following the instructions in this link. The user name must match the user name that the source uses.
   - To connect to an LDAP server that the source is using, see [Connecting to your LDAP server](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/admin/ldap.html).


### Associating users with an instance
{: #associateusersdls}

1. Click the main-menu icon in the upper-left corner, and click **My instances** > **Provisioned instances**.
1. Hover over the instance you want to add users to. When you hover over your chosen instance, an expandable menu icon appears on the right side of the instance.
1. Click the expandable menu icon, and select **Manage Access**.
1. Click **Add user**.
1. Add the users you want from the list by clicking **Add user**, select the desired user from the list, assign their role as **User**, and click **Add**.

When querying collections that have document level security enabled, no results are returned if the users associated with your {{site.data.keyword.discovery-data_short}} instance are not present in the source system. For more information about querying these collections, see [Querying with document level security enabled](/docs/services/discovery-data?topic=discovery-data-querydls#querydls).
{: important}

Because {{site.data.keyword.discovery-data_short}} does not sync any changes to the users from the LDAP server, {{site.data.keyword.discovery-data_short}} administrators must ensure that the users list is current and remove any non-current users.
{: note}
