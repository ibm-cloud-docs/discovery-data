---

copyright:
  years: 2019, 2021
lastupdated: "2021-11-15"

keywords: discovery release notes,discovery cloud pak for data release notes,watson discovery release notes,what's new,new features,improvements,change log,changelog

subcollection: discovery-data
content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.discoveryshort}} 
{: #release-notes}

The release notes provide information about changes to {{site.data.keyword.discoveryfull}} since the previous release.
{: shortdesc}

Find software release information for your deployment type:

- [![IBM Cloud only](images/ibm-cloud.png) {{site.data.keyword.cloud_notm}} releases](#rn-cloud)
- [![Cloud Pak for Data only](images/desktop.png) {{site.data.keyword.discovery-data_short}} releases](#rn-cpd)

See [Known issues](/docs/discovery-data?topic=discovery-data-known-issues) for the list of {{site.data.keyword.discoveryfull}} known issues.

## Service API Versioning
{: #apiversioning}

API requests require a version parameter that takes a date in the format `version=YYYY-MM-DD`. Whenever we change the API in a backwards-incompatible way, we release a new minor version of the API.

Send the version parameter with every API request. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.

The current version is `2020-08-30`.

## Beta features
{: #beta-features}

IBM releases services, features, and language support for your evaluation that are classified as beta. These features might be unstable, might change frequently, and might be discontinued with short notice. Beta features also might not provide the same level of performance or compatibility that generally available features provide and are not intended for use in a production environment.

## ![IBM Cloud only](images/ibm-cloud.png) Discovery for {{site.data.keyword.cloud_notm}} releases
{: #rn-cloud}

The following new features and changes are available for managed deployments of {{site.data.keyword.cloud_notm}}.

### ![IBM Cloud only](images/ibm-cloud.png) 11 November 2021
{: #discovery-11november2021}
{: release-note}

New locations for Enterprise plan now available
:   The Enterprise plan is available from the Frankfurt, London, Sydney, and Tokyo locations in addition to the Dallas location. Scale and secure your {{site.data.keyword.discoveryshort}} application with enterprise-grade support and performance and address more use cases including contract analysis and content mining to explore insights across documents. For more information, see [Discovery pricing plans](/docs/discovery-data?topic=discovery-data-pricing-plans).

### ![IBM Cloud only](images/ibm-cloud.png) 3 November 2021
{: #discovery-3november2021}
{: release-note}

<!--4.0.4-0.5-->

New Enterprise plan
:   Scale and secure your {{site.data.keyword.discoveryshort}} application with enterprise-grade support and performance and address more use cases, including contract analysis and content mining to explore insights across documents. Currently, the Enterprise plan is available only from the Dallas location. For more information, see [Discovery pricing plans](/docs/discovery-data?topic=discovery-data-pricing-plans).

New beta entity extractor enrichment
:   The *Extract entities* enrichment brings the powerful ability to build a custom type system into {{site.data.keyword.discoveryshort}}. Use the tool to label entity examples within your industry data to build a machine learning model that {{site.data.keyword.discoveryshort}} can use to recognize meaningful terms for your business. Currently, this beta feature is available for English-language projects that are created in Premium plan service instances only. For more information, see [Customizing the terms that Discovery can recognize](/docs/discovery-data?topic=discovery-data-entity-extractor).

New *Helpful links* tab
:   The home page includes a *Helpful links* tab that has quick links to documentation, a community site, and other resources. 

Improved field selection choices
:   When you apply an enrichment to a field or choose a field to use as the source for a facet, the fields that are displayed for you to choose from now include only fields that are valid choices. Previously, the list included fields that were not valid choices.

### ![IBM Cloud only](images/ibm-cloud.png) 14 October 2021
{: #discovery-14october2021}
{: release-note}

<!--4.0.3-3.2-->

New Discovery home page
:   A new home page is displayed when you start Discovery and gives you quick access to a product overview video, and tours. You can collapse the home page welcome banner to see more projects.

New plan usage section 
:   Stay informed about plan usage and check your usage against the limits for your plan type from the *Plan limits and usage* page. From the product page header, click the user icon ![User icon](images/user-icon.png). The *Usage* section shows a short summary. Click **View all** to see usage information for all of the plan limit categories.

Change to spelling settings in Search
:   The spelling correction setting changed from being enabled automatically in new projects to being disabled by default. If you want to alert users when they misspell a term in their query, turn on *Spelling suggestions*. For more information, see [Customizing the search bar](/docs/discovery-data?topic=discovery-data-search-bar).

Improved **Guided tours** availability
:    The **Guided tours** button is now available from the product page header, which make them accessible from anywhere. Previously, it was available from the *My Projects* page only.

### ![IBM Cloud only](images/ibm-cloud.png) 1 October 2021
{: #discovery-1october2021}
{: release-note}

Change to Lite and Advanced plans in all locations
:   Lite and Advanced plans are discontinued. You cannot create **new** service instances that use the Lite or Advanced plan types in the Dallas, Frankfurt, London, Seoul, Sydney, Tokyo, and Washington DC locations. Any existing Lite and Advanced plans continue to function properly and continue to be supported. You can upgrade from a Lite plan to an Advanced plan. Use the new Plus plan and its associated 30-day free trial to explore new features and a simpler way to build that is available with the latest version of the product.

### ![IBM Cloud only](images/ibm-cloud.png) 24 September 2021
{: #discovery-24september2021}
{: release-note}

<!--4.0.3-1.2-->

New scoring for NLU enrichments
:   Relevance and confidence scores are displayed for NLU enrichments that are returned by search. For example, when you open the JSON view of the document preview from a query result, you can see confidence scores for Entities mentions and relevance scores for Keyword mentions.

### ![IBM Cloud only](images/ibm-cloud.png) 9 September 2021
{: #discovery-9september2021}
{: release-note}

New location for Plus plan
:   The Plus plan is now available from the Sydney location. Use the new Plus plan and its associated 30-day free trial to explore new features and a simpler way to build that is available with the latest version of the product. For more information, see [Getting the most from {{site.data.keyword.discoveryshort}}](/docs/discovery-data?topic=discovery-data-version-choose).

Change to Lite and Advanced plans in most locations
:   Lite and Advanced plans are discontinued. You cannot create **new** service instances that use the Lite or Advanced plan types in the Dallas, Frankfurt, London, Sydney, Tokyo, or Washington DC locations. Any existing Lite and Advanced plans continue to function properly and continue to be supported. You can upgrade from a Lite plan to an Advanced plan.

### ![IBM Cloud only](images/ibm-cloud.png) 26 August 2021
{: #discovery-26august2021}
{: release-note}

New locations for the Plus plan
:   The Plus plan is now available from the London and Washington DC locations, in addition to Dallas, Frankfurt, and Tokyo.

Change to Lite and Advanced plans in some locations
:   You cannot create **new** service instances that use the Lite or Advanced plan types in the Dallas, Frankfurt, London, Tokyo, or Washington DC locations. Any existing Lite and Advanced plans continue to function properly and continue to be supported. You can upgrade from a Lite plan to an Advanced plan.

New answer finding feature
:   Answer finding is now generally available for managed deployments. Use answer finding when you want to return a concise answer to a question. For more information, see [Answer finding](/docs/discovery-data?topic=discovery-data-query-parameters#answer-finding).

### ![IBM Cloud only](images/ibm-cloud.png) 16 August 2021
{: #discovery-16august2021}
{: release-note}

New locations for the Plus plan
:   The Plus plan is now available from the Frankfurt and Tokyo locations, in addition to Dallas.

Change to Lite and Advanced plans in some locations
:   Lite and Advanced plans are no longer offered. You cannot create **new** service instances that use the Lite or Advanced plan types in the Dallas, Frankfurt, or Tokyo locations. Any existing Lite and Advanced plans continue to function properly and continue to be supported. You can upgrade from a Lite plan to an Advanced plan.

### ![IBM Cloud only](images/ibm-cloud.png) 27 July 2021
{: #discovery-27july2021}
{: release-note}

Improved document size limit
:   Document size limit is increased. For Premium plan collections, you can now upload files that are up to 50 MB in size instead of 32 MB. For more information, see [Document limits](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-collections#collections-doc-limits).

### ![IBM Cloud only](images/ibm-cloud.png) 23 July 2021
{: #discovery-23july2021}
{: release-note}

Improved SharePoint Online connector
:   The Microsoft SharePoint Online data source connector now accepts any valid Azure Active Directory user ID syntax; the format of the user ID doesn't need to match the `<admin_user>@.onmicrosoft.com` syntax. For more information, see [Microsoft SharePoint Online](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cloud).

### ![IBM Cloud only](images/ibm-cloud.png) 16 July 2021
{: #discovery-16july2021}
{: release-note}

New beta dynamic website web crawl
:   The Web crawler can now crawl dynamic websites that use JavaScript to render content. If you enable this beta feature, the time it takes to crawl the site increases. For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cloud).

### ![IBM Cloud only](images/ibm-cloud.png) 23 June 2021
{: #discovery-23june2021}
{: release-note}

New Plus plan
:   Use the new Plus plan and its associated 30-day free trial to explore new features and a simpler way to build that is available with the latest version of the product. Currently, the Plus plan is available from the Dallas location. For more information, see [Getting the most from {{site.data.keyword.discoveryshort}}](/docs/discovery-data?topic=discovery-data-version-choose).

Change to Lite and Advanced plans
:   Lite and Advanced plans are no longer offered. You cannot create **new** service instances that use the Lite or Advanced plan types in the Dallas location. Any existing Lite and Advanced plans continue to function properly and continue to be supported. You can upgrade from a Lite plan to an Advanced plan.

### ![IBM Cloud only](images/ibm-cloud.png) Endpoint deprecation reminder
{: #discovery-6april2021}
{: release-note}

Change to Discovery API endpoint
:   As part of work done to fully support Identity and Access Management (IAM) authentication, the endpoint that you use to access your {{site.data.keyword.discoveryshort}} service programmatically is changing. The old endpoint URLs are deprecated and **will be retired on 26 May 2021**. Update your API calls to use the new URLs.

    The pattern for the endpoint URL changed from `gateway-{location}.watsonplatform.net/discovery/api/` to `api.{location}.discovery.watson.cloud.ibm.com/`. The domain, location, and offering identifier are different in the new endpoint. For more information, see [Updating endpoint URLs from watsonplatform.net](/docs/watson?topic=watson-endpoint-change){: external}.

    If your service instance API credentials use the old endpoint, create a new credential and start using it today. After you update your custom applications to use the new credential, you can delete the old one.

### ![IBM Cloud only](images/ibm-cloud.png) 19 March 2021
{: #discovery-19march2021}
{: release-note}

Improved Web crawl connector
:   You can use the Web crawl collection type to connect to content that is stored on an internal company website. For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cloud).

### ![IBM Cloud only](images/ibm-cloud.png) 4 March 2021
{: #discovery-4march2021}
{: release-note}

New drag and drop feature when uploading
:   Upload collections now support dragging and dropping documents before and during document upload. For more information, see [Uploading data](/docs/discovery-data?topic=discovery-data-upload-data).

New list view for collections
:   You can view a list of collections that are connected to a particular gateway. For more information, see [Viewing collections connected to a gateway](/docs/discovery-data?topic=discovery-data-sources#gateway-connection).

### ![IBM Cloud only](images/ibm-cloud.png) 17 December 2020
{: #discovery-17december2020}
{: release-note}

Improved date and time display on Activity tab
:   Each collection now displays the **Next sync scheduled for** date and time on the **Activity** tab of the **Manage collections** page.

New beta FAQ extraction
:   Released the beta feature FAQ extraction. FAQ extraction automatically extracts question-and-answer pairs from FAQ (frequently asked questions) documents and web pages so that your application returns more precise answers. For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction). For a statement explaining beta features, see [Beta features](/docs/discovery-data?topic=discovery-data-release-notes#beta-features).

### ![IBM Cloud only](images/ibm-cloud.png) 3 December 2020
{: #discovery-3december2020}
{: release-note}

New Content Intelligence
:   You can now apply the **Contracts** enrichment to a **Document Retrieval** project when you create it. The Contracts enrichment can be used to classify contract terms, parties, effective dates and more within your documents. For more information, see [Document Retrieval for Contracts](/docs/discovery-data?topic=discovery-data-projects#doc-retrieval-contracts).

### ![IBM Cloud only](images/ibm-cloud.png) 10 November 2020
{: #discovery-10november2020}
{: release-note}

New Box connector
:   Crawl Box systems. For more information, see [Box](/docs/discovery-data?topic=discovery-data-sources#connectboxpublic).

New SharePoint 2016 On-Premise connector
:   Crawl SharePoint 2016 On-Premise systems. For more information, see [SharePoint 2016 On-Premise](/docs/discovery-data?topic=discovery-data-connector-sharepoint-onprem-cloud).

### ![IBM Cloud only](images/ibm-cloud.png) 30 October 2020
{: #discovery-30october2020}
{: release-note}

New language support for Bosnian, Croatian, Hindi, and Serbian
:   Basic language support now available for Bosnian, Croatian, Hindi, and Serbian. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

New beta Patterns enrichment
:   The beta release of Patterns enrichment uses pattern induction to help you teach {{site.data.keyword.discoveryshort}} to recognize patterns in your data. Pattern induction generates extraction patterns from the examples you specify. After you specify a small number of examples, {{site.data.keyword.discoveryshort}} will suggest additional rules that you verify to complete the pattern. You can use pattern induction as an enrichment or to create a facet. For more information, see [Patterns](/docs/discovery-data?topic=discovery-data-domain#patterns) and [Creating a facet by identifying a pattern](/docs/discovery-data?topic=discovery-data-facets#facetpattern). For a statement explaining beta features, see [Beta features](/docs/discovery-data?topic=discovery-data-release-notes#beta-features).


Change to Document Retrieval projects
:   In new **Document Retrieval** projects, the `suggested refinements` query setting is now set to `false` by default. It was previously set to `true`.

### ![IBM Cloud only](images/ibm-cloud.png) 14 September 2020
{: #discovery-14september2020}
{: release-note}

New pre-trained model for SDU
:   A new pre-trained model is available in Smart Document Understanding for Document Retrieval projects. This model is ideal if you need to extract data from documents that include a large number of tables. For more information, see [Identifying fields](/docs/discovery-data?topic=discovery-data-configuring-fields#identify-fields).

### ![IBM Cloud only](images/ibm-cloud.png) 30 August 2020
{: #discovery-30august2020}
{: release-note}

Update to API version
:   The current API version (v2) is now 2020-08-30. The following change was made with this version:

Change to 'options' object
:   The List enrichments method no longer returns the `options` object per enrichment. Use the Get enrichment method to return the `options` object for a single enrichment.

### ![IBM Cloud only](images/ibm-cloud.png) 16 July 2020
{: #discovery-16july2020}
{: release-note}

New release for Premium instances
:   This release is available for Premium instances of {{site.data.keyword.discoveryshort}} on {{site.data.keyword.cloud_notm}} created after 16 July 2020. For Premium instances created before that date and for all Lite and Advanced plans, see [Getting started with Discovery](/docs/discovery?topic=discovery-getting-started).

Change to **IBM Cloud Premium** 
:   The Premium plan is now generally available.

New Project-based interface
:   The project-based UI includes configurations optimized for three common use cases: Document Retrieval, Conversational Search, and Content Mining. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).

New Content Mining app
:   This entirely new capability of Watson {{site.data.keyword.discoveryshort}} allows you to find insights in your data when you may not even know the question to ask. The powerful correlation tooling will help you unlock value from large unstructured data sets. For details, see [Using the Content Mining application](/docs/discovery-data?topic=discovery-data-contentminerapp).

New tables as answers
:   Snippets of text aren't helpful if they are found in a table, so {{site.data.keyword.discoveryshort}} instead returns a formatted table as an answer if your question is best answered by a table. For more information, see [Table retrieval](/docs/discovery-data?topic=discovery-data-query-parameters#table_retrieval).

New dynamic faceted search feature
:   Underspecified queries are common. Dynamic Faceted Search automatically categorizes your search results into intelligence facets without training by understanding how they are used in the sentences. See [Facets in Document retrieval projects](/docs/discovery-data?topic=discovery-data-facets#facetdr).

New reusable components
:   You no longer need to build a {{site.data.keyword.discoveryshort}} application from scratch. We now ship out of the box with reusable, open source, React components. As you configure your Discovery application, you are using the real components. From there you simply deploy to get a custom Discovery application. See [Building and deploying components](/docs/discovery-data?topic=discovery-data-deploy).

New Domain Vocabulary feature
:   You can build a facet for your users without a Dictionary. Use Domain Vocabulary to build a powerful facet with our understanding of how the data is used in as little as 5 minutes.  See [Facets](/docs/discovery-data?topic=discovery-data-facets).

New relevancy training
:   You can train at a project level. {{site.data.keyword.discoveryshort}} ranks the best answer regardless of the data source/collection. See [Improving result relevance with training](/docs/discovery-data?topic=discovery-data-train).

New built-in spelling corrector
:   {{site.data.keyword.discoveryshort}} has spelling suggestions built in. See [Parameters descriptions](/docs/discovery-data?topic=discovery-data-query-reference#parameter-descriptions).

Improved Autocomplete
:   {{site.data.keyword.discoveryshort}} includes autocomplete (type-ahead) for searches, as well as a reusable component for providing this feature to your end users.

New support for 12 languages
:   Language support for {{site.data.keyword.discoveryshort}} is now available in 12 additional languages. For the complete list, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

Current API version
:   The API version (v2) is `2019-11-29`.

Change to features in this release
:   Deduplication is not available in this release.
:   Anomaly Detection is not offered.
:   Watson Discovery News is no longer included.
:   Several Watson Natural Language Understanding enrichments are not available at this time (Entity extraction, Relation extraction, Keyword extraction, Category classification, Concept tagging, Semantic Role extraction, Sentiment analysis, Emotion analysis)
:   The SharePoint 2016 On-Premise and Box data sources are not available at this time.

## ![Cloud Pak for Data only](images/desktop.png) {{site.data.keyword.discovery-data_short}} releases
{: #rn-cpd}

The following new features and changes in each release and update are available for installed deployments of {{site.data.keyword.discovery-data_short}}. 

### ![Cloud Pak for Data only](images/desktop.png) 4.0.2 release, 5 October 2021
{: #discovery-data-5october2021}

{{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.2 is available.

Support for newer platform software
:   {{site.data.keyword.icp4dfull}} 4.0.2 can be installed on {{site.data.keyword.openshiftlong}} 4.8.

New scoring for NLU enrichments
:   Relevance and confidence scores are displayed for NLU enrichments that are returned by search. For example, when you open the JSON view of the document preview from a query result, you can see confidence scores for Entities mentions and relevance scores for Keyword mentions.

Improved Web crawl
:   The *Web crawl* data source supports more customization options, including the ability to ignore a site's robots.txt file. For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cp4d).

New upgrade support
:   The 4.0.2 release supports in-place upgrade from {{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}} 4.0.0. For more information, see [Upgrading Watson Discovery to a newer 4.0 refresh](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=discovery-upgrading-watson-version-40){: external}

<!--### IBM Cloud Private End Of Support
### ![Cloud Pak for Data only](images/desktop.png) 4 release, 30 September 2021
{: #discovery-data-30september2021}

Effective 30 September 2021, IBM withdrew support for the following programs:

- IBM Watson Assistant Discovery Extension for IBM Cloud Private
- IBM Watson Discovery for ICP for Data
- IBM Watson Discovery for ICP for Data Add-on

For more information, see announcements [ENUS921-005.PDF](https://www.ibm.com/common/ssi/cgi-bin/ssialias?subtype=ca&infotype=an&appname=iSource&supplier=897&letternum=ENUS921-005){: external} and [ENUSLP21-0099.PDF](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/9/899/ENUSLP21-0099/index.html&request_locale=en).-->

### ![Cloud Pak for Data only](images/desktop.png) 4 release, 13 July 2021
{: #discovery-data-13july2021}

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

### ![Cloud Pak for Data only](images/desktop.png) 2.2.1 release, 26 February 2021
{: #discovery-data-26february2021}

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

### ![Cloud Pak for Data only](images/desktop.png) 2.2.0 release, 8 December 2020
{: #discovery-data-8december2020}

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

### ![Cloud Pak for Data only](images/desktop.png) 2.1.4 release, 2 September 2020
{: #discovery-data-2september2020}

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


### ![Cloud Pak for Data only](images/desktop.png) 2.1.3 release, 19 June 2020
{: #discovery-data-19june2020}

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

### ![Cloud Pak for Data only](images/desktop.png) 2.1.2 release, 31 March 2020
{: #discovery-data-31march2020}

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

### ![Cloud Pak for Data only](images/desktop.png) 2.1.1 release, 24 January 2020
{: #discovery-data-24january2020}

New release now available
:   {{site.data.keyword.discovery-data_long}} version 2.1.1 is available.

Fixed the following defects in the 2.1.1 release:
:   In Document Retrieval project types, when you perform an empty search, and the search results source is set to `passages,` the query results will display `excerpt unavailable` in the Project workspace.
:   When visiting the Storybook links on the Integrate and deploy page, the links do not go to the correct location. Please visit [Storybook](https://watson-developer-cloud.github.io/discovery-components/storybook){: external} instead to view documentation.
:   If you are using Smart Document Understanding, two variables no longer need to be set during installation or reinstallation. For more information, see [Environment variable settings for Smart Document Understanding](/docs/discovery-data?topic=discovery-data-troubleshoot#troubleshoot-sdu).
:   Discovery for Content Intelligence and Table Understanding enrichments are configured out of the box to be applied on a field named `html`. When a user uploads a JSON document without a root-level field named `html`, these enrichments will not yield results in the index. To run the enrichments on this kind of JSON documents, users must re-configure the enrichments to run on an existing field (or fields) in the JSON document.

### ![Cloud Pak for Data only](images/desktop.png) 2.1.0 release, 27 November 2019
{: #discovery-data-27november2019}

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

### ![Cloud Pak for Data only](images/desktop.png) 2.0.1 release, 30 August 2019
{: #discovery-data-30august2019}

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

### ![Cloud Pak for Data only](images/desktop.png) 2.0.0, General Availability (GA) release, 28 June 2019
{: #discovery-data-28june2019}

Discovery for Cloud Pak for Data now available
:   The {{site.data.keyword.discovery-data_long}} service brings the cognitive capabilities of {{site.data.keyword.discoveryfull}} to the {{site.data.keyword.icp4dfull}} platform.
