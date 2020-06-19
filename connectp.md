---

copyright:
  years: 2015, 2020
lastupdated: "2020-06-19"

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

<!-- 2.1.3 c/s help for the *Select a Collection type* page for IBM Cloud. Do not delete. -->
![IBM Cloud only](images/cloudonly.png) You can use {{site.data.keyword.discoveryfull}} on the {{site.data.keyword.cloud}} to connect to and crawl documents from remote sources. For information about Cloud Pak for Data data sources, see [Configuring Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types).
{: shortdesc}

You can connect to a data source and pull documents on a schedule into {{site.data.keyword.discoveryshort}} by configuring a collection to associate with that source. You can configure each collection with one data source. {{site.data.keyword.discoveryshort}} pulls documents from the data source using a process called crawling. Crawling is the process of systematically browsing and retrieving documents from the specified start location. {{site.data.keyword.discoveryshort}} only crawls items that you explicitly specify. The first time that a crawler crawls a data source is a full crawl, and every time that the crawler runs after the full crawl, per the crawl schedule, is a refresh, also called a recrawl.

## Data source requirements
{: #public-requirements}

The following requirements and limitations are specific to {{site.data.keyword.discoveryshort}} on {{site.data.keyword.cloud_notm}}:

-  The individual document file size limit for Salesforce, SharePoint Online, IBM Cloud Object Storage, and Web Crawl is 50MB.
-  If you crawl Salesforce, a list of available resources is presented when you configure a source, using the {{site.data.keyword.discoveryshort}} tooling.
-  If you are using the {{site.data.keyword.discoveryshort}} tooling, you can configure a collection with a single data source. If you are using the API, you can ingest documents from multiple data sources into a single collection.
-  Crawling a data source uses resources, namely API calls, of the data source. The number of API calls depends on the number of documents that need to be crawled. You must obtain an appropriate level of service license, for example Enterprise, for the data source. For information about the appropriate service level license that you need, contact the source system administrator.
-  {{site.data.keyword.discoveryshort}} source crawls do not delete documents that are stored in a collection, but you can manually delete them using the API. When a source is re-crawled, new documents are added, updated documents are modified to the current version, and deleted documents remain as the version last stored.

View the following table to see the objects that a data source can crawl and which data sources support crawling new and modified documents during a refresh:

Data source                          | Crawls new and modified documents during refresh? | Compatible objects that can be crawled
------------------------------------ | ------------------------------------------------- | --------------------------------------
Salesforce                           | Yes                                               | Any default and custom objects that you have access to, accounts, contacts, cases, contracts, knowledge articles, attachments
Microsoft SharePoint Online          | Yes                                               | SiteCollections, websites, lists, list items, document libraries
Web Crawl                            | No                                                | Websites, website subdirectories
IBM Cloud Object Storage             | Yes                                               | Buckets, files
{: caption="Table 1. Data sources that support crawling new and modified documents during refresh and objects that can be crawled" caption-side="top"}


## Available data sources
{: #available sources}

You can use {{site.data.keyword.discoveryshort}} to crawl from the following data sources:

-  [Salesforce](/docs/discovery-data?topic=discovery-data-sources#connectsfpublic)
-  [Microsoft SharePoint Online](/docs/discovery-data?topic=discovery-data-sources#connectsppublic)
-  [Web Crawl](/docs/discovery-data?topic=discovery-data-sources#connectwebcrawlpublic)
-  [IBM Cloud Object Storage](/docs/discovery-data?topic=discovery-data-sources#connectcos)

You can connect to a data source using the {{site.data.keyword.discoveryshort}} tooling or the API. The {{site.data.keyword.discoveryshort}} tooling provides a simplified method of connection that requires less understanding of the source systems, and the API provides a more granular and highly configurable interface, which requires a greater understanding of the source that you are connecting to. Consult the following process overview to see which sections of this document to read next:

1.  Read the [Data source requirements](/docs/discovery-data?topic=discovery-data-sources#public-requirements).
2.  Read the requirements for your data source. For the available data sources, see the list above.
3.  Read the instructions to connect to {{site.data.keyword.discoveryshort}} by using one of the following methods:
    -  [Using the tooling](/docs/discovery-data?topic=discovery-data-sources#source_tooling)
    -  [Using the API](/docs/discovery-data?topic=discovery-data-sources#source_api)

You can use an IBM App Connect default connector to send data from a large set of popular data sources to {{site.data.keyword.discoveryshort}} by creating flows within the App Connect tooling. Note that creating a separate App Connect instance is required to use this App Connect default connector and that any costs that you incur when you use a paid App Connect instance are not included with the cost for using {{site.data.keyword.discoveryshort}}. Additionally, except for indexing, {{site.data.keyword.discoveryshort}} does not support any integration with App Connect that you perform on your own. For information about integrating App Connect with {{site.data.keyword.discoveryshort}} or for integration support or questions, see [Using IBM App Connect with {{site.data.keyword.discoveryfull}}](https://developer.ibm.com/integration/docs/app-connect/how-to-guides-for-apps/use-ibm-app-connect-watson-discovery/){: external}. For the available data sources that you can use with the App Connect default connector to send data to {{site.data.keyword.discoveryshort}}, see [Connectors A-Z](https://www.ibm.com/cloud/app-connect/connectors/){: external}.


### Salesforce
{: #connectsfpublic}

When connecting to a Salesforce source, ensure that the instance you plan to connect to is an Enterprise plan or higher.

The following credentials are required to connect to a Salesforce source. If you do not know these credentials, consult your Salesforce administrator:
-  `url` - The `url` of the source that these credentials connect to.
-  `username` - The `username` of the source that these credentials connect to.
-  `password` - The `password` consists of the Salesforce password and a valid Salesforce security token concatenated. This value is never returned and is only used when creating or modifying credentials.

When identifying the credentials, it might be useful to consult the [Salesforce developer documentation](https://developer.salesforce.com/docs/){: external}.

Other items to note when you crawl Salesforce:

-  Knowledge Articles are only crawled if their **version** is `published` and their languages is `en-us`.
-  When you use the API, you must have a list of Salesforce objects that you want to crawl. Use the {{site.data.keyword.discoveryshort}} tooling to browse and select which content to crawl.


### SharePoint Online
{: #connectsppublic}


When connecting to a Microsoft SharePoint Online source, ensure that the instance that you plan to connect to is an Enterprise (E1) plan or higher.

Except for `site_collection_path`, the following fields are required to connect to a SharePoint Online source. If you do not know what to enter in these fields, contact your SharePoint administrator, or consult the [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}:

-  `username` - The `username` to connect to the SharePoint Online SiteCollection that you want to crawl. This user must have access to all sites and lists that the user wants to crawl and index. Your `username` input must be a default Azure Active Directory (Azure AD) account, which is formatted as follows: `<username>@<domain>.onmicrosoft.com`. If you do not have an Azure AD username, contact your SharePoint site administrator.
-  `password` - The `password` to connect to the SharePoint Online SiteCollection that you want to crawl. This value is never returned and is only used when creating or modifying credentials.
-  `organization_url` - The `organization_url` of the source that you want to crawl. When you enter this input, only enter the domain name of the URL, for example `https://<company>.<domain>.com/`. If you enter a URL that extends beyond the domain name, or `.com/`, the input is invalid.
-  `site_collection_path` Optional: - The `site_collection_path` to the source that you want to crawl. For guidance on how to format this input, see the following example: `/sites/test`. If unspecified, the default is `/`, and the root site collection is crawled.

Note the following items when you crawl Microsoft SharePoint Online:

-  To crawl SharePoint, the `username` account does not need `SiteCollection Administrator` permissions.
-  When you crawl SharePoint, you must have the list of SharePoint site collection paths that you want to crawl. {{site.data.keyword.discoveryshort}} does not support folder paths as input.
-  You might want to use the default Azure AD authentication.

To successfully crawl Microsoft SharePoint Online, you must enable legacy authentication and Contribute level permissions. To enable legacy authentication, visit the [Azure portal](https://portal.azure.com/){: external}, or contact your SharePoint administrator. For assistance with enabling Contribute level permissions, you can also contact your SharePoint administrator.
{: important}

If you created a SharePoint Online account after January 2020, two-factor authentication is enabled for your account, by default. To crawl your SharePoint Online collection, you must disable two-factor authentication. To view and change your multifactor authentication status, see [View the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#view-the-status-for-a-user){: external} or [Change the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#change-the-status-for-a-user){: external}.
{: important}


### Web Crawl
{: #connectwebcrawlpublic}


You can use the web crawler to crawl public websites that don’t require a password. You can select how often you'd like {{site.data.keyword.discoveryshort}} to sync with the websites, the language, and the number of hops.

-  `Sync my data` - You can choose to sync hourly, daily, weekly, or monthly.
-  `Select language` - Choose the language of the websites from the list of supported languages. For the list of languages that {{site.data.keyword.discoveryshort}} supports, see [Language support](/docs/discovery-data?topic=discovery-data-language-support). You should create a separate collection for each language.
-  `URL group to sync` - Enter your URL and click the **Add** button to add it to the URL group. To specify the **Crawl settings** for this URL group, click the ![Cog](images/icon_settings.png) icon. You can set the **Maximum hops**, which is the number of consecutive links to follow from the starting URL (the starting URL is `0`). The default number of hops is `2` and the maximum is `20`. If you are using the API, the maximum is `1000`. You can specify URL paths to exclude from the crawl in the **Exclude URLs where the path includes** field. Separate the paths, using commas, for example, if you specified the URL `http://domain.com`, you could exclude `http://domain.com/licenses` and `http://domain.com/pricing` by entering `/licenses/, /pricing/`.

When you specify a URL to crawl, the final `/` determines the subtree to crawl. For example, if you enter the URL `https://www.example.com/banking/faqs.html`, all URLs that begin with `https://www.example.com/banking/` are crawled, and the input of `https://www.example.com/banking` crawls all URLs that begin with `https://www.example.com/`. If you would like to restrict the crawl to a specific URL, such as `https://www.example.com/banking/faqs.html`, enter that URL in the `URL group to sync` field, and then set the **Maximum hops** to `0`.

The web crawler does not crawl dynamic websites that use JavaScript to render content. You can confirm the use of JavaScript by viewing the source code of the website in your browser.

The number of web pages crawled is limited to 250,000, so the web crawler might not crawl all the specified websites and might reach the maximum number of hops.
{: note}

If you require different **Crawl settings** for other URLs, click **Add URL group** and create a new group. You can create as many URL groups as you need.
{: tip}


### IBM Cloud Object Storage
{: #connectcos}


When you connect to an {{site.data.keyword.blockstoragefull}} source, the following credentials are required. You can obtain them from your {{site.data.keyword.blockstoragefull}} administrator:

-  `endpoint` - The `endpoint` name used to interact with {{site.data.keyword.blockstoragefull}} data.
   Do not enter `http://` or `https://`, as part of the {{site.data.keyword.blockstoragefull}} `endpoint` credential. Otherwise, you might receive an error message indicating that you have invalid or expired credentials. For the proper formatting of endpoints, see the column named Endpoint in the table in [Regional Endpoints](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints#endpoints-region).
-  `access_key_id` - `access_key_id` obtained when the {{site.data.keyword.blockstoragefull}} instance was created.
-  `secret_access_key` - `secret_access_key` to sign requests obtained when the {{site.data.keyword.blockstoragefull}} instance was created.

IAM authentication is not currently supported for this connector. You need to set up HMAC authentication before you configure this connector. See [Service Credentials](/docs/cloud-object-storage/iam?topic=cloud-object-storage-service-credentials) for instructions.
{: important}

After this information is entered, you can choose how often you want to sync your data and select the buckets you want to sync to.

Other items to note when you crawl {{site.data.keyword.blockstoragefull}}:

-  This connector does not support crawling private endpoints.
-  For more information about IBM Cloud Object Storage endpoints, see [Endpoints and storage locations](/docs/cloud-object-storage/basics?topic=cloud-object-storage-endpoints).
-  There is a slight performance issue if all buckets are selected. In this case, a delay is possible, before the documents complete indexing.

## Creating a collection using the tooling
{: #source_tooling}

Connecting to a data source using the {{site.data.keyword.discoveryshort}} tooling is performed by creating a collection specifically for a source. Perform the following steps to create a source collection and crawl it:

1.  From the **Manage data** page of the {{site.data.keyword.discoveryshort}} tooling, select **Connect a data source**.
2.  Select the data source that you want to connect to.
3.  Enter your source credentials, and click **Connect**. You must obtain your source credentials from your source system administrator.
4.  Choose which data that you want to crawl and how often you want to sync it:
    -  **once an hour**: runs every hour
    -  **once a day**: runs every day between the hours of 00:00 and 06:00 in the specified time zone
    -  **once a week**: runs every week on Sunday between hours of 00:00 and 06:00 in the specified time zone
    -  **once a month**: runs every month on the first Sunday of the month between the hours of 00:00 and 06:00 in the specified time zone
    
    Example crawl status:
    
    ```json
    "crawl_status" : {
    "source_crawl" : {
      "status" : "completed",
      "next_crawl" : "2019-02-10T05:00:00-05:00"
    }
    ```
5.  Click **Save & Sync objects** to start crawling your data source. You are then redirected to the collection status page, which updates as documents are added to the collection.

After the initial sync, all subsequent crawls run on the frequency that you specified. For information about managing a collection, see [Manage collections](/docs/discovery-data?topic=discovery-data-sources#manage-collections-public).

If you modify anything in the **Sync settings** screen and then click **Save and Sync objects**, a crawl starts at that time or restarts if one is already running.
{: note}

When you connect to a data source, you can see document level errors under **Errors and warnings** on your collection page. There is a delay in publishing the errors and warnings that are related to a crawl.
{: note}

## Creating a collection using the API
{: #source_api}

Use the following process to create a collection connected to a data source, using the API.

The following example uses the SharePoint data source.

1.  Create credentials for the source that you are connecting to using the [Source Credentials API](https://{DomainName}/apidocs/discovery-data/){: external}. Record the returned **credential_id** of the newly created credentials.
2.  Create a new configuration, using the [Add configuration](https://{DomainName}/apidocs/discovery-data/){: external} API method. To define what to crawl, include a **source** object that contains the **credential_id** that you recorded earlier.
    ```json
    "source" : {
      "type" : "salesforce",
      "credential_id" : "{credential_id}",
      "schedule" : {
        "enabled" : true,
        "time_zone" : "America/New_York",
        "frequency" : "weekly"
      },
      "options" : {
         "site_collections" : [ {
         "site_collection_path" : "/sites/TestSiteA",
         "limit" : 10
         } ]
      }
    }
    ```
    {: codeblock}
    Record the returned **configuration_id** of the newly created configuration.
3.  Create a new collection using the [Collections API](https://{DomainName}/apidocs/discovery-data/){: external}. The object defining the collection must contain the **configuration_id** that you recorded earlier.

The source crawl begins as soon as you create the collection. After the initial crawl, all subsequent crawls run on the frequency that you specified. For information about managing a collection, see [Manage collections](/docs/discovery-data?topic=discovery-data-sources#manage-collections-public).

If you modify anything in the **source** object of the configuration, a new crawl starts at that time or restarts if one is already running.
{: note}

### Specifying a `customer_id`
{: #source_customer_id}

A `customer_id` field in an ingested {{site.data.keyword.discoveryshort}} document can be used to delete content based on the `customer_id` using the **user-data** method in the API. Incoming documents from a data source are not automatically assigned a `customer_id` when ingested. If your application requires a `customer_id` to be defined, you can specify one (or more) of the incoming fields from the source system to be copied and used as a `customer_id`. To do this you must modify the configuration that is being used to connect to the source.

1.  Perform a sample query and identify which field you want to use as a `customer_id`.
2.  Modify the configuration. Add a **Normalization** section to create the `customer_id` field.
    -  In the tooling, navigate to your collection and click the **edit** link in the configuration section. Next, click the **Normalization** tab and add in a **copy** normalization to create the `customer_id` field. Then click **Apply & save**.
    ![Copy normalization](images/norm_copy.png)
    -  When you use the API, add the following object to the **normalizations** array:
       ```json
       {
         "operation" : "copy",
         "source_field" : "{original_field_name}",
         "destination_field" : "customer_id"
       }
       ```
       {: codeblock}
3.  The next scheduled crawl adds the `customer_id` field to all documents. To start a crawl immediately, modify the source configuration (**Sync settings** in the tooling).

See [Information security](/docs/discovery-data?topic=discovery-data-information-security) for more information and information about deleting based on `customer_id`.

## Managing collections
{: #manage-collections-public}

After you create a collection, you can view a crawler status or change the content that you want to crawl, your security credentials to connect to a data source, or a crawler schedule.
{: shortdesc}

When you click **Manage data**, these tabs are available after collection processing finishes. The tabs contain data that is associated with your collection and options for managing it.

**Overview** tab:
- The number of documents
- The collection status. While syncing is in progress, the collection status states, `Sync in progress`. If you recrawl your collection when the sync is in progress, the current crawler stops, and a new full crawling session begins. Unless you want to make a change to your collection immediately, you might want to wait until syncing completes before starting a recrawl. When collection processing completes, you receive a status message that states, `Your documents have finished processing! You can now work with your full data set.`.
- The creation and last update dates of the collection
- A list of warnings and errors
- Any fields that the crawler identified from your data
- Any enrichments that were added to your data and the option to **Add enrichments**
- Available sample queries and the option to **Build your own query**

**Errors and warnings** tab:
- A list of any warnings and errors that might appear while your collection processes, such as the affected file name and its associated document ID

**Sync settings** tab:
- The option to change your security credentials. If your security credentials for connecting to a data source change, you must update your credentials. To update your credentials, in the **Your service's credentials** pane, click **Edit credentials**.
- The option to edit the content that you want to crawl in the **Enter the data that you would like to sync** pane. You can change or delete any URL or file path that you already specified. To delete a URL or file path, click the minus icon next to the ![Settings](images/icon_settings.png) icon.
- The option to change your crawler schedule in the **Additional settings** pane by clicking **Sync frequency**
- The **Crawl settings** dialog box. For example, if you select **Web Crawl** and you already added a start URL, you can click the ![Settings](images/icon_settings.png) icon next to the start URL to access the **Crawl settings** dialog box. In this dialog box, you can specify the **Maximum hops** or exclude URLs that include specific subdirectories in **Exclude URLs where the path includes**.

**Search settings** tab:
- The option to upload a synonym list file to enhance your query
- The option to upload a stopwords file to further enhance the relevance of your results

For information about creating a collection, see [Creating a collection using the tooling](/docs/discovery-data?topic=discovery-data-sources#source_tooling) or [Creating a collection using the API](/docs/discovery-data?topic=discovery-data-sources#source_api).

## Data source connection and data isolation
{: #source_isolation}

[Connecting to external data sources](/docs/discovery-data?topic=discovery-data-sources) reduces the data isolation of your service instance because data in transit between the source and the service cannot be isolated. All other isolation (at-rest, administration, query) remains in full. All in-flight communication between and within services and data sources is encrypted using TLS v1.2. The private keys for the TLS certificates are encrypted at rest using AES-256-GCM, the service certificates expire every three years, and the certificate revocation lists are updated monthly. All credentials are sent over an encrypted connection using TLS v1.2 and encrypted at rest using AES-256. Connections to those data sources use whatever secure protocols are supported by those data sources.
