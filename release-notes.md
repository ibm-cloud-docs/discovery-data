---

copyright:
  years: 2019, 2021
lastupdated: "2021-07-27"

keywords: release notes

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

The release notes provide information about changes to {{site.data.keyword.discoveryfull}} since the previous release.
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

Find software release information for your deployment type:

- [![IBM Cloud only](images/ibm-cloud.png) {{site.data.keyword.cloud_notm}} releases](#rn-cloud)
- [![Cloud Pak for Data only](images/desktop.png) {{site.data.keyword.discovery-data_short}} releases](#rn-cpd)

See [Known issues](/docs/discovery-data?topic=discovery-data-known-issues) for the list of {{site.data.keyword.discoveryfull}} known issues.

## ![IBM Cloud only](images/ibm-cloud.png) {{site.data.keyword.cloud_notm}} releases
{: #rn-cloud}

The following new features and changes are available for managed deployments. 

For more information about software releases for installed deployments, see [{{site.data.keyword.discovery-data_short}} releases](#rn-cpd).

### ![IBM Cloud only](images/ibm-cloud.png) 27 July 2021
{: #27july2021}

- **Document size limit increase**: For Premium plan collections, you can now upload files that are up to 50 MB in size instead of 32 MB. For more information, see [Document limits](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-collections#collections-doc-limits).

### ![IBM Cloud only](images/ibm-cloud.png) 23 July 2021
{: #23july2021}

- **SharePoint Online data source update**: The connector now accepts any valid Azure Active Directory user ID syntax; the format of the user ID doesn't have to match the `<admin_user>@.onmicrosoft.com` syntax. For more information, see [Microsoft SharePoint Online](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cloud).

### ![IBM Cloud only](images/ibm-cloud.png) 16 July 2021
{: #16july2021}

- **Web crawl supports crawling dynamic websites**: The web crawler now can crawl dynamic websites that use JavaScript to render content. If you enable this beta feature, the time it takes to crawl the site increases. For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cloud).

### ![IBM Cloud only](images/ibm-cloud.png) 23 June 2021
{: #23june2021}

- **Introducing the Plus plan!**: Use the new Plus plan and its associated 30-day free trial to explore new features and a simpler way to build that is available with the latest version of the product. Currently, the Plus plan is available from the Dallas location. For more information, see [Getting the most from {{site.data.keyword.discoveryshort}}](/docs/discovery-data?topic=discovery-data-version-choose).
- **Lite and Advanced plans are no longer offered**: You cannot create new service instances that use the Lite or Advanced plan types in the Dallas location. Any existing Lite and Advanced plans continue to function properly and continue to be supported. You can upgrade from a Lite plan to an Advanced plan.

### ![IBM Cloud only](images/ibm-cloud.png) Endpoint deprecation reminder
{: #6apr2021}

- **Service API endpoint change**: As part of work done to fully support Identity and Access Management (IAM) authentication, the endpoint that you use to access your {{site.data.keyword.discoveryshort}} service programmatically is changing. The old endpoint URLs are deprecated and **will be retired on 26 May 2021**. Update your API calls to use the new URLs.

  The pattern for the endpoint URL changed from `gateway-{location}.watsonplatform.net/discovery/api/` to `api.{location}.discovery.watson.cloud.ibm.com/`. The domain, location, and offering identifier are different in the new endpoint. For more information, see [Updating endpoint URLs from watsonplatform.net](/docs/watson?topic=watson-endpoint-change){: external}.

  If your service instance API credentials use the old endpoint, create a new credential and start using it today. After you update your custom applications to use the new credential, you can delete the old one.

### ![IBM Cloud only](images/ibm-cloud.png) 19 March 2021
{: #19mar2021}

- You can use the Web crawl collection type to connect to content that is stored on an internal company website. For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cloud).

### ![IBM Cloud only](images/ibm-cloud.png) 4 March 2021
{: #4mar2021}

- Upload collections now support dragging and dropping documents before and during document upload. For more information, see [Uploading data](/docs/discovery-data?topic=discovery-data-upload-data).
- You can view a list of collections that are connected to a particular gateway. For more information, see [Viewing collections connected to a gateway](/docs/discovery-data?topic=discovery-data-sources#gateway-connection).

### ![IBM Cloud only](images/ibm-cloud.png) 17 December 2020
{: #17dec2020}

- Each collection now displays the **Next sync scheduled for** date and time on the **Activity** tab of the **Manage collections** page.
- Released the beta feature FAQ extraction. FAQ extraction automatically extracts question-and-answer pairs from FAQ (frequently asked questions) documents and web pages so that your application returns more precise answers. For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction). For a statement explaining beta features, see [Beta features](/docs/discovery-data?topic=discovery-data-release-notes#beta-features).

### ![IBM Cloud only](images/ibm-cloud.png) 3 December 2020
{: #3dec2020}

- **Content Intelligence** added - You can now apply the **Contracts** enrichment to a **Document Retrieval** project when you create it. The Contracts enrichment can be used to classify contract terms, parties, effective dates and more within your documents. For more information, see [Document Retrieval for Contracts](/docs/discovery-data?topic=discovery-data-projects#doc-retrieval-contracts).

### ![IBM Cloud only](images/ibm-cloud.png) 10 November 2020
{: #10nov2020}

- **Box connector** added - Crawl Box systems. For more information, see [Box](/docs/discovery-data?topic=discovery-data-sources#connectboxpublic).
- **SharePoint 2016 On-Premise connector** added - Crawl SharePoint 2016 On-Premise systems. For more information, see [SharePoint 2016 On-Premise](/docs/discovery-data?topic=discovery-data-connector-sharepoint-onprem-cloud).

### ![IBM Cloud only](images/ibm-cloud.png) 30 October 2020
{: #30oct2020}

- Added basic support for Bosnian, Croatian, Hindi, and Serbian. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
- Released the beta feature Patterns enrichment, which uses pattern induction to help you teach {{site.data.keyword.discoveryshort}} to recognize patterns in your data. Pattern induction generates extraction patterns from the examples you specify. After you specify a small number of examples, {{site.data.keyword.discoveryshort}} will suggest additional rules that you verify to complete the pattern. You can use pattern induction as an enrichment or to create a facet. For more information, see [Patterns](/docs/discovery-data?topic=discovery-data-domain#patterns) and [Creating a facet by identifying a pattern](/docs/discovery-data?topic=discovery-data-facets#facetpattern). For a statement explaining beta features, see [Beta features](/docs/discovery-data?topic=discovery-data-release-notes#beta-features).

  Changes made in this release:

- In new **Document Retrieval** projects, the `suggested refinements` query setting is now set to `false` by default. It was previously set to `true`.

### ![IBM Cloud only](images/ibm-cloud.png) 14 September 2020
{: #14sept2020}

- A new pre-trained model is available in Smart Document Understanding for Document Retrieval projects. This model is ideal if you need to extract data from documents that include a large number of tables. For more information, see [Identifying fields](/docs/discovery-data?topic=discovery-data-configuring-fields#identify-fields).

### ![IBM Cloud only](images/ibm-cloud.png) 16 July 2020
{: #16jul2020}

This release is available for Premium instances of {{site.data.keyword.discoveryshort}} on {{site.data.keyword.cloud_notm}} created after 16 July 2020. For Premium instances created before that date and for all Lite and Advanced plans, see [Getting started with Discovery](/docs/discovery?topic=discovery-getting-started).

- **IBM Cloud Premium** is generally available.
- New Project-based interface, which includes configurations optimized for three common use cases: Document Retrieval, Conversational Search, and Content Mining. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).
- Content Mining: This entirely new capability of Watson {{site.data.keyword.discoveryshort}} allows you to find insights in your data when you may not even know the question to ask. The powerful correlation tooling will help you unlock value from large unstructured data sets. For details, see [Using the Content Mining application](/docs/discovery-data?topic=discovery-data-contentminerapp).
- Tables as Answers: Snippets of text aren't helpful if they are found in a table, so {{site.data.keyword.discoveryshort}} instead returns a formatted table as an answer if your question is best answered by a table. For more information, see [Table retrieval](/docs/discovery-data?topic=discovery-data-query-parameters#table_retrieval).
- Dynamic Faceted Search: Underspecified queries are very common. Dynamic Faceted Search automatically categorizes your search results into intelligence facets without training by understanding how they are used in the sentences. See [Facets in Document retrieval projects](/docs/discovery-data?topic=discovery-data-facets#facetdr).
- Reusable Components: You no longer have to build a {{site.data.keyword.discoveryshort}} application from scratch. We now ship out of the box with reusable, open source, React components. As you configure your Discovery application, you are actually using the real components themselves. From there it is as simple as deploying to get a custom Discovery application. See [Building and deploying components](/docs/discovery-data?topic=discovery-data-deploy).
- Domain Vocabulary: You can build a facet for your users without a Dictionary. You can use Domain Vocabulary to build a powerful facet with our understanding of how the data is used in as little as 5 minutes.  See [Facets](/docs/discovery-data?topic=discovery-data-facets).
- Relevancy Training: You can train at a project level. {{site.data.keyword.discoveryshort}} ranks the best answer regardless of the data source/collection. See [Improving result relevance with training](/docs/discovery-data?topic=discovery-data-train).
- Spelling correction: {{site.data.keyword.discoveryshort}} has spelling suggestions built-in. See [Parameters descriptions](/docs/discovery-data?topic=discovery-data-query-reference#parameter-descriptions).
- Autocomplete: {{site.data.keyword.discoveryshort}} includes autocomplete (type-ahead) for searches, as well as a reusable component for providing this feature to your end users.
- Language support: {{site.data.keyword.discoveryshort}} supports 12 additional languages. For the complete list, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

  The following features are not available in this release:

- Deduplication is not available in this release.
- Anomaly Detection is not offered.
- Watson Discovery News is no longer included.
- Several Watson Natural Language Understanding enrichments are not available at this time (Entity extraction, Relation extraction, Keyword extraction, Category classification, Concept tagging, Semantic Role extraction, Sentiment analysis, Emotion analysis)
- The SharePoint 2016 On-Premise and Box data sources are not available at this time.

## ![Cloud Pak for Data only](images/desktop.png) {{site.data.keyword.discovery-data_short}} releases
{: #rn-cpd}

The following new features and changes are available for installed deployments. 

For more information about software releases for managed deployments, see [{{site.data.keyword.cloud_notm}} releases](#rn-cloud).

### ![Cloud Pak for Data only](images/desktop.png) 4 release, 13 July 2021
{: #13july2021}

{{site.data.keyword.discovery-data_short}} 4 is available.

This release is supported on {{site.data.keyword.icp4dfull}} 4.0.0.

- **Service name change**: The new name is {{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}}.
- **New Smart Document Understanding (SDU) predefined model**: When you identify fields, instead of annotating documents with the SDU tool, you can choose to use a pretrained model. The pretrained model applies a non-customizable model that automatically extracts text and identifies tables, lists, and sections.
- **Enabling contract analysis is easier**: To enable the Contracts enrichment that recognizes and tags contract-related concepts in your data, you can choose to create a Document Retrieval project type, and then select **Apply contracts enrichment**. You no longer need to use an installation override YAML file to enable it. This change also means that you can choose which Document Retrieval projects use the Contracts enrichment; it is not applied to all Document Retrieval projects automatically.
- Many data source improvements were made:

  - **New LDAP directory data source**: Connect to data that is stored in an external directory that supports the Lightweight Directory Access Protocol (LDAP), such as a corporate email directory. As the directory data is added to your collection, {{site.data.keyword.discoveryshort}} interprets and stores key attributes of each record, such as department and location information. Later, you can find relevant records by filtering on these attribute categories. For more information, see [LDAP directory](/docs/discovery-data?topic=discovery-data-connector-ldap-cp4d).
  - **Simplified SharePoint OnPrem connection process**: The steps you follow to connect to a SharePoint instance that is hosted on-premises were simplified. You no longer need to deploy a web services package on the SharePoint server before you can connect to the SharePoint OnPrem data source. For more information, see [SharePoint OnPrem](/docs/discovery-data?topic=discovery-data-connector-sharepoint-onprem-cp4d).
  - **Salesforce proxy support**: You can now connect to a Salesforce data source when using a proxy server. For more information, see [Salesforce](/docs/discovery-data?topic=discovery-data-connector-salesforce-cp4d).

- **Custom connector improvements**: Support was added for the following features:

  - Optical character recognition (OCR)
  - Document-level security

  For more information about the custom connector, see [Building a Cloud Pak for Data custom connector](/docs/discovery-data?topic=discovery-data-build-connector).

- Support for *Dynamic Faceted Search* and its associated `suggested_refinements` API query parameter was removed.

### ![Cloud Pak for Data only](images/desktop.png) 2.2.1 release, 26 February 2021
{: #26feb2021}

IBM Watson™ Discovery for IBM Cloud Pak for Data version 2.2.1 is available.

- {{site.data.keyword.discovery-data_short}} supports an in-place upgrade from version 2.2.0 to 2.2.1 so that you do not need to manually uninstall an earlier version and then install the latest version of the service. For more information, see [Upgrading Discovery for Cloud Pak for Data](/docs/discovery-data?topic=discovery-data-install#upgrade-discovery).
- You can now download the custom connector SDK package from your {{site.data.keyword.discovery-data_short}} cluster, instead of retrieving the images and the SDK package from the Docker registry. For more information, see [Downloading the custom-crawler-docs.zip file in Discovery 2.2.1 and later](/docs/discovery-data?topic=discovery-data-connector-dev#download-ccs-zip).
- `Invoices` and `Purchase orders` models can no longer be enabled in the tooling. If you need these models, please contact [IBM Cloud Support](https://cloud.ibm.com/unifiedsupport/supportcenter){: external} to obtain instructions for enabling these models.
- In a `Document Retrieval` project that has the `Contracts` enrichment applied, tables are not included inside the `contracts` field, as they were previously in projects that had the `Contracts` enrichment enabled. Tables will continue to be included in a separate `tables` field when the `Table Understanding` enrichment is applied.
- Support for connecting to the following database data source versions was removed because version support was ended by the vendors:

  - Oracle Database 11g: Vendor support ended on 31 December 2020
  - Postgres 9.5: Vendor support ended on 11 February 2021

### ![Cloud Pak for Data only](images/desktop.png) 2.2.0 release, 8 December 2020
 {: #8dec2020}

IBM Watson™ Discovery for IBM Cloud Pak for Data version 2.2 is available.

{{site.data.keyword.discovery-data_short}} now works with I{{site.data.keyword.icp4dfull}} 3.5.

- Added support for attachments in the Notes data source. For more information, see [Notes](/docs/discovery-data?topic=discovery-data-collection-types#connectnotes)
- You can specify the exact time that you would like your crawls to run for any data source, giving you the flexibility to run them at the times you prefer. For more information, see [Configuring Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types).
- You can now create Facet groups in a Content Miner application. For more information, see [Facet analysis pane](/docs/discovery-data?topic=discovery-data-contentminerapp#cmofap).
- Added the option to create your own custom crawler plug-in. For more information, see [Building a Cloud Pak for Data crawler plug-in](/docs/discovery-data?topic=discovery-data-crawler-plugin-build) **Note:** Any custom code used with Watson Discovery is the responsibility of the developer and is not covered by IBM support.
- Dynamic Facets are no longer enabled by default in Document Retrieval projects.

### ![Cloud Pak for Data only](images/desktop.png) 2.1.4 release, 2 September 2020
{: #2sept2020}

{{site.data.keyword.discovery-data_long}} version 2.1.4 is available.

- **Notes connector** added - Crawl Notes version 9.0.1 systems. For more information, see [Notes connector](/docs/discovery-data?topic=discovery-data-collection-types#connectnotes).
- Multiple improvements to several connectors:

  - Added the **Enable proxy settings** option to the [Box](/docs/discovery-data?topic=discovery-data-collection-types#connectbox), [Microsoft SharePoint Online](/docs/discovery-data?topic=discovery-data-collection-types#connectsp), and [Microsoft SharePoint OnPrem](/docs/discovery-data?topic=discovery-data-collection-types#connectsp_op) connectors.
  - Added support for multiple tables and the Row filter option to the [Database connector](/docs/discovery-data?topic=discovery-data-collection-types#databaseconnect).
  - Added three new authentication types to the [Web crawler](/docs/discovery-data?topic=discovery-data-collection-types#connectwebcrawl): Basic authentication, NTLM authentication, and FORM authentication.
- You can now monitor the usage of the Analyze API using the tooling. For more information, see [Monitoring usage](/docs/discovery-data?topic=discovery-data-analyzeapi#api-usage).


### ![Cloud Pak for Data only](images/desktop.png) 2.1.3 release, 19 June 2020
{: #19jun2020}

{{site.data.keyword.discovery-data_long}} version 2.1.3 is available.

{{site.data.keyword.discovery-data_short}} now works with {{site.data.keyword.icp4dfull}} 3.0.1.

- Added basic support for Finnish and Hebrew. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
- The Analyze endpoint, which supports stateless document ingestion workflows. For details, see the [Analyze API](/docs/discovery-data?topic=discovery-data-analyzeapi). The Analyze API supports JSON documents only. Use of the Analyze API affects license usage, please reference the latest [license information](http://www.ibm.com/software/sla/sladb.nsf/searchlis/?searchview&searchorder=4&searchmax=0&query=(watson+discovery){: external}.
- The content mining application includes two new options: [Cyclic time scale](/docs/discovery-data?topic=discovery-data-contentminerapp#cmotsdb) on the Time series dashboard, and the [Contextual view](/docs/discovery-data?topic=discovery-data-contentminerapp#contextual-view) tab.
- For **Content Mining** projects only, the **Improve and customize** page includes a shortcut: the **Launch application** button. Previously, you were required to open the **Integrate and deploy** page, select the **Launch application** tab, and click the **Launch** button.
- The segment limit when splitting documents has been increased to 1,000. For details, see [Split documents to make query results more succinct](/docs/discovery-data?topic=discovery-data-split-documents).
- The [Filenet connector](/docs/discovery-data?topic=discovery-data-collection-types#filenet-connect) has document level security.
- You can specify up to 1,000 curations. For details about this beta feature, see [Curations](/docs/discovery-data?topic=discovery-data-train#curations).

The following issues were resolved in the 2.1.3 release:

- In versions 2.1.2, 2.1.1, and 2.1.0, PNG, TIFF, and JPG individual image files are not scanned, and no text is extracted from those files. PNG, TIFF, and JPEG images embedded in PDF, Word, PowerPoint, and Excel files are also not scanned, and no text is extracted from those image files.

### ![Cloud Pak for Data only](images/desktop.png) 2.1.2 release, 31 Mar 2020
{: #31mar2020}

{{site.data.keyword.discovery-data_long}} version 2.1.2 is available.

- **IBM FileNet connector** added - Crawl IBM FileNet systems. For more information, see [FileNet connector](/docs/services/discovery-data?topic=discovery-data-collection-types#filenet-connect). 
- Added basic support for Swedish, Norwegian (Bokma&#778;l and Nynorsk), and Danish. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
- The [Advanced Rule models enrichment](/docs/discovery-data?topic=discovery-data-domain#advanced-rules) is now GA.
- Several **enhancements to the tooling**; including improvements to the navigation, messages, and status updates.
- You can now view your search results in a document preview for the following source documents: PDF, Word, PowerPoint, Excel, and all image files. See [supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes) for the list of image files. This view makes it easier for you to see search results as highlighted passages within the text of the original document, making the context clearer.
- The [Web Crawl connector](/docs/services/discovery-data?topic=discovery-data-collection-types#connectwebcrawl) has proxy support. 
- Running a query with an empty `aggregations` parameter returns zero aggregations in the response.
- Support for connecting to the following database data source version was removed because version support was ended by the vendor:

  - Postgres 9.4: Vendor support ended on 13 February 2020
  
The following issues were resolved in the 2.1.2 release:

- When installing {{site.data.keyword.discovery-data_short}} on OpenShift, the `ranker-rest` service might intermittently fail to startup, due to an incompatible jar in the `classpath`.
- When you upload documents to a collection with existing documents, a `Documents uploaded!` message displays on the **Activity** page, but no further processing status displays until the number of documents increases.
- Running a query with an empty `aggregations` parameter returns an empty aggregations array.
- Deprovisioning a {{site.data.keyword.discovery-data_long}} Instance will not delete the underlying data. Delete the collections and documents manually.
  
### ![Cloud Pak for Data only](images/desktop.png) 2.1.1 release, 24 Jan 2020
{: #24jan2020}

{{site.data.keyword.discovery-data_long}} version 2.1.1 is available.

The following issues were resolved in the 2.1.1 release:

- In Document Retrieval project types, when you perform an empty search, and the search results source is set to `passages,` the query results will display `excerpt unavailable` in the Project workspace.
- When visiting the Storybook links on the Integrate and deploy page, the links do not go to the correct location. Please visit [Storybook](https://watson-developer-cloud.github.io/discovery-components/storybook){: external} instead to view documentation.
- If you are using Smart Document Understanding, two variables no longer need to be set during installation or reinstallation. For more information, see [Environment variable settings for Smart Document Understanding](/docs/discovery-data?topic=discovery-data-troubleshoot#troubleshoot-sdu).
- Discovery for Content Intelligence and Table Understanding enrichments are configured out of the box to be applied on a field named `html`. When a user uploads a JSON document without a root-level field named `html`, these enrichments will not yield results in the index. To run the enrichments on this kind of JSON documents, users must re-configure the enrichments to run on an existing field (or fields) in the JSON document.

### ![Cloud Pak for Data only](images/desktop.png) 2.1.0 release, 27 Nov 2019
{: #27nov2019}

{{site.data.keyword.discovery-data_long}} version 2.1.0 is available.

{{site.data.keyword.discovery-data_short}} now works with {{site.data.keyword.icp4dfull}} 2.5.0.0.

Changes made in this release:

- New **Project** based interface - Test your application like an end-user would with the **Document retrieval**, **Conversational Search**, and **Content Mining** project types. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).
- **Content Mining** - Build an end user interface for extracting insights proactively from your entire corpus. For more information, see [Using the Content Mining application](/docs/discovery-data?topic=discovery-data-contentminerapp).
- **Content Intelligence** - Optional add-on to enrich your documents with pre-built domain knowledge for Contracts. For more information, see [Document Retrieval for Contracts](/docs/discovery-data?topic=discovery-data-projects#doc-retrieval-contracts).
- **Reusable components** to quickly build your application using Discovery. We ship an autocomplete, rich preview, results and facets component. For more information, see [Building and deploying components](/docs/discovery-data?topic=discovery-data-deploy).
- **Additional Language support** - Basic support for Czech, Slovak, Russian, Polish and Romanian. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
- **Built-in table understanding** - Extract tables from your documents without training, and optionally return tables as answers to natural language queries. For more information, see [Understanding tables](/docs/discovery-data?topic=discovery-data-understanding_tables). 
- **Connector SDK** - Build custom connectors your Discovery users can use to build their own applications. For more information, see [Building and implementing a custom connector](/docs/discovery-data?topic=discovery-data-build-connector).
- **Sample Project** - The sample project is preloaded with data so you can learn about Discovery. For more information, see [Getting started with Watson Discovery for {{site.data.keyword.icp4dfull_notm}}](/docs/discovery-data?topic=discovery-data-getting-started).
- **Passage retrieval** - Will return the most relevant passages from your documents, plus you can specify the number of passages returned per document. See [passages](/docs/discovery-data?topic=discovery-data-query-parameters#passages).
- **Project level querying and relevancy training** - Query multiple collections at once including relevance training.
- Improvements and additional options to the **Web crawl connector** - For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-collection-types#connectwebcrawl).
- **Local File System connector** added - Crawl Linux or other file systems. For more information, see [Local file system](/docs/discovery-data?topic=discovery-data-collection-types#localfilesystemconnect)
- **Dynamic Facets** - Automatically generate facets based on the understanding of your data. For more information, see [Facets](/docs/discovery-data?topic=discovery-data-facets).
- **Dictionary suggestions** - Dictionary terms will be suggested to you based on your content. For more information, see [Dictionary](/docs/discovery-data?topic=discovery-data-domain#dictionary).
- **Curations** (beta) - Specify a particular result for a given query. For more information, see the [API reference](https://{DomainName}/apidocs/discovery/discovery-data#createcuration){: external}.

### ![Cloud Pak for Data only](images/desktop.png) 2.0.1 release, 30 August 2019
{: #30aug2019}

{{site.data.keyword.discovery-data_long}} version 2.0.1 is available.

{{site.data.keyword.discovery-data_short}} now works with {{site.data.keyword.icp4dfull}} 2.1.0.1. 

- Added the Windows File System and Database connectors.  For more information, see [Database connector](/docs/discovery-data?topic=discovery-data-collection-types#databaseconnect) and [Windows File System connector](/docs/discovery-data?topic=discovery-data-collection-types#windowsfilesystemconnect).
- Added support for Traditional Chinese. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
- Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.discovery-data_long}} offerings purchased on or after August 30, 2019. FISMA support is also available to those who purchased the June 28, 2019 version and upgrade to the August 30, 2019 version. {{site.data.keyword.discovery-data_long}} is FISMA High Ready.
- Released the Classifier enrichment. For more information, see [Classifier](/docs/discovery-data?topic=discovery-data-domain#classifier).
- Added support for installing {{site.data.keyword.icp4dfull}} on Red Hat OpenShift.

The following issues were resolved in {{site.data.keyword.discovery-data_short}} offerings purchased on or after August 30, 2019:

- During an active web crawl, if you add an enrichment, then click the **Recrawl collection** button on the **Activity** page, the collection will stop processing. If the collection does not return to a Syncing state on its own, clicking the **Recrawl collection** button an additional time might be required.
- While training a collection in the tooling , if you rate the relevancy of a result (for example, as`Relevant`), then switch to the opposite rating (`Not relevant`), the page may go blank. To restore the page, refresh the browser. Your updated rating will be retained.
- Chinese, Japanese, and Korean language Microsoft Word, Excel, and PowerPoint documents will not display correctly in the index or the Smart Document Understanding editor.
- If you upload a zip, gzip, or tar file to your collection, and that file contains multiple files/file types supported by Smart Document Understanding (PDF, Word, Excel, PowerPoint, PNG, TIFF, JPEG), only one of the files in that zip, gzip, or tar file will be available for training in the SDU editor (unless the SDU document limit has already been met). All of the documents will be available in the index. Unzip the file before uploading to avoid this issue.
- Query expansion and autocomplete return the wrong error code when the `collection_id` is invalid. Query expansion will return a `500` error code instead of a `404`. Autocomplete will return a `400` when the `collection_id` is invalid and the `prefix` parameter isn’t set. It should also return a `404`.
- When crawling Microsoft SharePoint 2019 collections, only HTML documents will be crawled and indexed. This is a SharePoint issue with how it processes mime-types. See this Microsoft [blog post](https://blog.stefan-gossner.com/2018/11/30/common-issue-sp2019-items-in-document-libraries-are-downloaded-with-mime-type-application-octet-stream-rather-than-the-accurate-one/) for a workaround.
- If you delete an installation of the {{site.data.keyword.discovery-data_short}} add-on, the instance will not uninstall completely and your re-installation will fail. See the {{site.data.keyword.discovery-data_short}} Readme for post-cleanup steps.
- If a JSON document that contains nested JSON objects is ingested, the nested JSON will be indexed as a JSON string.    

### ![Cloud Pak for Data only](images/desktop.png) 2.0.0, General Availability (GA) release, 28 June 2019
{: #28jun2019}

The {{site.data.keyword.discovery-data_long}} service brings the cognitive capabilities of {{site.data.keyword.discoveryfull}} to the {{site.data.keyword.icp4dfull}} platform.