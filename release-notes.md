---

copyright:
  years: 2019, 2020
lastupdated: "2020-04-02"

keywords: release notes, known issues

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

# Release notes
{: #release-notes}

The release notes provide information about changes to {{site.data.keyword.discovery-data_long}} since the previous release.
{: shortdesc}

## Service API Versioning
{: #apiversioning}

API requests require a version parameter that takes a date in the format `version=YYYY-MM-DD`. Whenever we change the API in a backwards-incompatible way, we release a new minor version of the API.

Send the version parameter with every API request. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.

The current version is `2019-11-29`.

## Beta features
{: #beta-features}

IBM releases services, features, and language support for your evaluation that are classified as beta. These features might be unstable, might change frequently, and might be discontinued with short notice. Beta features also might not provide the same level of performance or compatibility that generally available features provide and are not intended for use in a production environment.

## Changes
{: #change-log}

The following new features and changes to the service are available.

See [Known issues](/docs/discovery-data?topic=discovery-data-known-issues) for the list of {{site.data.keyword.discovery-data_long}} known issues.

### 2.1.2 release, 31 Mar 2020
{: #31mar2020}

**{{site.data.keyword.discovery-data_long}} version 2.1.2 is available.**

Changes made in this release:

  -  **IBM FileNet connector** added - Crawl IBM FileNet systems. For more information, see [FileNet connector](/docs/services/discovery-data?topic=discovery-data-collections#filenet-connect). 
  -  Added basic support for Swedish, Norwegian (Bokma&#778;l and Nynorsk), and Danish. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
  - The [Advanced Rule models enrichment](/docs/discovery-data?topic=discovery-data-create-enrichments#advanced-rules) is now GA.
  - Several **enhancements to the tooling**; including improvements to the navigation, messages, and status updates.
  - You can now view search results in a preview of your document. This feature is available for the following source documents: PDF, Word, PowerPoint, Excel, and all image files. See [supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes) for the list of image files.
  -  The [Web Crawl connector](/docs/services/discovery-data?topic=discovery-data-collections#connectwebcrawl) has proxy support. 
  -  Running a query with an empty `aggregations` parameter returns zero aggregations in the response.
  
Issues resolved in the {{site.data.keyword.discovery-data_short}} 2.1.2 release:

  -  When installing {{site.data.keyword.discovery-data_short}} on OpenShift, the `ranker-rest` service might intermittently fail to startup, due to an incompatible jar in the `classpath`.
  -  When you upload documents to a collection with existing documents, a `Documents uploaded!` message displays on the **Activity** page, but no further processing status displays until the number of documents increases.
  -  Running a query with an empty `aggregations` parameter returns an empty aggregations array. 
  
### 2.1.1 release, 24 Jan 2020
{: #24jan2020}

**{{site.data.keyword.discovery-data_long}} version 2.1.1 is available.**

Issues resolved in the {{site.data.keyword.discovery-data_short}} 2.1.1 release:

  -  In Document Retrieval project types, when you perform an empty search, and the search results source is set to `passages,` the query results will display `excerpt unavailable` in the Project workspace.
  -  When visiting the Storybook links on the Integrate and deploy page, the links do not go to the correct location. Please visit [Storybook](https://watson-developer-cloud.github.io/discovery-components/storybook){: external} instead to view documentation.
  -  If you are using Smart Document Understanding, two variables no longer need to be set during installation or reinstallation. See [Environment variable settings for Smart Document Understanding](/docs/discovery-data?topic=discovery-data-troubleshoot#troubleshoot-sdu) for details.


### 2.1.0 release, 27 Nov 2019
{: #27nov2019}

**{{site.data.keyword.discovery-data_long}} version 2.1.0 is available.** 

{{site.data.keyword.discovery-data_short}} now works with {{site.data.keyword.icp4dfull}} 2.5.0.0.

Changes made in this release:

  -  New **Project** based interface - Test your application like an end-user would with the **Document retrieval**, **Conversational Search**, and **Content Mining** project types. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).
  -  **Content Mining** - Build an end user interface for extracting insights proactively from your entire corpus. For more information see [Mining Content](/docs/discovery-data?topic=discovery-data-contentminerapp).
  -  **Content Intelligence** - Optional add-on to enrich your documents with pre-built domain knowledge for Contracts, Invoices, and Purchase Orders. For more information, see [Understanding Discovery for Content Intelligence](/docs/discovery-data?topic=discovery-data-output_schema).
  -  **Reusable components** to quickly build your application using Discovery. We ship an autocomplete, rich preview, results and facets component. For more information, see [Building and deploying components](/docs/discovery-data?topic=discovery-data-deploy).
  -  **Additional Language support** - Basic support for Czech, Slovak, Russian, Polish and Romanian. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
  -  **Out of the box table understanding** - Extract tables from your documents without training, and optionally return tables as answers to natural language queries. For more information, see [Table understanding](/docs/discovery-data?topic=discovery-data-understanding_tables). 
  -  **Connector SDK** - Build custom connectors your Discovery users can use to build their own applications. For more information, see [Building and implementing a custom connector](/docs/discovery-data?topic=discovery-data-build-connector).
  -  **Sample Project** - The sample project is preloaded with data so you can learn about Discovery. For more information, see [Getting started with Watson Discovery for IBM Cloud Pak for Data](/docs/discovery-data?topic=discovery-data-getting-started).
  -  **Passage retrieval** - Will return the most relevant passages from your documents, plus you can specify the number of passages returned per document. See [passages](/docs/discovery-data?topic=discovery-data-query-parameters#passages).
  -  **Project level querying and relevancy training** - Query multiple collections at once including relevance training. For more information, see [Customizing and improving your project](/docs/discovery-data?topic=discovery-data-improve)
  -  Improvements and additional options to the **Web crawl connector** - For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-collections#connectwebcrawl).
  -  **Local File System connector** added - Crawl Linux or other file systems. For more information, see [Local file system](/docs/discovery-data?topic=discovery-data-collections#localfilesystemconnect)
  -  **Dynamic Facets** - Automatically generate facets based on the understanding of your data. For more information, see [Facets](/docs/discovery-data?topic=discovery-data-facets).
  -  **Dictionary suggestions** - Dictionary terms will be suggested to you based on your content. For more information, see [Dictionary enrichments](/docs/discovery-data?topic=discovery-data-create-enrichments#dictionary-enrichment).
  -  **Curations** (beta) - Specify a particular result for a given query. For more information, see [Curations](https://cloud.ibm.com/apidocs/discovery/discovery-data-v2#create-curation){: external}.


### 2.0.1 release, 30 August 2019
{: #30aug2019}

**{{site.data.keyword.discovery-data_long}} version 2.0.1 is available.** 

{{site.data.keyword.discovery-data_short}} now works with {{site.data.keyword.icp4dfull}} 2.1.0.1. 

Changes made in this release:

  -  Added the Windows File System and Database connectors.  See [Database connector](/docs/discovery-data?topic=discovery-data-collections#databaseconnect) and [Windows File System connector](/docs/discovery-data?topic=discovery-data-collections#windowsfilesystemconnect) for details.
  -  Added support for Traditional Chinese. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
  -  Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.discovery-data_long}} offerings purchased on or after August 30, 2019. FISMA support is also available to those who purchased the June 28, 2019 version and upgrade to the August 30, 2019 version. {{site.data.keyword.discovery-data_long}} is FISMA High Ready.
  -  Released the Classifier enrichment. See [Classifier enrichment](/docs/discovery-data?topic=discovery-data-create-enrichments#classifier-enrichment) for details.
  -  Added support for installing {{site.data.keyword.icp4dfull}} on Red Hat OpenShift.

Issues resolved in {{site.data.keyword.discovery-data_short}} offerings purchased on or after August 30, 2019:

-  During an active web crawl, if you add an enrichment, then click the **Recrawl collection** button on the **Activity** page, the collection will stop processing. If the collection does not return to a Syncing state on its own, clicking the **Recrawl collection** button an additional time might be required.
-  While training a collection in the tooling , if you rate the relevancy of a result (for example, as`Relevant`), then switch to the opposite rating (`Not relevant`), the page may go blank. To restore the page, refresh the browser. Your updated rating will be retained.
-  Chinese, Japanese, and Korean language Microsoft Word, Excel, and PowerPoint documents will not display correctly in the index or the Smart Document Understanding editor.
-  If you upload a zip, gzip, or tar file to your collection, and that file contains multiple files/file types supported by Smart Document Understanding (PDF, Word, Excel, PowerPoint, PNG, TIFF, JPEG), only one of the files in that zip, gzip, or tar file will be available for training in the SDU editor (unless the SDU document limit has already been met). All of the documents will be available in the index. Unzip the file before uploading to avoid this issue.
-  Query expansion and autocomplete return the wrong error code when the `collection_id` is invalid. Query expansion will return a `500` error code instead of a `404`. Autocomplete will return a `400` when the `collection_id` is invalid and the `prefix` parameter isn’t set. It should also return a `404`.
-  When crawling Microsoft SharePoint 2019 collections, only HTML documents will be crawled and indexed. This is a SharePoint issue with how it processes mime-types. See this Microsoft [blog post](https://blog.stefan-gossner.com/2018/11/30/common-issue-sp2019-items-in-document-libraries-are-downloaded-with-mime-type-application-octet-stream-rather-than-the-accurate-one/) for a workaround.
-  If you delete an installation of the {{site.data.keyword.discovery-data_short}} add-on, the instance will not uninstall completely and your re-installation will fail. See the {{site.data.keyword.discovery-data_short}} Readme for post-cleanup steps.
-  If a JSON document that contains nested JSON objects is ingested, the nested JSON will be indexed as a JSON string.    

### 2.0.0, General Availability (GA) release, 28 June 2019
{: #28jun2019}

The {{site.data.keyword.discovery-data_long}} service brings the cognitive capabilities of {{site.data.keyword.discoveryfull}} to the {{site.data.keyword.icp4dfull}} platform.