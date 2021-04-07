---

copyright:
  years: 2019, 2021
lastupdated: "2021-04-07"

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


# Configuring Cloud Pak for Data data sources 
{: #collection-types}

<!-- 2.1.3 c/s help for the *Select a Data Source* page CP4D. Do not delete. -->

In {{site.data.keyword.discovery-data_short}}, you can crawl documents you upload or connect to from a remote data source. The following sections introduce supported data sources, pre-authentication information, instructions about how to configure a collection, and links to third-party documentation for more information. For information about {{site.data.keyword.cloud_notm}} data sources, see [Configuring {{site.data.keyword.cloud_notm}} data sources](/docs/discovery-data?topic=discovery-data-sources).
{:shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{:note}

Depending on your data source, the steps to configure a collection vary. See the section for your data source to learn what you must do to configure the authentication for a {{site.data.keyword.discovery-data_short}} collection.

You can use {{site.data.keyword.discovery-data_short}} to crawl from the following data sources:

-  [Box](#connectbox)
-  [Salesforce](#connectsf)
-  [Microsoft SharePoint Online](#connectsp)
-  [Microsoft SharePoint OnPrem](#connectsp_op)
-  [Web crawl](#connectwebcrawl)
-  [Database](#databaseconnect)
-  [Windows File System](#windowsfilesystemconnect)
-  [Local File System](#localfilesystemconnect)
-  [FileNet P8](#filenet-connect)
-  [Notes](#connectnotes)
-  [Uploading data](/docs/discovery-data?topic=discovery-data-upload-data)
-  [Reuse data from an existing collection](#reuse)

*Your data source isn't listed?* You can work with a developer to create a custom connector. For more information, see [Building a Cloud Pak for Data custom connector](/docs/discovery-data?topic=discovery-data-build-connector).

If you have special requirements that you need to address when you add source documents to a collection, such as excluding certain files, you can work with a developer to create a custom crawler plug-in. The crawler plug-in can apply more nuanced rules to what documents and what fields in the documents get added. For more information, see [Building a Cloud Pak for Data custom crawler plug-in](/docs/discovery-data?topic=discovery-data-crawler-plugin-build).

## Processing settings
{: #processing-options}

You can specify an additional option for this collection:
 
-  **Run OCR (Optical Character Recognition)** - Extracts text from images, using Optical Character Recognition (OCR).

## Data source requirements
{: #requirements}

The following requirements and limitations are specific to {{site.data.keyword.discoveryfull}}:

-  The individual file size limit is 32 MB per file, which includes compressed archive files (ZIP, CZIP, TAR). When uncompressed, the individual files within compressed files cannot exceed 32 MB per file. This limit is the same for collections in which you upload your own data.
-  [Document level security](#configuredls) is supported for the following connectors: Box, SharePoint Online, SharePoint OnPrem (2013, 2016, and 2019), Windows File System (Windows Server 2012 R2, 2016, and 2019), FileNet P8, and Notes.
-  When a source is re-crawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the index during refresh.
-  Depending on the type of installation (default or production mode), the number of collections you can ingest simultaneously varies. A default installation includes 1 crawler pod, which allows three collections to be processed simultaneously. A production installation includes 2 crawler pods, which can process six collections simultaneously.

     If you are running a default installation and you want to process more than three collections simultaneously, you must increase the number of crawler pods by running the following commands:

     ```bash
     oc patch wd wd --type=merge --patch='{"spec": {"ingestion": {"crawler": {"replicas": <number-of-replicas> } } } }'
     ```
     {: pre}

     In a default installation, the maximum number of simultaneous collections performing crawls is 3. If you start a fourth, that collection does not start to process until the prior three finish.
     {: note}

     Each `number-of-replicas` allows 3 simultaneous crawls, so `number-of-replicas=2` increases the replicas to 6, and `number-of -replicas=3` increases them to 9.


### Box
{: #connectbox}

You can use this option to crawl Box. Only documents supported by {{site.data.keyword.discoveryshort}} in your Box folders are crawled; all others are ignored.
{: shortdesc}


#### Creating an app on Box
{: #boxappcreate}

1. Make sure you have a [Box account](https://www.box.com/){: external}. During this process, you obtain the public key 1 ID and the enterprise ID.

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
   
      If you create an RSA key pair with a passphrase, you must install unlimited strength JCE Policy files, or .jar files (`local_policy.jar` and `US_export_policy.jar`). You can download these unlimited strength JCE Policy files from Unrestricted SDK JCE policy files. Copy these files to the persistent volume in the folder `config/certs/jvm/`, for example `config/certs/jvm/local_policy.jar` and `config/certs/jvm/US_export_policy.jar`. The certificates are imported into the JVM trust store when the container starts.
      {: note}

1. Next, create an app on the Box developer site. Log in to your [Box Developers account](https://developer.box.com/){: external}, and create a new enterprise integration app. After you log in to your Box account, make sure you complete the following tasks:

   - In **Authentication Method**, click **OAuth 2.0 with JWT (Server Authentication)**.
   - Copy the client ID and client secret.
   - In **User Access**, select **All Users** for the application to request authorization for access.
   - In **Application Access**, click **Enterprise**.
   - In **Application Scopes**, select all the check boxes. Selecting the **Read and write all files and folders stored in Box** check box ensures that users must authenticate to have read permissions in the files contained in your application.
   - In **Advanced Features**, set **Perform Actions as Users** and **Generate User Access Tokens** to on. Setting these switches to on ensures that the **Managing users** and **App users** options are checked for **Scopes - Enterprise**.
   - When you add a public key, enter the content of `public-box.pem` that you generated when you created the RSA key pair.
   - Copy the public key 1 ID.

1. Next, you must authorize the app. In the Box admin console, complete the following tasks:

   - In the **App info** pane on the **General** page, copy the **Enterprise ID**.
   - Enter the client ID in the **API Key** field, and authorize your new app. You copied the client ID when you created the app. If you modify the app later, you must reauthorize it.

1. Establish the OAuth2 parameters. Make sure that you complete the following tasks:

   - On the **General** page, ensure that your app name is correct. You can also provide a description of your app or a custom website URL.
   - Under **Public Key Management**, paste your public key into the provided text box, and click **Verify**.
   - After the key is verified, click **Save** to finish setting up your public key.

1. After you receive your client ID, client secret, private key path, private key passphrase, key ID, and enterprise ID on the configuration page on [Box Developers](https://developer.box.com/){: external}, download the app settings as a JSON file, or `config.json`.

For more information about setting up your application, see [JWT Application Setup](https://developer.box.com/docs/setting-up-a-jwt-app){: external}.

The field names and functions in Box might change. Consult the [Box developer documentation](https://developer.box.com/){: external} for updates.
{: note}


#### Configuring a Box collection
{: #configurebox}

In {{site.data.keyword.discoveryshort}}, after you select **Box** as the collection type, enter the following information:

1. Click the following button in the **Box JSON configuration** section in **Enter your credentials**:
    - **Select file** - Upload the `config.json` file that contains your client ID, client secret, private key path, private key passphrase, key ID, and enterprise ID. You can download this JSON file from the configuration page on [Box Developers](https://developer.box.com/){: external}.
1. Complete the following field in **Specify what you want to crawl**:
    - **Box Folder or User URL to crawl** - Optional: Crawls a specific user content or folder content. If unspecified, it crawls all content. You can crawl different types of URLs. See the following examples of URLs that you can specify to crawl user or folder content:

        - To crawl an entire enterprise, enter `box://app.box.com/`.
        - To crawl a specific folder, enter `box://app.box.com/user/USER_ID/folder/FOLDER_ID/FolderName`.
        - To crawl a specific user, enter `box://app.box.com/user/USER_ID/`.

1. Optional: Set the following switch in **Proxy settings**:
    -  **Enable proxy settings** - By default, is set to **Off**. Enable this option when you are using the proxy server to access the data source server.
        -  **Username** - Optional: The username that you use to authenticate, if the proxy server requires authentication. If you do not know your username, you can obtain it from the administrator of the proxy server.
        -  **Password** - Optional: The password that you use to authenticate, if the proxy server requires authentication. If you do not know your password, you can obtain it from the administrator of the proxy server.
        -  **Proxy server host name or IP address** - The host name or the IP address of the proxy server.
        -  **Proxy server port number** - The network port that you want to connect to on the proxy server.

1. Optional: Set the following switch in **Security**:
    - **Enable Document Level Security** - By default, this switch is set to **Off**. You must enable this option to activate document level security. When this option is enabled, your users can crawl and query content that they have access to when logged in to Box. For more information, see [About document level security](#configuredls).
1. Click **Finish**.


### Salesforce
{: #connectsf}

Use this option to crawl Salesforce. Only documents supported by {{site.data.keyword.discoveryshort}} in your Salesforce folders are crawled; all others are ignored.
{: shortdesc}


#### Downloading JAR files
{: #download-copy-files}

For information about downloading the .jar files, see the following links:

   - [Generate or Obtain the Web Service WSDL](https://developer.salesforce.com/docs/atlas.en-us.210.0.api.meta/api/sforce_api_quickstart_steps_generate_wsdl.htm){: external}
   - [Import the WSDL File Into Your Development Platform](https://developer.salesforce.com/docs/atlas.en-us.210.0.api.meta/api/sforce_api_quickstart_steps_import_wsdl.htm){: external}
   - [Download Apache Commons BeanUtils](https://commons.apache.org/proper/commons-beanutils/download_beanutils.cgi){: external}
   - [Apache Commons BeanUtils](https://mvnrepository.com/artifact/commons-beanutils/commons-beanutils){: external}

1. Download the following .jar files:

   - `force-partner.jar` (from partner WSDL)
   - `force-metadata.jar` (from metadata WSDL)
   - `force-wsc.jar` (from Force.com Web Service Connector (WSC))
   - `commons-beanutils.jar` (from Apache Commons BeanUtils)

1. Compress the .jar files into a .zip file, which you must upload to {{site.data.keyword.discoveryshort}}.


#### Configuring a Salesforce collection
{: #configuresf}

In {{site.data.keyword.discoveryshort}}, after you select **Salesforce** as the collection type, enter the following information:

1. Complete the following fields in **Specify what you want to crawl**:
    - **Username** - The username to call the Salesforce API.
    - **Password** - The password of the specified user.
    - **Security Token** - The security token of the user to call Salesforce API.
    - **Jar zip archive file** - Upload a .zip file that contains the .jar files that you downloaded in [Downloading JAR files](#download-copy-files). You can also select or delete a .zip file that you previously uploaded.
1. Complete the following field in **Object Types**:
    - **Object Types to crawl** - Specifies the object types to crawl. The default behavior is to crawl all object types. For custom object names, append `__c` to match the Salesforce API convention for custom object names. For example, regarding MyCustomObject, specify `MyCustomObject__c`. Do not specify comment objects, such as FeedComment, CaseComment, IdeaComment without FeedItem, Case, Idea, respectively. If you specify a tag object, you must also specify its parent. For example, do not specify the AccountTag object without the Account object.
1. Click **Finish**.

For more information about Salesforce, see [Salesforce developer documentation](https://developer.salesforce.com/docs/){: external}.


### SharePoint Online
{: #connectsp}

Use this option to crawl SharePoint Online. Only documents supported by {{site.data.keyword.discoveryshort}} in your SharePoint folders are crawled; all others are ignored.
{: shortdesc}


#### Prerequisites
{: #spprerequisites}

Before you begin, be sure to obtain site collection administrator permission. Non-root site collection crawling is not supported. You can only crawl root site collections.


#### Configuring a SharePoint Online collection
{: #configuresp}

In {{site.data.keyword.discoveryshort}}, after you select **Sharepoint Online** as the collection type, enter the following information:

1. Complete the following fields in **Enter your credentials**:
    -  **Username** - The username of the SharePoint user with  access to all sites and lists that need to be crawled and indexed, for example `<crawl_username>@<company_name>.onmicrosoft.com`.
    -  **Password** - The password of the SharePoint user. This value is never returned and is used only when creating or modifying credentials.
1. Complete the following fields in **Specify what you want to crawl**:
    -  **Site Collection Url** - The SharePoint web service URL, for example `https://<organization_name>.com`.
    -  **Site Collection Name** - The name you must obtain from site collection settings. The name the site collection uses.
1. Optional Set the following switch in **Proxy settings**:
    -  **Enable proxy settings** - By default, is set to **Off**. Enable this option when you are using the proxy server to access the data source server.
         -  **Username** - Optional: The proxy server username to authenticate, if the proxy server requires authentication. If you do not know your username, you can obtain it from the administrator of your proxy server.
         -  **Password** - Optional: The proxy server password to authenticate, if the proxy server requires authentication. If you do not know your password, you can obtain it from the administrator of your proxy server.
         -  **Proxy server host name or IP address** - The host name or the IP address of the proxy server.
         -  **Proxy server port number** -  The network port that you want to connect to on the proxy server.
1. Optional: Set the following switch in **Security**:
    -  **Enable Document Level Security** - By default, this switch is set to **Off**. You must enable this option to activate document level security, and after enabling it, you must supply the application ID. When this option is enabled, your users can crawl and query content that they have access to. For more information, see [About document level security](#configuredls).
        - **Application ID** - The Azure ID assigned to the application, upon registration. Obtain the Application ID from the SharePoint administrator. If you are configuring document level security in SharePoint Online, see [App registration with SharePoint Online](#register-sp) for instructions.
1. Click **Finish**.


#### App registration with SharePoint Online
{: #register-sp}

When you enable document level security, you must register your app with SharePoint Online. You can register your app by logging in to the Microsoft Azure Portal, using your administrator account associated with your SharePoint Online collection in {{site.data.keyword.discoveryshort}}. The username is in the form of `<admin_user>@<domain>.onmicrosoft.com`. For additional steps regarding registering your app on the Azure Portal, see [Register an application with the Microsoft identity platform](https://docs.microsoft.com/en-us/graph/auth-register-app-v2){: external}. 

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
- Your application ID is entered in the **Application ID** field in {{site.data.keyword.discoveryshort}} so that document level security is enabled.

Using the application ID you generated in this procedure, you can finish creating your collection, as described in [Configuring a SharePoint Online collection](#configuresp).

For more information on how to register an app or how to grant permissions, see [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}.


### SharePoint OnPrem
{: #connectsp_op}

Use this option to crawl SharePoint OnPrem 2013, 2016, or 2019. Only documents supported by {{site.data.keyword.discoveryshort}} in your SharePoint folders are crawled; all others are ignored.
{: shortdesc}


#### Obtaining the web services package from your Discovery cluster
{: #sp_opprerequisites}

Before you create a SharePoint OnPrem collection, you must have full read access for the web application.

In addition, before you create a SharePoint OnPrem collection, you must obtain a web services package from your {{site.data.keyword.discoveryshort}} cluster. This web services package is a custom module that the crawler uses to obtain the necessary information to crawl successfully. Complete the following steps to obtain the web services package from your {{site.data.keyword.discoveryshort}} cluster:

1. Log in to your {{site.data.keyword.discoveryshort}} cluster.
1. Enter the following command to obtain your crawler pod name:

   ```
   oc get pods | grep crawler
   ```
   {: pre}

   You might see output that is similar to the following:

   ```
   wd-discovery-crawler-57985fc5cf-rxk89     1/1     Running     0          85m
   ```

1. Enter the following command to obtain the `ESSPSolution.wsp` file, replacing `{crawler-pod-name}` with the crawler pod name that you obtained in step 2:

   ```
   oc exec {crawler-pod-name} -- ls -l /opt/ibm/wex/zing/resources/ | grep ESSPSolution
   ```
   {: pre}

   You might see output that is similar to the following:

   ```
   -rw-r--r--. 1 dadmin dadmin  8600 Feb  3 08:23 ESSPSolution-${build-version}.wsp
   ```

1. Enter the following command to copy the `ESSPSolution.wsp` file to the host server, replacing `{build-version}` with the build version number from the previous step and `{crawler-pod-name}` with the crawler pod name from step 2:

   ```
   oc cp {crawler-pod-name}:/opt/ibm/wex/zing/resources/ESSPSolution-${build-version}.wsp ESSPSolution.wsp
   ```
   {: pre}

After you obtain the web services package from your {{site.data.keyword.discoveryshort}} cluster, you must deploy the web services on the SharePoint server. For information about deploying the web services package on the SharePoint server, see [Deploying the web services on the SharePoint server](#deploy-web-services).

#### Deploying the web services on the SharePoint server
{: #deploy-web-services}

To support farm-aware crawling, you must next deploy the web services package that is bundled in your {{site.data.keyword.discoveryshort}} crawler pod on the SharePoint server. You can either manually deploy the web services on the SharePoint server or run a script that automatically deploys them. Refer to the following task to run the script that automatically deploys the web services:

1. Run the `ESSPSolution.wsp` script on the SharePoint server by entering the following Windows PowerShell cmdlet: `Add-SPSolution -LiteralPath C:\files\ESSPSolution.wsp`
1. In SharePoint, open SharePoint Central Administration and then system settings.
1. Deploy tbe package by using farm solutions.
1. Select the `esspsolution.wsp` solution, and deploy the solution. After the deployment is complete, the farm solution is listed in the SharePoint administration console. An administrator can enable or disable the solution and can schedule triggers.
1. Optional: Regardless of the approach that you used to deploy the web services, to complete the deployment in some environments, you might need to apply the following configurations to the IIS server that hosts the SharePoint server and the web services:
   
   - Allow .NET impersonation on IIS
   - Change the ASP.NET trust level to WSS_Medium

   You can apply these configurarations in the Internet Information Services Manager.

For information about obtaining the web services package from your {{site.data.keyword.discoveryshort}} cluster, see [Obtaining the web services package from your Discovery cluster](#sp_opprerequisites).


#### Configuring a SharePoint OnPrem collection
{: #configuresp_op}

In {{site.data.keyword.discoveryshort}}, after you select **Sharepoint OnPrem** as the collection type, enter the following information:

1. Complete the following fields in **Enter your credentials**:
    -  **Username** - The username of the SharePoint user with access to all sites and lists that need to be crawled and indexed.
    -  **Password** - The password of the SharePoint user. This value is never returned and is only used when creating or modifying credentials.
1. Optional: Set the following switch:
    -  **Enable SAML authentication** - By default, this switch is set to **Off**. When set to **On**, you can use SAML claims-based authentication. The default is NTLM authentication.
         - **Identity Provider endpoint** - The URL of the Identity Provider endpoint, for example `https://adfs.server.example.com/adfs/services/trust/2005/UsernameMixed`.
         - **Relying Party endpoint** - Optional: The URL of the Relying Party Trust endpoint. If unspecified, the following value is used: `https://<sharepoint_server>:<port>/_trust/`.
         - **Relying Party Trust identifier** - The URL of the Relying Party Trust identifier, for example `urn:sharepoint:sample`. If unspecified, the following value is used: `https://<sharepoint_server>:<port>/_trust/`. This feature is available in the 2013, 2016, and 2019 versions.
1. Complete the following field in **Specify what you want to crawl**:
    -  **Web Application Url** - The SharePoint web service URL, for example `https://<host>:<port>`.
    
1. Optional: Set the following switch in **Proxy settings**:
    -  **Enable proxy settings** - By default, is set to **Off**. Enable this option when you are using the proxy server to access the data source server.
         -  **Username** - Optional: The proxy server username to authenticate, if the proxy server requires authentication. If you do not know your username, you can obtain it from the administrator of your proxy server.
         -  **Password** - Optional: The proxy server password to authenticate, if the proxy server requires authentication. If you do not know your password, you can obtain it from the administrator of your proxy server.
         -  **Proxy server host name or IP address** - The host name or the IP address of the proxy server.
         -  **Proxy server port number** -  The network port that you want to connect to on the proxy server.
1. Optional: Set the following switch in **Security**:
    - **Enable Document Level Security** - By default, this switch is set to **Off**. When set to **On**, search time and document level security is activated. When you enable this option, you need to obtain the following information from the LDAP administrator. For more information, see [About document level security](#configuredls):
        - **LDAP server URL** - The LDAP server URL to connect to, for example `ldap://<ldap_server>:<port>`.
        - **LDAP binding username** - The username used to bind to the directory service. In most cases, this username is a distinguished name (DN). The logon name might sometimes work with Active Directory. But unlike the general Windows logon, it is case-sensitive. It is recommended to use the DN, which always works.
        - **LDAP binding user password** - The password used to bind to the directory service.
        - **LDAP base DN** - The starting point for searching user entries in LDAP, for example `CN=Users,DC=example,DC=com`.
        - **LDAP user filter** - The user filter to search user entries in LDAP. If unspecified, the default value is `(userPrincipalName={0})`.

          Before adding users so they can query using document level security, you need to authorize your app by connecting to the LDAP in your app and handling it. For more information about configuring a connection to your LDAP server in your app, see [Connecting to your LDAP server](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/admin/ldap.html).
          {: important}

1. Click **Finish**.

For more information about SharePoint OnPrem, see [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}.


### Web crawl
{: #connectwebcrawl}

Use this option to crawl websites. The web content is processed as HTML.
{: shortdesc}


#### Configuring a web crawl collection
{: #configurewebcrawl}

In {{site.data.keyword.discoveryshort}}, after you select **Web crawl** as the collection type, enter the following information:

1. Complete the following field in **Specify where you want to crawl**:
    -  **Starting URLs** - The URLs where the crawler begins crawling. By default, the web crawl can crawl subtrees, and URLs can only be crawled from the path supplied in the seed. Use the full URL, for example `http://www.example.com/`. The start URL in the web crawl has two limitations as to what is crawled:
       - It crawls the same domain name as the start URL.
       - It crawls all URL content up to and including the last slash (`/`) in **Starting URLs**. If your start URL has a subtree, the web crawl does not crawl that subtree, unless you specify its URL in **Starting URLs**.

1. Click the **Add** button to add one or more starting URLs. After you add one or more starting URLs, you can click **Authentication settings** and select one of three authentication types to apply to your chosen starting URL: **Basic authentication**, **NTLM authentication**, or **FORM authentication**. Complete the following fields for your chosen authentication type:
   
   **Basic authentication**
     -  **Username** - The username of the user for authentication.
     -  **Password** - The password of the user for authentication.

   **NTLM authentication**
     -  **Username** - The username of the user for authentication.
     -  **Password** - The password of the user for authentication.
     -  **NTLM domain name** - The NTLM domain name that belongs to the user who is authenticating.
     -  **NTLM host name** - The host name of the NTLM server.

   **FORM authentication**
     1. In **Form type**, select one of the following options:
        -  **Direct** - Click this option if you do not want to fetch the login page.
        -  **Indirect** - Click this option if you want to fetch the login page and you want to fill the parameters in the login form.
     1. Complete the following fields:
        -  **Form login url** - This field is required if you select the **Indirect** form type.
        -  **Form action url** - The form action URL that is required to submit the form.
        -  **Form name** - This field is required if you select the **Indirect** form type.
     1. In **Form method**, select either **POST** or **GET**.
     1. Complete the following fields:
        -  **Form parameters** - The list of the key-value pairs of form parameters. Complete the **Key** and **Value** fields, and click **+** to add one or more form parameters.
   
1. Optional: Under **Proxy Settings**, set the following switch:
    -  **Enable Proxy Settings** - Is set to **Off** by default. When you set **Enable Proxy Settings** to **On**, you activate proxy authentication for the starting URLs that you want to crawl.
       - **Username** - The username that you use to authenticate with a proxy server. You can obtain your username from the website administrator.
       - **Password** - The password that you use to authenticate with a proxy server. You can obtain your password from the website administrator.
       - **Proxy server domain(s)** - The domain(s) that the host resides in. You can specify a wildcard in this field, such as an asterisk (`*`) to crawl all domains or a leading asterisk (`*.server1.bar.com`) to crawl domains that match a pattern.
       - **Proxy server host name or IP address** - The host name, if you want to access the server by using a LAN, or the IP address of the server that you want to use as the proxy server.
       - **Proxy server port number** - The network port that you want to connect to on the proxy server.

1. Optional: Complete the following fields in **Advanced Configuration**:
    -  **Code page to use** - The field used to enter the character encoding. If unspecified, the default value used is `UTF-8`.

       If you are crawling Chinese websites, enter `UTF-8` as the character set in **Code page to use**.
       {: tip}

    -  **URL Path Depth** - The depth of a website to crawl, indicated by subtrees in a link. For example, `https://www.example.com/some/more/examples/index.html` has a path depth of 4, `/some/more/examples/index`. You can only enter a positive value. If unspecified, the default value is `5`. The maximum path depth is `20`.
    -  **Maximum hops** - The number of consecutive links to follow from the start URL. If unspecified, the default value is `5`. The maximum number of links that you can follow is `20`. If you want to disable this field, enter `-1`, but if you want to enable it, enter a positive value. You can only crawl links that are within the hop. If there is a link that you want to crawl that is out of reach of the hop, you must enter that link in **Starting URLs** to crawl the web page.
1. Optional: Set the following switch:
    -  **Ignore certificate** - If you enable this option, ignores any SSL certificates that are present on websites. This option only applies to HTTPS websites.
1. Click **Finish**.

After the crawl begins, the **Activity** tab opens and updates as documents are added to the collection.

If the web pages are updated after your initial crawl, the sync frequency is adjusted.
{: note}


### Database
{: #databaseconnect}

Use this option to crawl documents from IBM Db2, Microsoft SQL Server, Postgresql, Oracle, and other databases that support JDBC. {{site.data.keyword.discoveryshort}} supports the following data source versions:

- IBM Db2: 10.5, 11.1, 11.5
- Microsoft SQL Server: 2012, 2014, 2016, 2017
- Oracle Database: 11g, 12c, 18c, 19c
- Postgres: 9.4, 9.5, 9.6, 10, 11

Only documents supported by {{site.data.keyword.discoveryshort}} are crawled; all others are ignored.
{: shortdesc}


#### Copying Database JAR files
{: #copydatabasefiles}

1. Copy the Oracle DB, Postgres, MSSQL, Db2, or JDBC .jar files that are associated with the database that you want to crawl. See the following list for the .jar files that are associated with each database:
   - Db2 - `db2jcc4.jar`
   - Oracle - `ojdbc8.jar`
   - SQL Server - `mssql-jdbc-7.2.2.jre8.jar`
   - Postgresql - `postgresql-42.2.6.jar`
1. Compress the .jar files into a .zip file. If you have a JDBC driver that has one .jar file, you do not need to compress the .jar file into a .zip file; simply upload the .jar file in {{site.data.keyword.discoveryshort}}.


#### Configuring a Database collection
{: #configuredatabase}

Before you complete the fields in **Enter your credentials**, you might want to check that the user credentials are associated with a user who has restricted permissions to access the tables that you want to crawl.

Before you complete the fields in **Specify what you want to crawl**, keep the following points in mind if you crawl multiple tables:

- You can crawl multiple tables in a collection, and you can specify tables that have different schema, or sets of columns.
- If you crawl multiple tables that have columns with the same name but different data types, the data in one of the tables is excluded from the index. For example, if you have two tables that have columns called `DATA` and the `DATA` column in one table is populated with dates and the column in the other table is populated with strings, the data in one of the tables is excluded from the index. In this case, to resolve a column name conflict, use a `VIEW`.

Only in content mining projects, columns that have such a conflict are assigned fields that have a data type suffix, such as `DATA_string`. To see if data types are excluded from the index, click **Warnings and errors** in the **Activity** tab.
{: note}

In {{site.data.keyword.discoveryshort}}, after you select **Database** as the collection type, enter the following information:

1. Complete the following fields in **Enter your credentials**:
    -  **Database URL** - The main URL to the database you select. The format of the database URL is `jdbc:<database_type>://<path>:<port>`. See the following list for examples of database URLs:
       - Db2 - `jdbc:db2://localhost:50000/sample`
       - Oracle - `jdbc:oracle:thin:@localhost:1521:sample`
       - SQL Server - `jdbc:sqlserver://localhost:1433;DatabaseName=sample`
       - Postgresql - `jdbc:postgresql://localhost/sample`
    -  **User** - Your username that you obtain from the database you selected. You use this username to crawl the source. Your username is different from database to database.
    -  **Password** - Your password that you obtain from the database you selected. Your password is associated with your username. Your password is different from database to database.
1. Complete the following fields in **Connection settings**:
    -  **JDBC driver type** - The default is **DB2**. Lists the four databases that {{site.data.keyword.discoveryshort}} supports: Db2, Microsoft SQL Server, Postgresql, and Oracle. If you want to crawl from another database that is not listed, select **OTHER**.
    -  **JDBC driver classname** - The JDBC driver class name you obtain from the database you select. Depending on the database you select in **JDBC Driver Type**, this field is autofilled, except if you select **OTHER**.
    -  **JDBC driver classpath** - Upload a JDBC driver file, which can have a .jar or .zip file extension. You can select or delete a .jar or .zip file that you previously uploaded.
1. Complete the following fields in **Specify what you want to crawl**:
    -  **Schema Name** - The schema you want to crawl data from. You obtain the schema name from the database you are crawling.
    -  **Table Name** - The table within a schema you want to crawl data from. You obtain the table name from the database you are crawling.
         
         After you complete the **Schema name** and **Table name** fields and click **Add**, you can click the edit icon to access the **Table crawl settings** dialog box, where you can enter input in the following fields:
         -  **Primary key** - The primary key of the target database table. If the primary key is not configured in the target database table, you must complete this field. The JDBC database crawler appends this primary key value to the URL of each crawled row to keep its uniqueness. When the primary key is a composite key, concatenate the key names by using a comma, for example `key1,key2`. If unspecified, the project defaults to the primary key fields of the table. If the primary key is configured in the target database table, this key is automatically detected.
         -  **Row filter** - Optional: Specify the `SQL WHERE` clause to designate which table rows to crawl. You must specify a Boolean expression that can be the condition of a `WHERE` clause in a `SELECT` statement. If there is an error in syntax or column names, the table is excluded from the crawl, and no documents are indexed. In this case, update the condition, and click **Apply changes and reprocess**.
1. Click **Finish**.


### Windows File System
{: #windowsfilesystemconnect}

Use this option to crawl Windows file systems from the {{site.data.keyword.discoveryshort}} server. The Windows File System connector supports the Windows Server 2012 R2, 2016, and 2019 versions. Only documents supported by {{site.data.keyword.discoveryshort}} are crawled; all others are ignored.
{: shortdesc}


#### Installing the agent server
{: #agentinstall}

Before configuring a Windows File System collection, you must install the agent server on a remote Windows file server or on a remote Windows server. If you install the agent server on a remote Windows server, the remote Windows server must be able to mount one or more file servers so that the agent can crawl remote Windows file systems. The agent server is a Windows service that retrieves data from data source servers and sends data to {{site.data.keyword.discoveryshort}}. The Windows agent can crawl remote Windows file systems, the agent local drives, and shared network folders.
{: shortdesc}

1. Log in to {{site.data.keyword.discoveryshort}} as an admin, and navigate to **Windows File System**.
1. Under **Download & install Windows Agent**, click **Download Windows Agent Installer**. Clicking this link downloads the .zip file to run the agent installer.
1. Follow the prompts. While the installer runs, you receive the host name, username, password, agent authentication port number, and port number that you enter later in Windows File System on {{site.data.keyword.discoveryshort}}, so note them when you receive them. Also during installation, a check box appears that, when you check it, you can use to create a user account; when the check box is unchecked, you have administrative permissions.
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

1. Enter a username and password of an account that can be used to authorize access to the agent server. When you configure the agent for Windows File System in the administration console, you must specify this username and password. If the username does not exist, you can select the check box to create the account. 

   To crawl a domain in a secure collection, the username must be an existing domain user that has permission to access the files to be crawled. To specify a domain user, use the format `<username>@<domain name>`. The agent installation program does not create the domain user.
   {: important}

1. Click **Install** to use the default settings for all other installation options and to start installing the software.
1. Optional: If you want to change the default settings, click **Advanced Options**, instead of clicking **Install**. Use the following guidelines when you specify advanced installation options:

   - You can change the paths for the installation directory and data directory.
   - The agent server uses three TCP/IP ports for authenticating connections to the server, transferring data between the file systems and {{site.data.keyword.discoveryshort}}, and monitoring the agent server. The default port numbers are `8397` and `8398`. If those values conflict with other port assignments in your system, change the port numbers.

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

In {{site.data.keyword.discoveryshort}}, after you select **Windows File System** as the collection type, enter the following information:
 
1. Complete the following fields in **Enter your credentials**:
    -  **Host** - The host name of the remote Microsoft Windows server, for example `<hostname>.mydomain.com`. You obtain the host name when you install the agent server.
    -  **Username** - The username to connect the agent server, which you obtain when you install the agent server. You use your username to connect {{site.data.keyword.discoveryshort}} to the shared network folders and crawl content.
    -  **Password** - The password of the specified user, which you obtain when you install the agent server. You use your password to connect {{site.data.keyword.discoveryshort}} to the shared network folders and crawl content.
    -  **Agent Authentication Port** - The default port value is `8397`. The port for authenticating, which you obtain when you install the agent server.
    -  **Port** - The default port value is `8398`. The port for transferring data, which you obtain when you install the agent server.
1. Complete the following field in **Specify what you want to crawl**:
    - **Path** - The file path that you need to enter to crawl documents from. You can enter multiple file paths.
1. Enter one or more paths, and click **Add**.
1. Optional: Set the following switch in **Security**:
    -  **Enable Document Level Security** - By default, this switch is set to **Off**. You must enable this option to activate document level security. When you enable this option, your users can crawl and query content that they have access to. For more information about Document Level Security, see [About document level security](#configuredls).
         - **LDAP server URL** - The LDAP server URL to connect to, for example `ldap://<ldap_server>:<port>`.
         - **LDAP binding username** - The username used to bind to the directory service. In most cases, this username is a DN. The logon name might sometimes work with Active Directory. But unlike the general Windows logon, it is case-sensitive. It is recommended to use the DN, which always works.
         - **LDAP binding user password** - The password used to bind to the directory service.
         - **LDAP base DN** - The starting point for searching user entries in LDAP, for example `CN=Users,DC=example,DC=com`. 
         - **LDAP user filter** - The user filter to search user entries in LDAP. If empty, the default value is `(userPrincipalName={0})`.

1. Click **Finish**.

When you specify a file path in **Path**, the letter case in this path must be the same as the letter case in the file path you specified when you configured the shared directories on the agent server. For example, if you configure the shared directories on the agent server as `C:\Foo\Test`, you must enter `C:\Foo\Test` as the file path in **Path** when you create a collection in Windows File System. If you do not match the letter case in both file paths exactly, you receive an error message, and your collection does not generate.
{: important}

The remote agent server and the file servers to be crawled must belong to the same Windows domain. A crawler can gather access control list (ACL) data from a single Windows domain.
{: important}


### Local File System
{: #localfilesystemconnect}

Use this option to crawl local file systems. Only documents supported by {{site.data.keyword.discoveryshort}} are crawled; all others are ignored.
{: shortdesc}

#### Creating and mounting a persistent volume claim on the crawler pod
{: #mount-persistent-volume}

Before you can configure a Local File System collection on {{site.data.keyword.discoveryshort}} version 2.2.0 and later, you must first create a persistent volume claim and mount it on the crawler pod. After you mount the persistent volume claim on the crawler pod, {{site.data.keyword.discoveryshort}} crawls your files, and you can edit these files later so that, after the next crawl, your edits are automatically reflected in the index.
{: shortdesc}

In {{site.data.keyword.discoveryshort}} version 2.2.0 and later, you can configure the persistent volume claim _after_ you install {{site.data.keyword.discoveryshort}}. In versions 2.2.0 and later, you can choose one of the following three ways to create the persistent volume claim and mount it on the crawler pod:

- [Using the external NFS server](#use-external-nfs)
- [Using dynamic provisioning with an NFS storage class](#dyn-prov-nfs)
- [Using dynamic provisioning with a Portworx storage class](#dyn-prov-portworx)

If you are using {{site.data.keyword.discoveryshort}} version 2.1.4 and earlier, you can make the files that you want to crawl accessible to the crawler pod by choosing from two ways, [Mounting a persistent volume on the crawler pod on versions 2.1.4 and earlier](#mount-pv-orig) or by [Copying local file system files to the crawler pod](#copy-local-folders).

##### Using the external NFS server
{: #use-external-nfs}

If the local file system files or folders that you want to crawl are stored in an external Network File System (NFS), you can use the external NFS server to create the persistent volume claim. After you create the persistent volume claim on the NFS server and mount it on the crawler pod, the [Local File System](#configurelocalfilesystem) crawler can directly crawl these files or folders from the server.
{: shortdesc}

1. Create a file called `crawler-pv-nfs.yaml`, and save the following configuration, replacing the `<>` and the content inside with the name of your persistent volume, for example `jdoe-nfs-pv`, and with the other required information:

   ```bash
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: <persistent-volume-name>
     labels:
       pv-name: <persistent-volume-name>
   spec:
     capacity:
       storage: 10Gi
     accessModes:
       - ReadWriteMany
     persistentVolumeReclaimPolicy: Retain
     nfs:
       server: <NFS server hostname or IP address>
       path: <Path of NFS exported folder>
   ```
   {: codeblock}

1. Enter the following command to create a persistent volume by using the `crawler-pv-nfs.yaml` file that you created:

   ```bash
   oc create -f crawler-pv-nfs.yaml
   ```
   {: pre}

   You might see output similar to the following:

   ```bash
   persistentvolume/jdoe-nfs-pv created
   ```
   {: codeblock}

1. Create a file called `crawler-pvc-nfs.yaml`, and save the following configuration, replacing the `<>` and the content inside with the name of your persistent volume claim, for example `jdoe-nfs-pvc`, and with the name of your persistent volume, for example `jdoe-nfs-pv`:

   ```bash
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: <persistent-volume-claim-name>
   spec:
     accessModes:
       - ReadWriteMany
     resources:
       requests:
         storage: 10Gi
     selector:
       matchLabels:
         pv-name: <persistent-volume-name>
   ```
   {: codeblock}

1. Enter the following command to create a persistent volume claim by using the `crawler-pvs-nfs.yaml` file that you created:

   ```bash
   oc create -f crawler-pvc-nfs.yaml
   ```
   {: pre}

   You might see output similar to the following:

   ```bash
   persistentvolumeclaim/jdoe-nfs-pvc created
   ```
   {: codeblock}

1. Enter the following command to mount the persistent volume claim to the crawler pod. This command also mounts the persistent volume claim to all ingestion-api pods. Replace the `<>` and the content inside with the name of your persistent volume claim, for example `jdoe-nfs-pvc`:

   ```bash
   oc patch wd wd --type=merge --patch='{"spec": {"ingestion": {"crawler": {"mount": {"enabled": true, "persistentVolumeClaimName": "<persistent-volume-claim-name>" } } } } }'
   ```
   {: pre}

For information about the other ways to create a persistent volume claim, see [Using dynamic provisioning with an NFS storage class](#dyn-prov-nfs) or [Using dynamic provisioning with a Portworx storage class](#dyn-prov-portworx). If you are using a version of {{site.data.keyword.discoveryshort}} 2.1.4 and earlier and you want to create and mount a persistent volume to the crawler pod and copy your local files to that pod, see [Creating and mounting a persistent volume claim on the crawler pod](#mount-persistent-volume).

##### Using dynamic provisioning with an NFS storage class
{: #dyn-prov-nfs}

If you want to crawl your local file system files or folders but you do not want to prepare an additional NFS server to store those files or folders, you can configure dynamic storage by using an NFS storage class. For information about storage providers that {{site.data.keyword.discoveryshort}} supports and for storage comparisons, see [Storage considerations](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/plan/storage_considerations.html){: external}. Before you complete this task, be sure to copy the files that you want to crawl to the {{site.data.keyword.discoveryshort}} cluster that you are working on. Also, if you have multiple {{site.data.keyword.discoveryshort}} clusters, you must copy the `crawler-pvc-dynamic.yaml` file that you will create in this task and the files that you want to crawl to each cluster.
{: shortdesc}

Complete the following steps to create and mount a persistent volume claim to the crawler pod by using an NFS storage class and to copy the files that you want to crawl to the persistent volume claim:

1. Enter the following command to check the `storageclass` name of the NFS provisioner:

   ```bash
   oc get storageclass
   ```
   {: pre}

   You might output similar to the following:

   ```bash
   NAME         PROVISIONER                                      RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
   nfs-client   cluster.local/innocence-nfs-client-provisioner   Delete          Immediate           true                   177m
   ```
   {: codeblock}

1. Create a file called `crawler-pvc-dynamic.yaml`, and save the following configuration, replacing the `<>` and the content inside with the name of your dynamic NFS persistent volume claim, for example `jdoe-dynamic-pvc`:

   ```bash
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: <name-of-dynamic-pvc>
   spec:
     accessModes:
       - ReadWriteMany
     resources:
       requests:
         storage: 10Gi
     storageClassName: nfs-client
   ```
   {: codeblock}

1. Enter the following command to create a persistent volume claim by using the `crawler-pvc-dynamic.yaml` file that you created:

   ```bash
   oc create -f crawler-pvc-dynamic.yaml
   ```
   {: pre}

   You might see output similar to the following:

   ```bash
   persistentvolumeclaim/jdoe-dynamic-pvc created
   ```
   {: codeblock}

1. Enter the following command to mount the persistent volume claim to the crawler pod. This command also mounts the persistent volume claim to all ingestion-api pods. Replace the `<>` and the content inside with the name of your dynamic NFS persistent volume claim in the previous step, for example `jdoe-dynamic-pvc`:
   ```bash
   oc patch wd wd --type=merge --patch='{"spec": {"ingestion": {"crawler": {"mount": {"enabled": true, "persistentVolumeClaimName": "<name-of-dynamic-pvc>" } } } } }'
   ```
   {: pre}

1. Enter the following command to copy the files that you want to crawl to your dynamic NFS persistent volume claim. You only need to run this command once against one of the existing crawler pods. The persistent volume claim is shared among all crawler and ingestion-api pods. Replace the `<>` and the content inside with the required information:

   ```bash
   oc rsync <path to local file system folder> <crawler pod>:/mnt
   ```
   {: pre}

Now that you mounted the persistent volume claim and copied all of the files that you want to crawl to it, you can [Configure your Local File System collection](#configurelocalfilesystem). For information about the other ways to create a persistent volume claim, see [Using the external NFS server](#use-external-nfs) or [Using dynamic provisioning with a Portworx storage class](#dyn-prov-portworx). If you are using a version of {{site.data.keyword.discoveryshort}} 2.1.4 and earlier and you want to create and mount a persistent volume to the crawler pod and copy your local files to that pod, see [Creating and mounting a persistent volume claim on the crawler pod](#mount-persistent-volume).

##### Using dynamic provisioning with a Portworx storage class
{: #dyn-prov-portworx}

If you want to crawl your local file system files or folders but you do not want to prepare an additional NFS server to store those files or folders, you can configure dynamic storage by using a Portworx storage class. For information about Portworx storage classes that {{site.data.keyword.discoveryshort}} supports, storage requirements, and how to automatically or manually create Portworx storage classes, see [Creating Portworx storage classes](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/install/portworx-storage-classes.html){: external}. Before you complete this task, be sure to copy the files that you want to crawl to the {{site.data.keyword.discoveryshort}} cluster that you are working on. Also, if you have multiple {{site.data.keyword.discoveryshort}} clusters, you must copy the `crawler-pvc-portworx.yaml` file that you will create in this task and the files that you want to crawl to each cluster.
{: shortdesc}

Complete the following steps to create and mount a persistent volume claim to the crawler pod by using a Portworx storage class and to copy the files that you want to crawl to the persistent volume claim:

1. Enter the following command to check the `storageclass` name of the Portworx provisioner:

   ```bash
   oc get storageclass | grep portworx-gp3-sc
   ```
   {: pre}

   You might see output similar to the following:

   ```bash
   NAME                             PROVISIONER                     RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
   portworx-gp3-sc                  kubernetes.io/portworx-volume   Retain          Immediate           true                   51d
   ```
   {: codeblock}

1. Create a file called `crawler-pvc-portworx.yaml`, and save the following configuration, replacing the `<>` and the content inside with the name of your dynamic Portworx persistent volume claim, for example `jdoe-pvc-portworx`:

   ```bash
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: <name-of-portworx-pvc>
   spec:
     accessModes:
       - ReadWriteMany
     resources:
       requests:
         storage: 10Gi
     storageClassName: portworx-gp3-sc
    ```
   {: codeblock}

1. Enter the following command to create the persistent volume claim by using the `crawler-pvc-portworx.yaml` file that you created:

   ```bash
   oc create -f crawler-pvc-portworx.yaml
   ```
   {: pre}

   You might see output similar to the following:

   ```bash
   persistentvolumeclaim/jdoe-pvc-portworx created
   ```
   {: codeblock}

1. Enter the following command to mount the persistent volume claim to the crawler pod. Replace the `<>` and the content inside with the name of your dynamic Portworx persistent volume claim, for example `jdoe-pvc-portworx`:

   ```bash
   oc patch wd wd --type=merge --patch='{"spec": {"ingestion": {"crawler": {"mount": {"enabled": true, "persistentVolumeClaimName": "<name-of-portworx-pvc>" } } } } }'
   ```
   {: pre}

1. Enter the following command to copy the files that you want to crawl to your dynamic Portworx persistent volume claim. You only need to run this command once against one of the existing crawler pods. The persistent volume claim is shared among all crawler and ingestion-api pods. Replace the `<>` and the content inside with the required information:

   ```bash
   oc rsync <path to local file system folder> <crawler pod>:/mnt
   ```
   {: pre}

Now that you mounted the persistent volume claim and copied all of the files that you want to crawl to it, you can [Configure your Local File System collection](#configurelocalfilesystem). For information about the other ways to create a persistent volume claim, see [Using the external NFS server](#use-external-nfs) or [Using dynamic provisioning with an NFS storage class](#dyn-prov-nfs). If you are using a version of {{site.data.keyword.discoveryshort}} 2.1.4 and earlier and you want to create and mount a persistent volume to the crawler pod and copy your local files to that pod, see [Creating and mounting a persistent volume claim on the crawler pod](#mount-persistent-volume).

#### Mounting a persistent volume on the crawler pod on versions 2.1.4 and earlier
{: #mount-pv-orig}

If you do not want to copy your [Local File System](#configurelocalfilesystem) files or folders to the crawler pod, you can establish a link from your cluster to a remote Network File System (NFS), which you can configure to serve as a persistent volume and mount on the crawler pod. After establishing this link and after {{site.data.keyword.discoveryshort}} crawls your files, you can edit these files later so that, after the next crawl, your edits are automatically reflected in the index.
{: shortdesc}

If you plan to install {{site.data.keyword.discoveryshort}} version 2.1.4 and earlier, you must create and configure the persistent volume _before_ you install {{site.data.keyword.discoveryshort}}.
{: important}

Complete the following steps to create and mount a persistent volume on the crawler pod on your {{site.data.keyword.discoveryshort}} instance version 2.1.4 and earlier:

1. Create a file called `crawler-pv.yaml`. The content of the file looks like the following. Replace the `<>` and the content inside with the required information:

   ```bash
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: "<label-name>"
     labels:
       "<label-name>": "<label-value>"
   spec:
     capacity:
       storage: "10Gi"
     accessModes:
       - ReadWriteMany
     persistentVolumeReclaimPolicy: Retain
     nfs:
       server: <NFS server hostname or IP address>
       path: <Path of NFS exported folder>
   ```
   {: codeblock}

1. Enter the following command to set `crawler-pv.yaml` as the persistent volume:

   ```
   create -f crawler-pv.yaml
   ```
   {: pre}

1. If you are using version 2.1.3 or 2.1.4, mount the persistent volume to the crawler pod by editing `override.yaml` to include the following input. This file overrides any default settings that you choose. In the `label` and `value` fields, you must use the same string that you specified when you created the `crawler-pv.yaml` file in step 1. Replace the `<>` and the content inside with the required information:

   ```bash
   core:
     ingestion:
       mount:
         useDynamicProvisioning: false
         storageClassName: ""
         accessModes: "ReadWriteMany"
         selector:
           label: "<label-name>"
           value: "<label-value>"
   ```
   {: codeblock}

   If you are using a version earlier than 2.1.3, mount the persistent volume to the crawler pod by creating a file called `override.yaml` in `ibm-watson-discovery-ppa/deploy/`. You might see the following content in `override.yaml`:

   ```bash
   core:
     ingestion:
       mount:
         useDynamicProvisioning: false
         storageClassName: ""
         selector:
           label: "<label-name>"
           value: "<label-value>"
   ```
   {: codeblock}

1. Install {{site.data.keyword.discoveryshort}} along with `override.yaml`. For information about installing {{site.data.keyword.discoveryshort}}, see [Installing the Watson Discovery service](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_3.0.1/cpd/svc/watson/discovery-install.html){: external}. For information about overriding values in `override.yaml` when you install {{site.data.keyword.discoveryshort}}, see [Override values for Watson Discovery installation](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_3.0.1/cpd/svc/watson/discovery-override.html){: external}.

   If you are using a version earlier than 2.1.3, from the `deploy` subdirectory, run the `deploy.sh` script by entering the `-d` flag, the file path to the files that you want to make accessible to `ibm-watson-discovery`, the `-O` flag, and your `override.yaml` file. You can also enter the `-e` flag with your `release-name-prefix`. If you do, your `release-name-prefix` must be 13 characters or fewer, or the installation will fail. If you do not enter the `-e` flag, the default `release-name-prefix` is `disco`. See the following example. Replace the `<>` and the content inside with the required information:

   ```bash
   ./deploy.sh -d </local root directory/subdirectory/>ibm-watson-discovery -O ./override.yaml -e <release-name-prefix>
   ```
   {: codeblock}

   For a list of flags and their descriptions or for help, run `./deploy.sh -h`.
   {: tip}

For information about copying your local files that you want to crawl to the crawler pod, see [Copying local file system files to the crawler pod on versions 2.1.4 and earlier](#copy-local-folders). For information about the different ways of creating and mounting a persistent volume in all {{site.data.keyword.discoveryshort}} versions, see [Creating and mounting a persistent volume claim on the crawler pod](#mount-persistent-volume).

#### Copying local file system files to the crawler pod on versions 2.1.4 and earlier
{: #copy-local-folders}

You can also copy your local files that you want to crawl to the crawler pod. Before you create a [Local File System collection](#configurelocalfilesystem), you must have the OpenShift CLI, or `oc`, installed. For more information about installing the OpenShift Origin CLI, see [Installing the OpenShift Origin CLI (`oc`)](/docs/openshift?topic=openshift-openshift-cli#cli_oc).
{: shortdesc}

Complete the following steps to copy your local file system files to the crawler pod on an instance of {{site.data.keyword.discoveryshort}} versions 2.1.4 and earlier, replacing the `<>` and the content inside with the required information:

1. Enter the following command to log on to your {{site.data.keyword.discoveryshort}} cluster:

   ```bash
   oc login https://<OpenShift administrative console URL> -u <cluster-administrator> -p <password>
   ```
   {: pre}

1. Enter the following command to switch to the proper namespace:
   ```bash
   oc project <discovery-install namespace>
   ```
   {: pre}

1. Enter `oc get pods|grep crawler` to find the crawler pod. If you are using a version earlier than 2.1.3, enter `oc get pods|grep ingestion` to find the ingestion pod.
1. Enter the following command to copy the local file system folders that you want to crawl to the `/mnt` directory on the crawler pod:

   ```bash
   oc rsync <path to local file system folder> <crawler pod>:/mnt
   ```
   {: pre}

   If you are using a version of {{site.data.keyword.discoveryshort}} that is older than 2.1.3, enter the following command:

   ```
   oc rsync <path to local file system folder> <ingestion pod>:/mnt
   ```
   {: pre}

   In versions earlier than 2.1.3, the files that you copy apply to all of the gateway and ingestion pods. The default number of ingestion pods is 1.

   If you edit files that you copied to the ingestion or gateway pod, your changes are not reflected in the index after a recrawl, unless you recopy the edited files to the gateway or ingestion pod.
   {: important}

For information about creating and mounting a persistent volume on the crawler pod on an instance of {{site.data.keyword.discoveryshort}} versions 2.1.4 and earlier, see [Mounting a persistent volume on the crawler pod on versions 2.1.4 and earlier](#mount-pv-orig). For information about the different ways of creating and mounting a persistent volume in all {{site.data.keyword.discoveryshort}} versions, see [Creating and mounting a persistent volume claim on the crawler pod](#mount-persistent-volume).

#### Configuring a Local File System collection
{: #configurelocalfilesystem}

In {{site.data.keyword.discoveryshort}}, after you select **Local File System** as the collection type, enter the following information:

1. Under **Specify what you want to crawl**, complete the following field:
    - **Path** - The file path that you need to enter to crawl folders and documents from. You can enter multiple file paths.
1. After you enter one or more paths, click **Add** and then **Finish**


### FileNet P8
{: #filenet-connect}

You can use this option to crawl FileNet P8 version 5.5.0. The FileNetP8 connector can also access the Content Engine Web Services (CEWS) of a FileNet server that is installed on {{site.data.keyword.cp4-automation_notm}}. FileNet P8 5.5.0 and FileNet on {{site.data.keyword.cp4-automation_short}} support the HTTP and HTTPS protocols. Only documents supported by {{site.data.keyword.discoveryshort}} are crawled; all others are ignored.
{: shortdesc}

If you are using FileNet P8 5.5.0 or FileNet on {{site.data.keyword.cp4-automation_short}}, the connector only supports the HTTPS protocol when a verified SSL server certificate is installed on the FileNet server.
{: note}

{{site.data.keyword.discoveryshort}} does not support role-based security when you crawl FileNet P8.
{: important}


#### Configuring a FileNet P8 collection
{: #configure-filenet}

In {{site.data.keyword.discoveryshort}}, after you select **FileNet P8** as the collection type, enter the following information, replacing the `<>` and the content inside with the requested information:

1. Complete the following fields in **Enter your credentials**:
    - **Content Engine Web Service URL** - The Content Engine web service URL of the IBM FileNet P8 server. When you enter the URL, use the following format: `<protocol>://<server>:<port>/wsi/FNCEWS40MTOM`. You can use the HTTP or HTTPS protocol. The `<server>` is the host name of the server where the Content Platform Engine is deployed, and the `<port>` is the HTTP port that the application server uses, or where the Content Platform Engine is deployed.
    - **User** - The username of the user who wants to crawl a FileNet P8 server. You can obtain your username from your FileNet administrator.
    - **Password** - The password of the user who wants to crawl a FileNet P8 server. You can obtain your password from your FileNet administrator.
1. Complete the following field in **Specify what you want to crawl**:
    - **ObjectStore Name** - The name of the object store that you can use to create, search, retrieve, and store documents.
1. In **Crawler Space Type**, select either **Folder** or **Class**.
1. Complete the following field:
    - **Folder subpath or Subclass name** - The subfolder path that you can specify under RootFolder that crawls all documents belonging to the specified folder or the custom subclass of the `Document` class that crawls all documents belonging to the specified class. Before you specify anything in this field, keep in mind the following items:
      - You can specify multiple crawler spaces by using both the `Class` and `Folder` types and crawl the documents belonging to the folder name and class name.
      - You cannot specify a class outside the object store that you defined.
      - No support is available for specifying a class that is a subclass of a `Custom Object` and `Folder`.
1. After you enter one or more paths, click **Add**.
1. Optional: Set the following switch in **Security**:
    -  **Enable Document Level Security** - By default, this switch is set to **Off**. You must enable this option to activate document level security. When you enable this option, your users can crawl and query content that they have access to. For more information about Document Level Security, see [About document level security](#configuredls).
1. Click **Finish**.


### Notes
{: #connectnotes}

Use this option to crawl an HCL Notes (formerly Lotus Notes) database version 9.0.1. Only documents that {{site.data.keyword.discoveryshort}} supports are crawled; all others are ignored.
{: shortdesc}

The Notes data source only supports the Domino Internet Inter-ORB Protocol (DIIOP) protocol. To crawl documents, including ACLs, you must have server, database, and document access on the Domino server, but at minimum, you must have `Reader` access. For group extractions for the internal Domino LDAP, you must have `Reader` access of the `names.nsf` directory database, and for group extractions for the external LDAP, you must have the credential for the LDAP server. You can define Notes users both in the internal Domino directory and in the external LDAP. However, {{site.data.keyword.discoveryshort}} only supports users in the internal Domino directory as crawl users; it does not support users in the external LDAP as crawl users.

#### Configuring DIIOP servers
{: #config-servers}

To crawl servers that use the DIIOP protocol, you must configure the server so that the Notes Domino crawler can use the protocol. The server that you want to crawl must be running the DIIOP and HTTP tasks.
{: shortdesc}

To configure a server that has the DIIOP protocol, complete the following steps:

1. Configure the server document:
   1. Open the `server` document on the Notes server that you want to crawl. This document is stored in the Domino directory.
   1. On the Configuration page, expand the **server** section.
   1. On the Security page in the Programmability Restrictions section, specify the appropriate security restrictions for your environment in the following three fields: **Run restricted Lotus Script/Java agents**, **Run restricted Java/Javascript/COM**, **Run unrestricted Java/Javascript/COM**

      For example, you might specify an asterisk (`*`) to allow unrestricted access by Lotus Script/Java agents and specify usernames that are registered in the Domino directory for the Java/Javascript/COM restrictions.

      To crawl a server that uses the DIIOP protocol, your configured crawler must be able to access the usernames that you specify in these fields.
      {: important}

   1. Open the Internet Protocol page, then the HTTP page, and set the **Allow HTTP clients to browse database** option to **Yes**.
1. Configure the user document:
   1. Open the `user` document on the server that you want to crawl. This document is stored in the Domino directory.
   1. On the Basics page in the **Internet password** field, specify a password. When you use the administration console to configure options for crawling a server, specify this user ID and password on the page where you identify the server to crawl. When you enter these credentials, the crawler can then access the server.
1. Restart the DIIOP task on the server.

#### Configuring a Notes collection
{: #configurenotes}

In {{site.data.keyword.discoveryshort}}, after you select **Notes** as the collection type, enter the following information:

1. Complete the following fields in **Enter your credentials**:
    -  **Host name** - The host name of the Notes server.
    -  **User name** - The username to crawl the Notes server.
    -  **Password** - The password of the specified user.
1. In **Crawl type**, click one of the following options:
    -  **Database** - Crawls a specified Notes database.
    -  **Directory** - The directory that you want to crawl.
1. Complete the applicable field:
    -  **Database file name** (when you click **Database** as the crawl type) - The file name of the database that you want to crawl.
    -  **Directory name** (when you click **Directory** as the crawl type) - The directory name that you want to crawl. If you select this option, {{site.data.keyword.discoveryshort}} crawls all Notes databases under the specified directory.
1. Optional: In **Security**, set the following switch:
    - **Enable Document Level Security** - By default, this switch is set to **Off**. You must enable this option to activate document level security. When set to **On**, your users can crawl content that they have access to in a Notes database or directory. When you enable this option, you need to obtain the following information from the LDAP administrator. For more information, see [About document level security](#configuredls).
    - **Use remote LDAP directory** - By default, is set to **Off**. This option is only available when you set **Enable Document Level Security** to **On**.
        - **LDAP server URL** - The LDAP server URL to connect to, for example `ldap://<ldap_server>:<port>`.
        - **LDAP binding username** - The username used to bind to the directory service.
        - **LDAP binding user password** - The password used to bind to the directory service.
        - **LDAP base DN** - The starting point for searching user entries in LDAP, for example `CN=Users,DC=example,DC=com`.
        - **LDAP user filter** - The user filter to search user entries in LDAP. If unspecified, the default value is `(userPrincipalName=\{0\})`.
        - **LDAP group filter** - The group filter to search group entries in LDAP.

        When you enable document level security, you can only crawl one LDAP server, which can either be a Domino server or an external server.
        {: note}

1. Optional: In **Advanced options**, set the following switches:
    - **Crawl attachments** - By default, is set to **On**. When set to **On**, crawls attachments of Notes documents.
    - **Automatic code page detection** - By default, is set to **On**. When this option is disabled, the encoding converter detects the code pages of crawled documents. Complete the following fields:
        -  **Code page to use** - Displays only when **Automatic code page detection** is set to **Off**. The field used to enter the character encoding. If unspecified, the default value is `UTF-8`.
        -  **Notes formula** - Specify the limits to the data that you crawl, for example `SELECT @IsAvailable(Year) & Year > 2003`.
1. Select an option in the following drop-down list:
    -  **Document date field** - The document date that is used in a crawl.
         -  **Document modification date** - By default, the modified dates of the crawled documents is stored as the original field `_ _$Date$_ _`.
         -  **Document crawl date** - Assigns the crawled dates to the original field `_ _$Date$_ _`.
         -  **Document creation date** - Assigns the creation dates of the crawled documents to the original field `_ _$Date$_ _`.


### Reuse data from an existing collection
{: #reuse}

<!-- c/s help for the *Select collection to reuse* page. Do not delete. -->

Use this option to reuse data that is stored in an existing collection.
{: shortdesc}

You can share collections across projects. However, only the following subsets of the collection are shared:

- The processed data
- Configured connector

If you make any of the following changes to a shared collection, those changes apply to the shared collection in every project. These changes include the following:

- Changing the **Run OCR (Optical Character Recognition)** setting
- Annotating fields or adding fields, using Smart Document Understanding
- Enabling or disabling fields
- Changing the setting for document splitting
- Changing any of the connector settings

The enrichments and other improvement tools are not included when a collection is shared because they are set at the project level.
{: important}

For more information about projects, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects#projects).

## Crawler plug-in settings
{: #plugin-settings}

When you deploy one or more crawler plug-ins, you can configure your collection to use one of the plug-ins.

These settings are only available when crawler plug-ins are deployed. For more information about building a plug-in, see [Building a Cloud Pak for Data crawler plug-in](/docs/discovery-data?topic=discovery-data-crawler-plugin-build), and for more information about deploying a crawler plug-in, see [Commands and options for managing your crawler plug-ins](/docs/discovery-data?topic=discovery-data-manage-plugin#mng-plugin-cmd-opt).
{: note}

When you are ready to configure a collection to use a crawler plug-in, you can see a **Plug-in settings** section. Review the following plug-in settings that you can use to process documents. You only see these options if you deploy a plug-in package by using the `scripts/manage_crawler_plugin.sh` script:

-  **Enable plug-in** - By default, this switch is set to **Off**. Enable this option if you want to use a crawler plug-in to process documents.
    -  **Plug-in** - Lists available crawler plug-in names. Select a plug-in to use.

## Managing collections
{: #manage-collections}

<!-- c/s help for the *Manage collections* page. Do not delete. -->

 All of your collections are listed here. You can delete unused collections and view statistics.

 To keep track of collection sharing across projects, open the **Projects** page, then complete the appropriate step for your deployment:
 
  -  ![Cloud Pak for Data only](images/desktop.png) **IBM Cloud Pak for Data**: Select **Data usage**, then **Collection usage and sharing**.
  -  ![IBM Cloud only](images/ibm-cloud.png) **IBM Cloud**: Select **Data usage and GDPR**, then **Collection usage and sharing**.

 
For more information see [Collection usage and sharing](/docs/discovery-data?topic=discovery-data-projects#collection-usage).


## Collection activity
{: #collection-overview}

<!-- c/s help for the *Collection activity* page. Do not delete. -->

{{site.data.keyword.discoveryshort}} provides collection details in the **Activity** tab.
{: shortdesc}

Collection details include the following:

-  Number of documents
-  Collection status
    -  A collection is finished processing when the status is `Syncing complete` or `Processing finished. Updated documents are ready for you.`.
    -  ![Cloud Pak for Data only](images/cpdonly.png) If processing fails, click either the **Recrawl collection** or **Reprocess collection** button. The button that you see varies, depending on the type of collection.
    -  ![Cloud Pak for Data only](images/cpdonly.png) If the collection status is `Syncing ...`, and you click the **Recrawl collection** button, the current crawl stops, and a new full crawl begins. It is recommended that you wait until the status is `Syncing complete` before starting a recrawl.
-  Date of creation and last update
-  An abbreviated list of **Warnings and errors**. To see the full list, select **View all**. The **Warnings and errors** page (![Cloud Pak for Data only](images/cpdonly.png)) contains more detailed information, including the`Type`, `Message`, and `Date` for each message.


## About document level security
{: #configuredls}

If you have document level security activated, you can leverage the security settings from your source documents to control the search results returned to different users, and it is supported in the Box, SharePoint OnPrem, SharePoint Online, Windows File System, and FileNet P8 data sources.

To enable document level security, you must configure these components:

- Enable document level security for your collection.

  - For a description of the feature in the SharePoint OnPrem data source, see [Enable Document Level Security for SharePoint OnPrem](#configuresp_op).
  - For a description of the feature in SharePoint Online, see [Enable Document Level Security for SharePoint Online](#configuresp).
  - For a description of the feature in Windows File System and the information required to configure a collection, consult [Enable Document Level Security for Windows File System](#configurewindowsfilesystem).
  - For a description of the feature in FileNet P8, see [Enable Document Level Security for FileNet P8](#configure-filenet).
  - For a description of the feature in Notes, see [Enable Document Level Security for Notes](#configurenotes).

- Configure document level security parameters for your [SharePoint Online collection](#configuresp), [SharePoint OnPrem collection](#configuresp_op), [Windows File System collection](#configurewindowsfilesystem), [FileNet P8 collection](#configure-filenet), or [Notes collection](#configurenotes).
  Document level security configuration options are visible when document level security is enabled in your collection configuration.
- Create {{site.data.keyword.discoveryshort}} users that match the users available on the source system.
- Associate users with your {{site.data.keyword.discoveryshort}} instance.

{{site.data.keyword.discoveryshort}} only supports pre-filtering. Pre-filtering involves replicating the document's source ACL at crawl time into the index and relying on the search engine to compare user credentials to the replicated document ACLs. {{site.data.keyword.discoveryshort}} performs the best when documents are pre-filtered and when you control which documents you add to the index. However, it is difficult to model all of the security policies of the various back-end sources in the index and implement comparison logic uniformly. Also, pre-filtering is not as responsive to any changes that might occur in the source ACLs after the most recent crawl.
{: note}


### Creating users for document level security
{: #createusersdls}

You must create users that match the users available on the source system that {{site.data.keyword.discoveryshort}} is connecting to so that they can query with document level security enabled.
{: shortdesc}

1. Log in to {{site.data.keyword.discoveryshort}} as an administrator.
1. Create users who match the users available on your source or who are connected to the LDAP server that your source system uses. If you create users for document level security, keep the following points in mind:

   - Optional: For each user who you want to access query results, you must add users. The username must match the username that the source uses. This option is only for development and testing purposes. To create users individually, see [Managing users](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/cpd/admin/users.html){: external}.
   - To connect to an LDAP server that the source is using, see [Connecting to your LDAP server](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/cpd/admin/ldap.html){: external}.


### Associating users with an instance
{: #associateusersdls}

1. Click the main-menu icon in the upper-left corner, and click **My instances** > **Provisioned instances**.
1. Hover over the instance you want to add users to. When you hover over your chosen instance, an expandable menu icon appears on the right side of the instance.
1. Click the expandable menu icon, and select **Manage Access**.
1. Click **Add user**.
1. Add the users you want from the list by clicking **Add user**, select the desired user from the list, assign their role as **User**, and click **Add**.

When you query collections that have document level security enabled, no results are returned if the users associated with your {{site.data.keyword.discoveryshort}} instance are not present in the source system. For more information about querying these collections, see [Querying with document level security enabled](/docs/discovery-data?topic=discovery-data-query-concepts#querydls).
{: important}

Because {{site.data.keyword.discoveryshort}} does not sync any changes to the users from the LDAP server, {{site.data.keyword.discoveryshort}} administrators must ensure that the users list is current and remove any non-current users.
{: note}
