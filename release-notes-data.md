---

copyright:
  years: 2019, 2022
lastupdated: "2022-03-04"

keywords: discovery release notes,discovery cloud pak for data release notes,watson discovery release notes,what's new,new features,improvements,change log,changelog

subcollection: discovery-data
content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}}
{: #release-notes-data}

Learn about features and changes that were included for each release and update of the product software.
{: shortdesc}

![{{site.data.keyword.cpd_full_notm}} only](images/desktop.png) **{{site.data.keyword.cpd_full_notm}} only** 

This information applies only to instances of {{site.data.keyword.discoveryfull}} that are installed on {{site.data.keyword.icp4dfull}}. For information about releases and updates for managed deployments, see [Release notes for Watson Discovery for {{site.data.keyword.cloud_notm}}](/docs/discovery-data?topic=discovery-data-release-notes).
{: note}

See [Known issues](/docs/discovery-data?topic=discovery-data-known-issues) for the list of {{site.data.keyword.discoveryfull}} known issues.

## 4.0.6 release, 1 March 2022
{: #discovery-data-1march2022}

{{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.6 is available.

Multitenancy is now supported
:   An administrator can now create up to 10 instances of the Discovery service per deployment, which means that more teams can work on discrete Discovery projects at the same time.

Simpler installation and management of custom connectors
:   The `manage_custom_crawler.sh` script was improved to make it easier for you to install and manage your custom connectors in a multitenant environment. For more information, see [Installing a custom crawler](/docs/discovery-data?topic=discovery-data-install-connector).

Security vulnerabilities were addressed
:   The following security patches were applied:

    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Java](https://www.ibm.com/support/pages/node/6556970)
    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Logback](https://www.ibm.com/support/pages/node/6556972)
    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Apache Log4j](https://www.ibm.com/support/pages/node/6556974)

Features that are not available in this release
:   The following features are generally available from managed {{site.data.keyword.cloud_notm}} deployments at the time of this release, but not from installed deployments:

    -   Home page updates
    -   Answer finding
    -   Access to guided tours from the page header

## 4.0.5 release, 26 January 2022
{: #discovery-data-26january2022}

{{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.5 is available.

A security vulnerability was addressed
:   The following security patch was applied: [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Apache Log4j](https://www.ibm.com/support/pages/node/6538332)

Features that are not available in this release
:   The following features are generally available from {{site.data.keyword.cloud_notm}} deployments at the time of this release, but not from installed deployments:

    -   Home page updates
    -   Answer finding
    -   Guided tours

## 4.0.4 release, 20 December 2021
{: #discovery-data-20december2021}

{{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.4 is available.

Guided tours are available
:   Access guided tours from anywhere in the product user interface by clicking the **Guided tours** button in the page header.

Security vulnerabilities were addressed
:   The following security patches were applied:

    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in LibTIFF](https://www.ibm.com/support/pages/node/6523814)
    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in TensorFlow](https://www.ibm.com/support/pages/node/6523816)
    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Node.js](https://www.ibm.com/support/pages/node/6523818)
    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Netty](https://www.ibm.com/support/pages/node/6523820)
    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Apache Log4j](https://www.ibm.com/support/pages/node/6526072)
    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Apache Log4j 1.2](https://www.ibm.com/support/pages/node/6526478)

Features that are not available in this release
:   The following features are generally available from {{site.data.keyword.cloud_notm}} deployments at the time of this release, but not from installed deployments:

    -   Home page updates
    -   Answer finding

## 4.0.3 release, 30 November 2021
{: #discovery-data-30november2021}

{{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.3 is available.

Another storage option is supported
:   IBM Spectrum Scale Container Native storage is now supported in addition to Red Hat OpenShift Container Storage and Portworx.

Microsoft SharePoint Online data source improvement
:   The *Sharepoint Online* data source now supports crawling your data as a service principal, which means you can access your data without disabling multifactor authentication. For more information, see [Microsoft Sharepoint Online](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cp4d).

Microsoft Windows File System improvements
:   Extra configuration options mean you can specify the following information:

    -   The types of files (by file extension) to include or exclude from a crawl of a Windows directory.
    -   The character encoding of the data to be crawled. Typically, the encoding is detected automatically. However, you can choose to specify the character encoding as a Java character set yourself.

    For more information, see [Windows File System](/docs/discovery-data?topic=discovery-data-connector-wfs-cp4d).

Field selection is improved
:   When you apply an enrichment to a field or choose a field to use as the source for a facet, the fields that are displayed for you to choose from now shows only fields that are valid choices.

Search settings change
:   The spelling correction setting changed from being enabled automatically in new projects to being disabled by default. If you want to alert users when they misspell a term in their query, turn on *Spelling suggestions*. For more information, see [Customizing the search bar](/docs/discovery-data?topic=discovery-data-search-bar).

A Salesforce crawling issue was fixed
:   Previously, {{site.data.keyword.discoveryshort}} had an issue where it timed out before it crawled some of the object types in a Salesforce collection. If your collection is configured to crawl the following object types, run a full data source crawl to make sure that your collection contains the most up-to-date data from all of the objects in your Salesforce data source:

    -   Attachment
    -   ContentVersion
    -   Document

Security vulnerabilities were addressed
:   The following security patches were applied:

    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Node.js](https://www.ibm.com/support/pages/node/6516464){: external}
    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Axios](https://www.ibm.com/support/pages/node/6516466){: external}
    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Python Pillow](https://www.ibm.com/support/pages/node/6516468){: external}
    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Apache Commons Compress](https://www.ibm.com/support/pages/node/6516470){: external}
    -   [Security Bulletin: IBM Watson Discovery for IBM Cloud Pak for Data affected by vulnerability in Java](https://www.ibm.com/support/pages/node/6516472){: external}

Features that are not available in this release
:   The following features are available from {{site.data.keyword.cloud_notm}} deployments at the time of this release, but not from installed deployments:

    -   Home page updates
    -   Guided tours
    -   Answer finding

## 4.0.2 release, 5 October 2021
{: #release-notes-data-5october2021}

{{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.2 is available.

Support for newer platform software
:   {{site.data.keyword.icp4dfull}} 4.0.2 can be installed on {{site.data.keyword.openshiftlong}} 4.8.

New scoring for NLU enrichments
:   Relevance and confidence scores are displayed for NLU enrichments that are returned by search. For example, when you open the JSON view of the document preview from a query result, you can see confidence scores for Entities mentions and relevance scores for Keyword mentions.

Improved Web crawl
:   The *Web crawl* data source supports more customization options, including the ability to ignore a site's robots.txt file. For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cp4d).

New upgrade support
:   The 4.0.2 release supports in-place upgrade from {{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.0. For more information, see [Upgrading Watson Discovery to a newer 4.0 refresh](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=discovery-upgrading-watson-version-40){: external}

## IBM Cloud Private End Of Support
{: #release-notes-data-30september2021}

Effective 30 September 2021, IBM withdrew support for the following programs:

-   IBM Watson Assistant Discovery Extension for IBM Cloud Private 2.1.0–2.1.4
-   IBM Watson Discovery for ICP for Data 2.1.0–2.1.4
-   IBM Watson Discovery for ICP for Data Add-on 2.1.0–2.1.4

For more information, see announcements [ENUS921-005.PDF](https://www.ibm.com/common/ssi/cgi-bin/ssialias?subtype=ca&infotype=an&appname=iSource&supplier=897&letternum=ENUS921-005){: external} and [ENUSLP21-0099.PDF](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/9/899/ENUSLP21-0099/index.html&request_locale=en).

## 4 release, 13 July 2021
{: #release-notes-data-13july2021}

New version now available
:   {{site.data.keyword.discovery-data_short}} 4 is available
:   This release is supported on {{site.data.keyword.icp4dfull}} 4.0.0.

Change to service name
:   The new name is {{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}}.

New Smart Document Understanding (SDU) predefined model
:   When you identify fields, instead of annotating documents with the SDU tool, you can choose to use a pretrained model. The pretrained model applies a non-customizable model that automatically extracts text and identifies tables, lists, and sections.

Improved contract analysis
:   To enable the Contracts enrichment that recognizes and tags contract-related concepts in your data, you can choose to create a Document Retrieval project type, and then select **Apply contracts enrichment**. You no longer need to use an installation override YAML file to enable it. This change also means that you can choose which Document Retrieval projects use the Contracts enrichment; it is not applied to all Document Retrieval projects automatically.

New LDAP directory data source
:   Connect to data that is stored in an external directory that supports the Lightweight Directory Access Protocol (LDAP), such as a corporate email directory. As the directory data is added to your collection, {{site.data.keyword.discoveryshort}} interprets and stores key attributes of each record, such as department and location information. Later, you can find relevant records by filtering on these attribute categories. For more information, see [LDAP directory](/docs/discovery-data?topic=discovery-data-connector-ldap-cp4d).

Improved SharePoint OnPrem connection process
:   The steps you follow to connect to a SharePoint instance that is hosted on-premises were simplified. You no longer need to deploy a web services package on the SharePoint server before you can connect to the SharePoint OnPrem data source. For more information, see [SharePoint OnPrem](/docs/discovery-data?topic=discovery-data-connector-sharepoint-onprem-cp4d).

New Salesforce proxy support
:   You can now connect to a Salesforce data source when using a proxy server. For more information, see [Salesforce](/docs/discovery-data?topic=discovery-data-connector-salesforce-cp4d).

Improved custom connector improvements
:   Support was added for Optical character recognition (OCR)
:   Support was added for Document-level security

    For more information about the custom connector, see [Building a Cloud Pak for Data custom connector](/docs/discovery-data?topic=discovery-data-build-connector).

Change to Dynamic Faceted Search
:   Support for *Dynamic Faceted Search* and its associated `suggested_refinements` API query parameter was removed.

## 2.2.1 release, 26 February 2021
{: #release-notes-data-26february2021}

New release now available
:   IBM Watson™ Discovery for IBM Cloud Pak for Data version 2.2.1 is available.

Support for upgrade
:   {{site.data.keyword.discovery-data_short}} supports an in-place upgrade from version 2.2.0 to 2.2.1 so that you do not need to manually uninstall an earlier version and then install the latest version of the service. For more information, see [Upgrading Discovery for Cloud Pak for Data](/docs/discovery-data?topic=discovery-data-install#upgrade-discovery).

New SDK download support
:   You can now download the custom connector SDK package from your {{site.data.keyword.discovery-data_short}} cluster, instead of retrieving the images and the SDK package from the Docker registry. For more information, see [Downloading the custom-crawler-docs.zip file in Discovery 2.2.1 and later](/docs/discovery-data?topic=discovery-data-connector-dev#download-ccs-zip).

Change to Invoices and Purchase orders
:   `Invoices` and `Purchase orders` models can no longer be enabled in the tooling. If you need these models, please contact [IBM Cloud Support](https://cloud.ibm.com/unifiedsupport/supportcenter){: external} to obtain instructions for enabling these models.

Change to Contracts enrichment tables
:   In a `Document Retrieval` project that has the `Contracts` enrichment applied, tables are not included inside the `contracts` field, as they were previously in projects that had the `Contracts` enrichment enabled. Tables will continue to be included in a separate `tables` field when the `Table Understanding` enrichment is applied.

Change to support for Oracle Database 11g and Postgres 9.5
:   Support for connecting to Oracle Database 11g was removed because the vendor ended version support on 31 December 2020.
:   Support for connecting to Postgres 9.5 was removed because the vendor ended version support on 11 February 2021.

## 2.2.0 release, 8 December 2020
{: #release-notes-data-8december2020}

New release now available
:   IBM Watson™ Discovery for IBM Cloud Pak for Data version 2.2 is available. 
:   {{site.data.keyword.discovery-data_short}} now works with I{{site.data.keyword.icp4dfull}} 3.5.

New support for Notes attachments
:   Added support for attachments in the Notes data source. For more information, see [Notes](/docs/discovery-data?topic=discovery-data-collection-types#connectnotes)

New web crawl scheduling option
:   You can specify the exact time that you would like your crawls to run for any data source, giving you the flexibility to run them at the times you prefer. For more information, see [Configuring Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types).

New Facet creation in Content Miner
:   You can now create Facet groups in a Content Miner application. For more information, see [Facet analysis pane](/docs/discovery-data?topic=discovery-data-contentminerapp#cmofap).

New custom crawler creation
:   Added the option to create your own custom crawler plug-in. For more information, see [Building a Cloud Pak for Data crawler plug-in](/docs/discovery-data?topic=discovery-data-crawler-plugin-build) **Note:** Any custom code used with Watson Discovery is the responsibility of the developer and is not covered by IBM support.

Change to Dynamic Facets
:   Dynamic Facets are no longer enabled by default in Document Retrieval projects.

## 2.1.4 release, 2 September 2020
{: #release-notes-data-2september2020}

New release now available
:   {{site.data.keyword.discovery-data_long}} version 2.1.4 is available.

New Notes connector
:   Crawl Notes version 9.0.1 systems. For more information, see [Notes connector](/docs/discovery-data?topic=discovery-data-collection-types#connectnotes).

New **Enable proxy settings** in multiple connectors
:   You can now select the option to enable proxy settings in [Box](/docs/discovery-data?topic=discovery-data-collection-types#connectbox), [Microsoft SharePoint Online](/docs/discovery-data?topic=discovery-data-collection-types#connectsp), and [Microsoft SharePoint OnPrem](/docs/discovery-data?topic=discovery-data-collection-types#connectsp_op) connectors.

New options for Database connector
:   Added support for multiple tables and the Row filter option to the [Database connector](/docs/discovery-data?topic=discovery-data-collection-types#databaseconnect).

New authentication types for Web crawler
:   You can select from three new authentication types in [Web crawler](/docs/discovery-data?topic=discovery-data-collection-types#connectwebcrawl): Basic authentication, NTLM authentication, and FORM authentication.

New Analyze API usage monitoring 
:   You can now monitor the usage of the Analyze API using the tooling. For more information, see [Monitoring usage](/docs/discovery-data?topic=discovery-data-analyzeapi#api-usage).

## 30 August 2020
{: #release-notes-data-30august2020}

Update to API version
:   The current API version (v2) is now 2020-08-30. The following change was made with this version:

Change to 'options' object
:   The List enrichments method no longer returns the `options` object per enrichment. Use the Get enrichment method to return the `options` object for a single enrichment.

## 2.1.3 release, 19 June 2020
{: #release-notes-data-19june2020}

New release now available
:   {{site.data.keyword.discovery-data_long}} version 2.1.3 is available.
:   {{site.data.keyword.discovery-data_short}} now works with {{site.data.keyword.icp4dfull}} 3.0.1.

New Finnish and Hebrew language support
:   Added basic support for Finnish and Hebrew. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

Change to Analyze endpoint
:   The Analyze endpoint, which supports stateless document ingestion workflows. For details, see the [Analyze API](/docs/discovery-data?topic=discovery-data-analyzeapi). The Analyze API supports JSON documents only. Use of the Analyze API affects license usage, please reference the latest [license information](http://www.ibm.com/software/sla/sladb.nsf/searchlis/?searchview&searchorder=4&searchmax=0&query=(watson+discovery){: external}.

New options for Content Miner
:   The content mining application includes two new options: [Cyclic time scale](/docs/discovery-data?topic=discovery-data-contentminerapp#cmotsdb) on the Time series dashboard, and the [Contextual view](/docs/discovery-data?topic=discovery-data-contentminerapp#contextual-view) tab.

New shortcut for Content Mining projects
:   For **Content Mining** projects only, the **Improve and customize** page includes a shortcut: the **Launch application** button. Previously, you were required to open the **Integrate and deploy** page, select the **Launch application** tab, and click the **Launch** button.

Improved segment limit
:   The segment limit when splitting documents has been increased to 1,000. For details, see [Split documents to make query results more succinct](/docs/discovery-data?topic=discovery-data-split-documents).

Improved Filenet connector
:   The [Filenet connector](/docs/discovery-data?topic=discovery-data-collection-types#filenet-connect) has document level security.

New beta Curations feature
:   You can specify up to 1,000 curations. For details about this beta feature, see [Curations](/docs/discovery-data?topic=discovery-data-train#curations).

Fixed defects in the 2.1.3 release
:   In versions 2.1.2, 2.1.1, and 2.1.0, PNG, TIFF, and JPG individual image files are not scanned, and no text is extracted from those files. PNG, TIFF, and JPEG images embedded in PDF, Word, PowerPoint, and Excel files are also not scanned, and no text is extracted from those image files.

## 2.1.2 release, 31 March 2020
{: #release-notes-data-31march2020}

New release now available
:   {{site.data.keyword.discovery-data_long}} version 2.1.2 is available.

New **IBM FileNet connector**
:   You can now crawl IBM FileNet systems. For more information, see [FileNet connector](/docs/services/discovery-data?topic=discovery-data-collection-types#filenet-connect).

New Swedish, Norwegian, and Danish language support
:   Added basic support for Swedish, Norwegian (Bokma&#778;l and Nynorsk), and Danish. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

Change to Advanced Rule models enrichment
:   The [Advanced Rule models enrichment](/docs/discovery-data?topic=discovery-data-domain#advanced-rules) is now GA.

New document preview for search results
:   You can now view your search results in a document preview for the following source documents: PDF, Word, PowerPoint, Excel, and all image files. See [supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes) for the list of image files. This view makes it easier for you to see search results as highlighted passages within the text of the original document, making the context clearer.

New proxy support for Web Crawl
:   Support was added to the [Web Crawl connector](/docs/services/discovery-data?topic=discovery-data-collection-types#connectwebcrawl) for proxy support.

Change to empty aggregations parameter
:   Running a query with an empty `aggregations` parameter returns zero aggregations in the response.

Change to Postgres support
:   Support for connecting to Postgres 9.4 was removed because the vendor ended version support was ended by the vendor on 13 February 2020.

Fixed the following defects in the 2.1.2 release
:   When installing {{site.data.keyword.discovery-data_short}} on OpenShift, the `ranker-rest` service might intermittently fail to startup, due to an incompatible jar in the `classpath`.
:   When you upload documents to a collection with existing documents, a `Documents uploaded!` message displays on the **Activity** page, but no further processing status displays until the number of documents increases.
:   Running a query with an empty `aggregations` parameter returns an empty aggregations array.
:   Deprovisioning a {{site.data.keyword.discovery-data_long}} Instance will not delete the underlying data. Delete the collections and documents manually.

## 2.1.1 release, 24 January 2020
{: #release-notes-data-24january2020}

New release now available
:   {{site.data.keyword.discovery-data_long}} version 2.1.1 is available.

Fixed the following defects in the 2.1.1 release:
:   In Document Retrieval project types, when you perform an empty search, and the search results source is set to `passages,` the query results will display `excerpt unavailable` in the Project workspace.
:   When visiting the Storybook links on the Integrate and deploy page, the links do not go to the correct location. Please visit [Storybook](https://watson-developer-cloud.github.io/discovery-components/storybook){: external} instead to view documentation.
:   If you are using Smart Document Understanding, two variables no longer need to be set during installation or reinstallation. For more information, see [Environment variable settings for Smart Document Understanding](/docs/discovery-data?topic=discovery-data-troubleshoot#troubleshoot-sdu).
:   Discovery for Content Intelligence and Table Understanding enrichments are configured out of the box to be applied on a field named `html`. When a user uploads a JSON document without a root-level field named `html`, these enrichments will not yield results in the index. To run the enrichments on this kind of JSON documents, users must re-configure the enrichments to run on an existing field (or fields) in the JSON document.

## 2.1.0 release, 27 November 2019
{: #release-notes-data-27november2019}

New release now available
:   {{site.data.keyword.discovery-data_long}} version 2.1.0 is available.
:   {{site.data.keyword.discovery-data_short}} now works with {{site.data.keyword.icp4dfull}} 2.5.0.0.

New Project-based interface
:   Test your application like an end-user would with the **Document retrieval**, **Conversational Search**, and **Content Mining** project types. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).

New Content Mining app
:   Build an end user interface for extracting insights proactively from your entire corpus. For more information, see [Using the Content Mining application](/docs/discovery-data?topic=discovery-data-contentminerapp).

New Content Intelligence add-on
:   Option to enrich your documents with pre-built domain knowledge for Contracts. For more information, see [Document Retrieval for Contracts](/docs/discovery-data?topic=discovery-data-projects#doc-retrieval-contracts).

New reusable components
:  Use reusable components to quickly build your application with Discovery. We ship an autocomplete, rich preview, results and facets component. For more information, see [Building and deploying components](/docs/discovery-data?topic=discovery-data-deploy).

New Czech, Polish, Romanian, Russian, and Slovak language support
:   Basic support for Czech, Slovak, Russian, Polish and Romanian is added. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

New built-in table understanding
:   Extract tables from your documents without training, and optionally return tables as answers to natural language queries. For more information, see [Understanding tables](/docs/discovery-data?topic=discovery-data-understanding_tables).

New SDK connector
:   Build custom connectors your Discovery users can use to build their own applications. For more information, see [Building and implementing a custom connector](/docs/discovery-data?topic=discovery-data-build-connector).

New pre-built sample project
:   The sample project is preloaded with data, so you can learn about Discovery. For more information, see [Getting started with Watson Discovery](/docs/discovery-data?topic=discovery-data-getting-started).

New passage retrieval
:   Will return the most relevant passages from your documents, plus you can specify the number of passages returned per document. See [Passages](/docs/discovery-data?topic=discovery-data-query-parameters#passages).

New project-level querying and relevancy training
:   Query multiple collections at once including relevance training.

Improved Web crawl connector
:   Additional options now available for the **Web crawl connector** - For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-collection-types#connectwebcrawl).

New Local File System connector
:   Crawl Linux or other file systems. For more information, see [Local file system](/docs/discovery-data?topic=discovery-data-collection-types#localfilesystemconnect)

New dynamic Facets
:   Automatically generate facets based on the understanding of your data. For more information, see [Facets](/docs/discovery-data?topic=discovery-data-facets).

New Dictionary suggestions
:   Dictionary terms are suggested based on your content. For more information, see [Dictionary](/docs/discovery-data?topic=discovery-data-domain#dictionary).

New beta Curations
:   Specify a particular result for a given query. For more information, see the [API reference](https://{DomainName}/apidocs/discovery/discovery-data#createcuration){: external}.

## 2.0.1 release, 30 August 2019
{: #release-notes-data-30august2019}

New release now available
:   {{site.data.keyword.discovery-data_long}} version 2.0.1 is available.
:   {{site.data.keyword.discovery-data_short}} now works with {{site.data.keyword.icp4dfull}} 2.1.0.1.

New Windows File System and Database connectors
:   Added the Windows File System and Database connectors. For more information, see [Database connector](/docs/discovery-data?topic=discovery-data-collection-types#databaseconnect) and [Windows File System connector](/docs/discovery-data?topic=discovery-data-collection-types#windowsfilesystemconnect).

New Chinese language support
:   Added support for Traditional Chinese. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

New FISMA support
:   Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.discovery-data_long}} offerings purchased on or after August 30, 2019. FISMA support is also available to those who purchased the June 28, 2019 version and upgrade to the August 30, 2019 version. {{site.data.keyword.discovery-data_long}} is FISMA High Ready.

New Classifier enrichment
:   Released the Classifier enrichment. For more information, see [Classifier](/docs/discovery-data?topic=discovery-data-domain#classifier).

New Red Hat OpenShift support
:   Added support for installing {{site.data.keyword.icp4dfull}} on Red Hat OpenShift.

Fixed the following defects in {{site.data.keyword.discovery-data_short}} offerings purchased on or after August 30, 2019
:   During an active web crawl, if you add an enrichment, then click the **Recrawl collection** button on the **Activity** page, the collection will stop processing. If the collection does not return to a Syncing state on its own, clicking the **Recrawl collection** button an additional time might be required.
:   While training a collection in the tooling , if you rate the relevancy of a result (for example, as`Relevant`), then switch to the opposite rating (`Not relevant`), the page may go blank. To restore the page, refresh the browser. Your updated rating will be retained.
:   Chinese, Japanese, and Korean language Microsoft Word, Excel, and PowerPoint documents will not display correctly in the index or the Smart Document Understanding editor.
:   If you upload a zip, gzip, or tar file to your collection, and that file contains multiple files/file types supported by Smart Document Understanding (PDF, Word, Excel, PowerPoint, PNG, TIFF, JPEG), only one of the files in that zip, gzip, or tar file will be available for training in the SDU editor (unless the SDU document limit has already been met). All of the documents will be available in the index. Unzip the file before uploading to avoid this issue.
:   Query expansion and autocomplete return the wrong error code when the `collection_id` is invalid. Query expansion will return a `500` error code instead of a `404`. Autocomplete will return a `400` when the `collection_id` is invalid and the `prefix` parameter isn’t set. It should also return a `404`.
:   When crawling Microsoft SharePoint 2019 collections, only HTML documents will be crawled and indexed. This is a SharePoint issue with how it processes mime-types. See this Microsoft [blog post](https://blog.stefan-gossner.com/2018/11/30/common-issue-sp2019-items-in-document-libraries-are-downloaded-with-mime-type-application-octet-stream-rather-than-the-accurate-one/) for a workaround.
:   If you delete an installation of the {{site.data.keyword.discovery-data_short}} add-on, the instance will not uninstall completely and your re-installation will fail. See the {{site.data.keyword.discovery-data_short}} Readme for post-cleanup steps.
:   If a JSON document that contains nested JSON objects is ingested, the nested JSON will be indexed as a JSON string.

## 2.0.0, General Availability (GA) release, 28 June 2019
{: #release-notes-data-28june2019}

Discovery for Cloud Pak for Data now available
:   The {{site.data.keyword.discovery-data_long}} service brings the cognitive capabilities of {{site.data.keyword.discoveryfull}} to the {{site.data.keyword.icp4dfull}} platform.
