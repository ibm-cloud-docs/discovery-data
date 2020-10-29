---

copyright:
  years: 2015, 2020
lastupdated: "2020-10-29"

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

-  [Salesforce](/docs/discovery-data?topic=discovery-data-sources#connectsfpublic)
-  [Microsoft SharePoint Online](/docs/discovery-data?topic=discovery-data-sources#connectsppublic)
-  [Web Crawl](/docs/discovery-data?topic=discovery-data-sources#connectwebcrawlpublic)
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

-  The individual document file size limit for Salesforce, SharePoint Online, {{site.data.keyword.cloud_notm}} Object Storage, and Web Crawl is 10MB, and the file size limit for uploading data is 32MB.
-  If you crawl Salesforce, a list of available resources is presented when you configure a source, using the {{site.data.keyword.discoveryshort}} tooling.
-  You can configure a collection with a single data source.
-  You must obtain an appropriate level of service license, for example Enterprise, for the data source. For information about the appropriate service level license that you need, contact the source system administrator.
-  {{site.data.keyword.discoveryshort}} source crawls do not delete documents that are stored in a collection. When a source is re-crawled, new documents are added, updated documents are modified to the current version, and deleted documents remain as the version last stored.

View the following table to see the objects that a data source can crawl and which data sources support crawling new and modified documents during a refresh:

Data source                          | Crawls new and modified documents during refresh? | Compatible objects that can be crawled
------------------------------------ | ------------------------------------------------- | --------------------------------------
Salesforce                           | Yes                                               | Any default and custom objects that you have access to, accounts, contacts, cases, contracts, knowledge articles, attachments
Microsoft SharePoint Online          | Yes                                               | SiteCollections, websites, lists, list items, document libraries
Web Crawl                            | No                                                | Websites, website subdirectories
{{site.data.keyword.cloud_notm}} Object Storage             | Yes                                               | Buckets, files
{: caption="Table 1. Data sources that support crawling new and modified documents during refresh and objects that can be crawled" caption-side="top"}

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


You can use the web crawler to crawl public websites that don’t require a password. You can select how often you'd like {{site.data.keyword.discoveryshort}} to sync with the websites, the language, and the number of hops.

-  `Start URLs` - Enter your URL and click the **Add** button to add it to the URL group. To specify the **Crawl settings** for this URL group, click the ![Cog](images/icon_settings.png) icon. You can set the **Maximum hops**, which is the number of consecutive links to follow from the starting URL (the starting URL is `0`). The default number of hops is `2` and the maximum is `20`. You can specify URL paths to exclude from the crawl in the **Exclude URLs where the path includes** field. Separate the paths, using commas, for example, if you specified the URL `http://domain.com`, you could exclude `http://domain.com/licenses` and `http://domain.com/pricing` by entering `/licenses/, /pricing/`.

When you specify a URL to crawl, the final `/` determines the subtree to crawl. For example, if you enter the URL `https://www.example.com/banking/faqs.html`, all URLs that begin with `https://www.example.com/banking/` are crawled, and the input of `https://www.example.com/banking` crawls all URLs that begin with `https://www.example.com/`. If you would like to restrict the crawl to a specific URL, such as `https://www.example.com/banking/faqs.html`, enter that URL in the `URL group to sync` field, and then set the **Maximum hops** to `0`.

The web crawler does not crawl dynamic websites that use JavaScript to render content. You can confirm the use of JavaScript by viewing the source code of the website in your browser.

The number of web pages crawled is limited to 250,000, so the web crawler might not crawl all the specified websites and might reach the maximum number of hops.
{: note}

The crawler has a limit of 10,000 child URLs per URL that is crawled. If the number of child URLs within any crawled URL exceeds 10,000, the crawler cannot process any of the content in the child URLs.
{: note}

If you require different **Crawl settings** for other URLs, click **Add URL group** and create a new group. You can create as many URL groups as you need.
{: tip}


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

## Data source connection and data isolation
{: #source_isolation}

[Connecting to external data sources](/docs/discovery-data?topic=discovery-data-sources) reduces the data isolation of your service instance because data in transit between the source and the service cannot be isolated. All other isolation (at-rest, administration, query) remains in full. All in-flight communication between and within services and data sources is encrypted using TLS v1.2. The private keys for the TLS certificates are encrypted at rest using AES-256-GCM, the service certificates expire every three years, and the certificate revocation lists are updated monthly. All credentials are sent over an encrypted connection using TLS v1.2 and encrypted at rest using AES-256. Connections to those data sources use whatever secure protocols are supported by those data sources.
