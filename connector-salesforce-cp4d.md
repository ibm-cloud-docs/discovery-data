---

copyright:
  years: 2019, 2022
lastupdated: "2021-11-16"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Salesforce
{: #connector-salesforce-cp4d}

Crawl documents that are stored in Salesforce.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments. For more information about connecting to Salesforce from a managed deployment, see [Salesforce](/docs/discovery-data?topic=discovery-data-connector-salesforce-cloud).
{: note}

## What documents are crawled
{: #connector-salesforce-cp4d-docs}

- Knowledge Articles are crawled only if their version is published and their languages is en-us.
- Only documents that are supported by {{site.data.keyword.discoveryshort}} are crawled; all others are ignored. For more information, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
- When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index during refresh.
- All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

{{site.data.keyword.discoveryshort}} can crawl the following objects:

-   Any default and custom objects that you have access to
-   Accounts
-   Contacts
-   Cases
-   Contracts
-   Knowledge articles
-   Attachments

## Data source requirements
{: #connector-salesforce-cp4d-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements) for all installed deployments, your Salesforce data source must meet the following requirements:

- The instance that you plan to connect to must be part of an Enterprise plan or higher.
- You must obtain any required service licenses for the data source that you want to connect to. For more information about licenses, contact the system administrator of the data source.

For more information about Salesforce, see the [Salesforce developer documentation](https://developer.salesforce.com/docs/){: external}.

## Prerequisite step
{: #connector-salesforce-cp4d-prereq}

To crawl documents in Salesforce, {{site.data.keyword.discoveryshort}} uses a Web Service Description Language (WSDL) file. The WSDL file defines a Web service to generate an API that manages access.

If you plan to crawl documents from both a Sandbox and Production instance of Salesforce, you must establish a connection to each web service separately. You must download JAR files from each web service and set up separate collections.
{: note}

For information about downloading the WSDL JAR files, see the following links:

-   [Generate or Obtain the Web Service WSDL](https://developer.salesforce.com/docs/atlas.en-us.210.0.api.meta/api/sforce_api_quickstart_steps_generate_wsdl.htm){: external}
-   [Import the WSDL File Into Your Development Platform](https://developer.salesforce.com/docs/atlas.en-us.210.0.api.meta/api/sforce_api_quickstart_steps_import_wsdl.htm){: external}
-   [Download Apache Commons BeanUtils](https://commons.apache.org/proper/commons-beanutils/download_beanutils.cgi){: external}
-   [Apache Commons BeanUtils](https://mvnrepository.com/artifact/commons-beanutils){: external}

1.  Download the following JAR files:

    -   `force-partner.jar` (from partner WSDL)
    -   `force-metadata.jar` (from metadata WSDL)
    -   `force-wsc.jar` (from Force.com Web Service Connector (WSC))
    -   `commons-beanutils.jar` (from Apache Commons BeanUtils)

1.  Compress the JAR files into a compressed file. You will upload the compressed file to {{site.data.keyword.discoveryshort}} in the next procedure.

### Connecting to a Salesforce data source
{: #connector-salesforce-cp4d-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Salesforce**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents in Salesforce is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  In the *Specify what you want to crawl* section, enter values in the following fields:

    Username
    :   The username to call the Salesforce API.
    
    Password
    :   The password of the specified user.
    
    Security Token
    :   The security token of the user to call Salesforce API.
    
    Jar zip archive file
    :   Upload a compressed file that contains the JAR files that you downloaded earlier. Or select a compressed file that you uploaded previously to reuse it.

1.  **Optional**: Expand the *Proxy settings* section to add information that is required if you are using a proxy server to access the data source server.

    -   **Enable proxy settings**: Set the switch to **On**, and then add the following information:

        Username
        :   The proxy server username to use to authenticate, if the proxy server requires authentication. If you do not know your username, you can get it from the administrator of your proxy server.

        Password
        :   The proxy server password to use to authenticate, if the proxy server requires authentication. If you do not know your password, you can get it from the administrator of your proxy server.

        Proxy server host name or IP address
        :   The hostname or the IP address of the proxy server.
      
        Proxy server port number
        :   The network port that you want to connect to on the proxy server.

1.  In the *Object Types** section, specify the object types to crawl.

    The default behavior is to crawl all object types.

    - For custom object names, append `__c` to match the Salesforce API convention for custom object names. For example, to crawl MyCustomObject, specify `MyCustomObject__c`.
    - Do not specify a comment object, such as `FeedComment`, `CaseComment`, `IdeaComment`, without also specifying the corresponding root object, such as `FeedItem`, `Case`, and `Idea`.
    - If you specify a tag object, you must also specify its parent. For example, do not specify the `AccountTag` object without also specifying the `Account` object.
1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    The processing time increases when this feature is enabled.
    {: note}

1. Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
