---

copyright:
  years: 2019, 2023
lastupdated: "2023-03-23"

keywords: discovery release notes,watson discovery release notes,what's new,new features,improvements,change log,changelog

subcollection: discovery-data
content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.discoveryshort}} for {{site.data.keyword.cloud_notm}}
{: #release-notes}

Learn about features and changes that were included for each release and update of the product software.
{: shortdesc}

[IBM Cloud]{: tag-ibm-cloud}

This information applies only to managed instances of {{site.data.keyword.discoveryfull}} that are hosted on {{site.data.keyword.cloud_notm}} or that were provisioned with [IBM Cloud Pak for Data as a Service](https://dataplatform.cloud.ibm.com/docs/content/wsj/landings/watsondisc.html){: external}. For information about releases and updates for installed deployments, see [Release notes for {{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}}](/docs/discovery-data?topic=discovery-data-release-notes-data).
{: note}

## 2 March 2023
{: #discovery-2march2023}
{: release-note}

<!-- 4.7.0-7.1 -->

Now you can specify the types of files to add to a collection
:   When you connect to an external data source, you can limit the types of files to add from the external data source to the collection. For example, you can choose to add only PDF files from a Box data source.

## 21 Febuary 2023
{: #discovery-21febuary2023}
{: release-note}

Optical character recognition v2 technology is used
:   The latest version (OCR v2) is used automatically when you enable OCR for English, German, French, Spanish, Dutch, Brazilian Portuguese, and Hebrew collections in all {{site.data.keyword.cloud_notm}} service plans. 

    The new optical character recognition model was developed by IBM Research to be better at extracting text from scanned documents and other images that have the following limitations:

    -   Low quality images due to incorrect scanner settings, insufficient resolution, bad lighting (such as with mobile capture), loss of focus, unaligned pages, and badly printed documents
    -   Documents with irregular fonts or a variety of colors, font sizes, and backgrounds

The entity extractor limits changed
:   The number of documents that are allowed in the training data for the Plus plan increased from 100 to 200.

    The number of entity types that you can create per plan decreased.
    
    - For Premium plans, the limit changed from 75 to 18.
    - For Enterprise plans, the limit changed from 50 to 18.
    - For Plus plans, the limit changed from 20 to 12.

The string variation operator now works with phrases
:   When you include the string variation operator with query input that contains a phrase, the variation is applied to each word in the phrase. For example, `"tom cat"~1` matches `top hat` in addition to `tom cat`. For more information about Discovery Query Language operators, see [Query operators](/docs/discovery-data?topic=discovery-data-query-operators).

## 10 Febuary 2023
{: #discovery-10febuary2023}
{: release-note}

<!-- 4.7.0-6.0 -->

Entity extractor is generally available
:   The *Extract entities* enrichment brings the powerful ability to build a custom type system into {{site.data.keyword.discoveryshort}}. Use the tool to label entity examples within your industry data to build a machine learning model that {{site.data.keyword.discoveryshort}} can use to recognize meaningful terms for your business. Already built an entity type system in {{site.data.keyword.knowledgestudioshort}}? You can use the corpus from {{site.data.keyword.knowledgestudioshort}} as a starting point for your {{site.data.keyword.discoveryshort}} entity extractor training data. For more information, see [Entity extractor](/docs/discovery-data?topic=discovery-data-entity-extractor).

    If you created an entity extractor enrichment for testing purposes when the feature was in beta release, now that it is generally available, it will count toward your custom model limit. The entity extractor enrichment incurs charges whether or not it is applied to a collection.
    {: attention}

## 7 Febuary 2023
{: #discovery-7febuary2023}
{: release-note}

<!-- 4.7.0-5.0 -->

Support for hourly crawls was removed
:   You can no longer choose to crawl a data source every hour. If an existing collection is configured to crawl hourly, you will be prompted to change the scheduled crawl the next time you edit the connector settings.

You can no longer enable FAQ extraction for a collection
:   The checkbox to enable or disable the beta FAQ extraction feature was removed. FAQ extraction was a beta feature that captured question-and-answer pairs from the data source as it was crawled. FAQ extraction generated a new subdocument for each pair and stored the question in the `title` field and the answer in the `text` field.

    You cannot apply FAQ extraction to new collections. 

    Any existing collections with FAQ extraction enabled retain FAQ documents in their indexes until the collection is reprocessed. At that time, most of the question-and-answer pair subdocuments are deleted. However, any FAQ subdocuments that were generated from HTML or TXT source files remain. If you want to remove these subdocuments, go to the *Manage data* page to delete them. Subdocuments that are generated from one parent document all have the same `metadata.parent_document_id` value.

    If you need a way to extract question-and-answer pairs from source documents that use a consistent style and formatting for questions and answers, you can use the Smart Document Understanding tool to annotate the pairs instead. For more information, see [Using Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields).

## 25 January 2023
{: #discovery-25january2023}
{: release-note}

<!-- 4.7.0-4.0 -->

Set up a Microsoft SharePoint Online data store connector that has *Read* permission
:   When you create a Microsoft SharePoint Online connector to crawl a SharePoint data source by using Open Authentication v2, the enterprise application that is created by Discovery to make the connection requires *Read* permission only. The enterprise application that was configured for you previously required *Write* permission.

    If you want to update an existing connector so that you can use the new Read permission configuration, you must delete your existing enterprise application first.

    For more information, see [Microsoft SharePoint Online connector](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cloud).

## FAQ extraction deprecation announcement
{: #faq-extraction-deprecation-1december2022}

The beta FAQ extraction feature that detects and extracts question-and-answer pairs from documents is being removed. Support for the feature will end in 1Q 2023.

## 6 December 2022
{: #discovery-6december2022}
{: release-note}

<!-- 4.7.0-3.0 -->

Now you can stop a data source crawl
:   You can stop a crawl that is in progress or that is scheduled to occur in the future. For more information, see [Stopping a crawl](/docs/discovery-data?topic=discovery-data-collections#collections-crawl-stop).

The following item is a known issue:

Box data source scheduled crawls are not updating documents
:   Due to a problem in the Box Events API, changes that occur between crawls in documents that are stored in Box are not detected and picked up by the Discovery collection during scheduled recrawls. To ensure that your collection is up-to-date, stop and restart the crawl.

## 1 December 2022
{: #discovery-1december2022}
{: release-note}

Plus plan supports fewer entity extractors
:   The maximum number of entity extractors that you can create with a Plus plan decreased from 6 to 3.

## 12 November 2022
{: #discovery-12november2022}
{: release-note}

Discovery users might experience issues with documents in collections where OCR is enabled that were added or processed between Nov 1 and Nov 11
:   Between 1 November and 11 November 2022, some projects with optical character recognition (OCR) enabled, including Document Retrieval for Contracts projects, experienced problems. The problems were related to a new version of the optical character recognition (OCR v2) feature that was enabled automatically for English, German, French, Spanish, Dutch, Brazilian Portuguese, and Hebrew collections during that timeframe. The new version changes sentence boundaries in ways that can negatively impact other functions, including element identification in contracts and the document labeling view in the entity extractor tool.

    If you experience any of these issues with documents that were added or processed during this period, revert the version of OCR that is applied to the documents. Starting on 12 November 2022, OCR v1 is applied to all collections where OCR is enabled. To go back to using OCR v1, make a change that will reprocess the affected documents. For example, you can re-add documents that were added during the timeframe to reprocess them. Or you can reprocess an entire collection.

    To reprocess a collection, from the *Manage collections* page, open the collection, and then go to the *Processing settings* tab. Expand the *More processing settings* section, set the OCR switch to **Off**, and then set it back to **On**. Click **Apply changes and reprocess** to reprocess your collection.

## 2 November 2022
{: #discovery-2november2022}
{: release-note}

A new and improved optical character recognition technology is available
:   A new version of optical character recognition technology is now available. This latest version (OCR v2) is used automatically when you enable OCR for English, German, French, Spanish, Dutch, Brazilian Portuguese, and Hebrew collections in all {{site.data.keyword.cloud_notm}} service plans. The new optical character recognition model was developed by IBM Research to be better at extracting text from scanned documents and other images that have the following limitations:

    -   Low quality images due to incorrect scanner settings, insufficient resolution, bad lighting (such as with mobile capture), loss of focus, unaligned pages, and badly printed documents
    -   Documents with irregular fonts or a variety of colors, font sizes, and backgrounds

## 1 November 2022
{: #discovery-1november2022}
{: release-note}

<!-- 4.7.0-1.0 -->

Entity extractor loads the first 40,000 characters from training data documents
:   Even extra long documents from the collection that you use to define custom entity examples are loaded into the document view of the tool. However, only the first 40,000 characters, which is approximately 15-20 pages, are displayed. The rest of the file content is truncated. You'll know if your document is truncated because a notification is displayed in the document view. For more information, see [Entity extractor](/docs/discovery-data?topic=discovery-data-entity-extractor).

You can set the passages per document setting to be higher than one
:   A bug was fixed that prevented you from using the search bar settings in the product user interface to increase the maximum number of passages to return per document. For more information, see [How passages are derived](/docs/discovery-data?topic=discovery-data-index-overview#query-results-passages).

Improved query aggregation documentation
:   The documentation that describes the aggregation types that you can specify in the query aggregation parameter was updated. For more information, see [Query aggregations](/docs/discovery-data?topic=discovery-data-query-aggregations).

## 30 September 2022
{: #discovery-30september2022}
{: release-note}

Lite plans are no longer available from the London data center
:   Lite plans are discontinued. You cannot create **new** service instances that use the Lite plan type in any location, including London. Use the new Plus plan and its associated 30-day free trial to explore new features and a simpler way to build that is available with the latest version of the product.

## 22 September 2022
{: #discovery-22september2022}
{: release-note}

Plus plan supports more entity extractors
:   The maximum number of entity extractors that you can create with a Plus plan increased from 3 to 6.

You cannot apply a Smart Document Understanding model to Microsoft Excel files
:   The quality of structural analysis that can be produced for Excel files is not sufficient. Starting on 22 September 2022, you cannot apply an SDU model to Excel files. This change does not impact Excel files in collections where an SDU model was applied before 22 September 2022.

## 16 September 2022
{: #discovery-16september2022}
{: release-note}

<!-- 4.6.0-6.4 -->

In-context document preview is now available for PDF files that are crawled
:   When you click to view a passage from a search result that is extracted from a PDF document, a document preview page is displayed that shows the returned passage in the context of the original PDF page. The in-context view is available for PDF files to which a Smart Document Understanding model is applied.

## 15 August 2022
{: #discovery-15august2022}
{: release-note}

SDKs were updated to reflect the latest API changes.
:    The following [Discovery v2 API](/apidocs/discovery-data){: external} changes are now reflected in the SDKs:

    -   Use the new document classifier API to get, add, update, or delete a document classifier.

    -   A new document status API is available. You can use it to get a list of the documents in a collection and to get details about a single document.

    -   You can now get, add, and remove a stop words or expansion list for a collection.

    -   A `smart_document_understanding` field is returned with the *Get collection* method. This new field specifies whether an SDU model is enabled for the collection and indicates the model type.

    -   A `similar` parameter is available from the *Query* method. Use it to find documents that are similar to documents of interest to you.
     
    -   The `suggested_refinements` parameter of the *Query* method is deprecated. The `suggested_refinements` parameter was used to identify dynamic facets from Premium plan data.

## 8 August 2022
{: #discovery-8august2022}
{: release-note}

Larger documents can be crawled
:   The maximum file sizes that are allowed for crawled documents increased for Premium plans. It also increased for the Box, IBM Cloud Object Storage, and Salesforce connectors. For more information, see [File size limits](/docs/discovery-data?topic=discovery-data-collections#collections-file-size-limits).

## 2 August 2022
{: #discovery-2august2022}
{: release-note}

<!-- 4.6.0-4.2 -->

IAM authentication support was added to the IBM Cloud Object Storage connector
:   You can now choose to authenticate with the IBM Cloud Identity and Access Management (IAM) service. For more information, see [IBM Cloud Object Storage](/docs/discovery-data?topic=discovery-data-connector-cos-cloud).

## 28 July 2022
{: #discovery-28july2022}
{: release-note}

API updates
:    The following changes were made to the [Discovery v2 API](/apidocs/discovery-data){: external}.

     New fields are available:

     -   A `smart_document_understanding` field is returned with the *Get collection* method. This new field specifies whether an SDU model is enabled for the collection and indicates the model type.
     -   A `similar` parameter is available from the *Query* method. Use it to find documents that are similar to documents of interest to you.
     
     The `suggested_refinements` parameter of the *Query* method is deprecated. The `suggested_refinements` parameter was used to identify dynamic facets from Premium plan data.

## Discovery v1 deprecation announcement
{: #discovery-v1-deprecation-12july2022}

Watson Discovery v1 is being deprecated. Existing clients who use Watson Discovery v1 are asked to migrate to Watson Discovery v2 before the end-of-support date of **11 July 2023**. End of Support means that no v1 instance will work on or after 11 July 2023. For more information about migration, see [Getting the most from Discovery](/docs/discovery-data?topic=discovery-data-version-choose).
{: deprecated}

## 11 July 2022
{: #discovery-11july2022}
{: release-note}

<!-- 4.6.0-2.5 -->

The advanced document view highlights even more enrichments
:   In addition to the built-in *Entities* and *Keywords* enrichments that are recognized by Watson Natural Language Processing models, the advanced document view now highlights the following types of enrichments:

    -   Custom dictionary terms
    -   Terms or numbers that match regular expression patterns that you define
    -   Custom entities and relationships that are defined by Watson Knowledge Studio machine learning and rules-based models
    -   Custom entities that are defined by using the entity extractor tool that is available as a beta feature

    For more information about enrichments that you can add to your documents, see [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain).

## 30 June 2022
{: #discovery-30june2022}
{: release-note}

Watson SDK support change
:   Support for the following SDKs is provided by the Watson community of developers instead of IBM:

    -   Go
    -   Ruby
    -   Swift
    -   Unity

    For more information, see [Watson SDKs](/docs/discovery-data?topic=watson-using-sdks).

## 1 June 2022
{: #discovery-1june2022}
{: release-note}

<!--  4.6.0-0.1 -->

The entity extractor tool is now easier to use
:   The user interface was redesigned to better support the workflow of adding entity types and labeling examples of them. As part of the new design, the bulk labeling feature now is enabled by default, the documents view is easier to find and use, the suggestions pane is more responsive, and you can track metrics scores across multiple training runs. For more information about the entity extractor, see [Customizing the terms that Discovery can recognize](/docs/discovery-data?topic=discovery-data-entity-extractor).

The entity extractor is now available in more plans and languages
:   The entity extractor beta feature is now available to users of Plus and Enterprise plans in addition to Premium plans. The extractor enrichment is supported for collections in languages other than English.

When you remove a starting URL from a Web crawl connector its associated documents are deleted
:   The Web crawl connector was updated. Starting with collections that you create after April 2022, if you remove a starting URL from the Web crawl configuration, any indexed documents that were derived from the content of the web page at that URL are deleted with the next crawl. For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cloud).

## 16 May 2022
{: #discovery-16may2022}
{: release-note}

Added API methods for working with stop words and expansion lists
:   You can now get, add, and remove a stop words or expansion list for a collection programmatically. For more information, see the [Query modifications](/apidocs/discovery-data#getstopwordlist){: external} methods.

## 13 May 2022
{: #discovery-13may2022}
{: release-note}

<!--  4.5.0-0.1 -->

An improved JSON view is available
:   You can now use keyboard keys to tab through elements in the view. The new JSON view also numbers the occurrences of elements in each JSON object, which makes it easier to keep track of information and to read totals at a glance.

## 20 April 2022
{: #discovery-20april2022}
{: release-note}

Analyze API is supported in Enterprise plan deployments
:   Use the Analyze API to process a JSON file according to a collection's configuration settings, and then return the file for realtime use without storing it in the collection. The Analyze API was supported only in installed deployments previously. For more information, see [Analyze API](/docs/discovery-data?topic=discovery-data-analyzeapi).

A new document status API is available
:   Use the new document status API to programmatically get a list of the documents in a collection and to get details about a single document. The following notes apply to this release:

    -   The API is supported for collections that are created after 23 March 2022. 
    
        If you want to get status information about a collection that was created earlier, trigger a process that runs the conversion step of ingestion on the documents. For example, you can enable the API by making changes in the *Identify fields*, *Manage fields*, *CSV settings*, or *Processing settings* (such as OCR or FAQ extraction settings) pages, or by applying a Smart Document Understanding model to the older collection.
    -   The API is available only from Plus and Enterprise plan instances. 

    For more information about the new API, see the [API reference documentation](/apidocs/discovery-data#listdocuments){: external}.

More messages are shown to keep you informed about the status of document processing
:   An issue was fixed which previously prevented informative messages from being displayed about the status of document conversion and indexing during the ingestion process. Now that the issue is fixed, you might see more messages than usual when you add or reprocess documents. This increase is expected. Nothing you did caused the increase in messages.

## 6 April 2022
{: #discovery-6april2022}
{: release-note}

<!-- 4.0.9-0.1 -->

Project tile has a more intuitive menu
:   The project tile was updated to include an overflow menu that you can use to perform actions such as deleting or renaming a project.

## 30 March 2022
{: #discovery-30march2022}
{: release-note}

A new document classifier API is available
:   Use the new document classifier to programmatically get, add, update, or delete a document classifier. Document classifier methods are supported on installed intances (IBM Cloud Pak for Data) or IBM Cloud-managed Premium or Enterprise plan instances.

    For more information about the new API, see the [API reference documentation](/apidocs/discovery-data#listdocumentclassifiers){: external}. For more information about adding a document classifier by using the product user interface, see [Classifying documents](/docs/discovery-data?topic=discovery-data-cm-doc-classifier).

## 21 March 2022
{: #discovery-21march2022}
{: release-note}

<!-- 4.0.8-1.0 -->

Visualize enrichments found in your documents
:   When you click to view the passage from a search result, a document preview page is displayed that shows a representation of the original document where the search result was found. For most document types, you can open a new *advanced view* of the document to see useful summary information, such as the number of occurrences of any enrichments that are detected in the document. You also can select one of the enrichments to highlight every occurrence of the element within the document text.

    Currently, only the *Entities* and *Keywords* enrichments are listed.
    {: note}

Improved format of search results from PDF documents
:   When you click to view a passage from a search result that is extracted from a PDF document, a document preview page is displayed that shows the returned passage in the context of the original PDF page.
    
    The in-context view is available for PDF files to which a Smart Document Understanding model is applied. The rich preview does not work on images, meaning it doesn't work on scanned PDF documents. The in-context view is available for PDFs in all languages; however, the enrichment highlighting might be misaligned in some languages.
    {: note}

Tell us what you think
:   Share your opinions and ideas with us at any time by clicking the **Share feedback** button from the page header of the product user interface.

## 10 March 2022
{: #discovery-10march2022}
{: release-note}

<!-- 4.0.8-0.6 -->

Manage the data in a collection from the new *Manage data* page
:   You can now access the *Manage data* page for a collection from the *Manage collections* navigation pane. Go there to see a list of the documents in your collection and get a quick view of information about the documents. You can also delete documents from a collection with just a few clicks. For more information, see [Excluding content from query results](/docs/discovery-data?topic=discovery-data-hide-data).

## 15 February 2022
{: #discovery-15february2022}
{: release-note}

<!-- 4.0.6-1.0 -->

An alternative authentication mechanism is available for Microsoft Sharepoint Online connectors
:   You can now use Open Authentication to sign in to Microsoft SharePoint directly when you configure a new {{site.data.keyword.cloud_notm}} connector. The *Sign in with Microsoft* option that uses Open Authentication to authenticate with the external data source is a beta feature. For more information, see [Microsoft SharePoint Online](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cloud).


## 7 January 2022
{: #discovery-7january2022}
{: release-note}

<!-- 4.0.5-4.0 -->

Upgrade from Plus to Enterprise without help
:   You can perform an in-place upgrade from a Plus plan to an Enterprise plan. For more information, see [Upgrading](/docs/discovery-data?topic=discovery-data-upgrade).

## 6 December 2021
{: #discovery-6december2021}
{: release-note}

<!-- 4.0.5-2.4 -->

Crawling web pages with dynamic content is now generally available
:   The *Execute JavaScript during crawl* feature was introduced as a beta feature, but is now generally available. For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cloud).

Capturing the SharePoint ACL information from crawled documents
:   You can now configure the data source crawl to store ACL information as metadata in the documents that are added to your SharePoint Online collection. For more information, see [Microsoft SharePoint Online](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cloud).

You can add more documents to the training data of the beta entity extractor model
:   If you added and labeled 20 documents to train a model, and now want to continue to improve the model's performance, you can add more documents. Add the additional documents to the collection that you are using to train the model. After you label the first 20 documents, and the model is up to date with any changes, you can choose to continue labeling documents. The new documents that you added to the collection are loaded. You can label them to augment the training data, and then retrain your model. For more information, see [Customizing the terms that {{site.data.keyword.discoveryshort}} can recognize](/docs/discovery-data?topic=discovery-data-entity-extractor).

Log out of {{site.data.keyword.discoveryshort}}
:   You can log out of the {{site.data.keyword.discoveryshort}} service instance at any time by clicking **Log out** from the user profile menu that is available from the page header of the product user interface.

## 18 November 2021
{: #discovery-18november2021}
{: release-note}

Enterprise plan is now available everywhere
:   The Enterprise plan is available from all data center locations. Scale and secure your {{site.data.keyword.discoveryshort}} application with enterprise-grade support and performance, and address more use cases including contract analysis and content mining to explore insights across documents. For more information, see [{{site.data.keyword.discoveryshort}} pricing plans](/docs/discovery-data?topic=discovery-data-pricing-plans).

## 11 November 2021
{: #discovery-11november2021}
{: release-note}

New locations for Enterprise plan now available
:   The Enterprise plan is available from the Frankfurt, London, Sydney, and Tokyo locations in addition to the Dallas location.

## 3 November 2021
{: #discovery-3november2021}
{: release-note}

<!--4.0.4-0.5-->

New Enterprise plan
:   Scale and secure your {{site.data.keyword.discoveryshort}} application with enterprise-grade support and performance and address more use cases, including contract analysis and content mining to explore insights across documents. Currently, the Enterprise plan is available only from the Dallas location. For more information, see [{{site.data.keyword.discoveryshort}} pricing plans](/docs/discovery-data?topic=discovery-data-pricing-plans).

New beta entity extractor enrichment
:   The *Extract entities* enrichment brings the powerful ability to build a custom type system into {{site.data.keyword.discoveryshort}}. Use the tool to label entity examples within your industry data to build a machine learning model that {{site.data.keyword.discoveryshort}} can use to recognize meaningful terms for your business. Currently, this beta feature is available for English-language projects that are created in Premium plan service instances only. For more information, see [Customizing the terms that {{site.data.keyword.discoveryshort}} can recognize](/docs/discovery-data?topic=discovery-data-entity-extractor).

New *Helpful links* tab
:   The home page includes a *Helpful links* tab that has quick links to documentation, a community site, and other resources. 

Improved field selection choices
:   When you apply an enrichment to a field or choose a field to use as the source for a facet, the fields that are displayed for you to choose from now include only fields that are valid choices. Previously, the list included fields that were not valid choices.

## 14 October 2021
{: #discovery-14october2021}
{: release-note}

<!--4.0.3-3.2-->

New {{site.data.keyword.discoveryshort}} home page
:   A new home page is displayed when you start {{site.data.keyword.discoveryshort}} and gives you quick access to a product overview video, and tours. You can collapse the home page welcome banner to see more projects.

New plan usage section 
:   Stay informed about plan usage and check your usage against the limits for your plan type from the *Plan limits and usage* page. From the product page header, click the user icon ![User icon](images/user-icon.png). The *Usage* section shows a short summary. Click **View all** to see usage information for all of the plan limit categories.

Change to spelling settings in Search
:   The spelling correction setting changed from being enabled automatically in new projects to being disabled by default. If you want to alert users when they misspell a term in their query, turn on *Spelling suggestions*. For more information, see [Customizing the search bar](/docs/discovery-data?topic=discovery-data-search-bar).

Improved **Guided tours** availability
:    The **Guided tours** button is now available from the product page header, which make them accessible from anywhere. Previously, it was available from the *My Projects* page only.

## 1 October 2021
{: #discovery-1october2021}
{: release-note}

Change to Lite and Advanced plans in all locations
:   Lite and Advanced plans are discontinued. You cannot create **new** service instances that use the Lite or Advanced plan types in the Dallas, Frankfurt, London, Sydney, Tokyo, and Washington DC locations. Any existing Lite and Advanced plans continue to function properly and continue to be supported. You can upgrade from a Lite plan to an Advanced plan. Use the new Plus plan and its associated 30-day free trial to explore new features and a simpler way to build that is available with the latest version of the product.

## 24 September 2021
{: #discovery-24september2021}
{: release-note}

<!--4.0.3-1.2-->

New scoring for NLU enrichments
:   Relevance and confidence scores are displayed for NLU enrichments that are returned by search. For example, when you open the JSON view of the document preview from a query result, you can see confidence scores for Entities mentions and relevance scores for Keyword mentions.

## 9 September 2021
{: #discovery-9september2021}
{: release-note}

New location for Plus plan
:   The Plus plan is now available from the Sydney location. Use the new Plus plan and its associated 30-day free trial to explore new features and a simpler way to build that is available with the latest version of the product. For more information, see [Getting the most from {{site.data.keyword.discoveryshort}}](/docs/discovery-data?topic=discovery-data-version-choose).

Change to Lite and Advanced plans in most locations
:   Lite and Advanced plans are discontinued. You cannot create **new** service instances that use the Lite or Advanced plan types in the Dallas, Frankfurt, London, Sydney, Tokyo, or Washington DC locations. Any existing Lite and Advanced plans continue to function properly and continue to be supported. You can upgrade from a Lite plan to an Advanced plan.

## 26 August 2021
{: #discovery-26august2021}
{: release-note}

New locations for the Plus plan
:   The Plus plan is now available from the London and Washington DC locations, in addition to Dallas, Frankfurt, and Tokyo.

Change to Lite and Advanced plans in some locations
:   You cannot create **new** service instances that use the Lite or Advanced plan types in the Dallas, Frankfurt, London, Tokyo, or Washington DC locations. Any existing Lite and Advanced plans continue to function properly and continue to be supported. You can upgrade from a Lite plan to an Advanced plan.

New answer finding feature
:   Answer finding is now generally available for managed deployments. Use answer finding when you want to return a concise answer to a question. For more information, see [Answer finding](/docs/discovery-data?topic=discovery-data-query-parameters#answer-finding).

## 16 August 2021
{: #discovery-16august2021}
{: release-note}

New locations for the Plus plan
:   The Plus plan is now available from the Frankfurt and Tokyo locations, in addition to Dallas.

Change to Lite and Advanced plans in some locations
:   Lite and Advanced plans are no longer offered. You cannot create **new** service instances that use the Lite or Advanced plan types in the Dallas, Frankfurt, or Tokyo locations. Any existing Lite and Advanced plans continue to function properly and continue to be supported. You can upgrade from a Lite plan to an Advanced plan.

## 27 July 2021
{: #discovery-27july2021}
{: release-note}

Improved document size limit
:   Document size limit is increased. For Premium plan collections, you can now upload files that are up to 50 MB in size instead of 32 MB. For more information, see [Document limits](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-collections#collections-doc-limits).

## 23 July 2021
{: #discovery-23july2021}
{: release-note}

Improved SharePoint Online connector
:   The Microsoft SharePoint Online data source connector now accepts any valid Azure Active Directory user ID syntax; the format of the user ID doesn't need to match the `<admin_user>@.onmicrosoft.com` syntax. For more information, see [Microsoft SharePoint Online](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cloud).

## 16 July 2021
{: #discovery-16july2021}
{: release-note}

New beta dynamic website web crawl
:   The Web crawler can now crawl dynamic websites that use JavaScript to render content. If you enable this beta feature, the time it takes to crawl the site increases. For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cloud).

## 23 June 2021
{: #discovery-23june2021}
{: release-note}

New Plus plan
:   Use the new Plus plan and its associated 30-day free trial to explore new features and a simpler way to build that is available with the latest version of the product. Currently, the Plus plan is available from the Dallas location. For more information, see [Getting the most from {{site.data.keyword.discoveryshort}}](/docs/discovery-data?topic=discovery-data-version-choose).

Change to Lite and Advanced plans
:   Lite and Advanced plans are no longer offered. You cannot create **new** service instances that use the Lite or Advanced plan types in the Dallas location. Any existing Lite and Advanced plans continue to function properly and continue to be supported. You can upgrade from a Lite plan to an Advanced plan.

## Endpoint deprecation reminder
{: #discovery-6april2021}
{: release-note}

Change to {{site.data.keyword.discoveryshort}} API endpoint
:   As part of work done to fully support Identity and Access Management (IAM) authentication, the endpoint that you use to access your {{site.data.keyword.discoveryshort}} service programmatically is changing. The old endpoint URLs are deprecated and **will be retired on 26 May 2021**. Update your API calls to use the new URLs.

    The pattern for the endpoint URL changed from `gateway-{location}.watsonplatform.net/discovery/api/` to `api.{location}.discovery.watson.cloud.ibm.com/`. The domain, location, and offering identifier are different in the new endpoint. For more information, see [Updating endpoint URLs from watsonplatform.net](/docs/watson?topic=watson-endpoint-change){: external}.

    If your service instance API credentials use the old endpoint, create a new credential and start using it today. After you update your custom applications to use the new credential, you can delete the old one.

## 19 March 2021
{: #discovery-19march2021}
{: release-note}

Improved Web crawl connector
:   You can use the Web crawl collection type to connect to content that is stored on an internal company website. For more information, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cloud).

## 4 March 2021
{: #discovery-4march2021}
{: release-note}

New drag and drop feature when uploading
:   Upload collections now support dragging and dropping documents before and during document upload. For more information, see [Uploading data](/docs/discovery-data?topic=discovery-data-upload-data).

New list view for collections
:   You can view a list of collections that are connected to a particular gateway. For more information, see [Viewing collections connected to a gateway](/docs/discovery-data?topic=discovery-data-sources#gateway-connection).

## 17 December 2020
{: #discovery-17december2020}
{: release-note}

Improved date and time display on Activity tab
:   Each collection now displays the **Next sync scheduled for** date and time on the **Activity** tab of the **Manage collections** page.

New beta FAQ extraction
:   Released the beta feature FAQ extraction. FAQ extraction automatically extracts question-and-answer pairs from FAQ (frequently asked questions) documents and web pages so that your application returns more precise answers. For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction). For a statement explaining beta features, see [Beta features](/docs/discovery-data?topic=discovery-data-release-notes#beta-features).

## 3 December 2020
{: #discovery-3december2020}
{: release-note}

New Content Intelligence
:   You can now apply the **Contracts** enrichment to a **Document Retrieval** project when you create it. The Contracts enrichment can be used to classify contract terms, parties, effective dates and more within your documents. For more information, see [Document Retrieval for Contracts](/docs/discovery-data?topic=discovery-data-projects#doc-retrieval-contracts).

## 10 November 2020
{: #discovery-10november2020}
{: release-note}

New Box connector
:   Crawl Box systems. For more information, see [Box](/docs/discovery-data?topic=discovery-data-sources#connectboxpublic).

New SharePoint 2016 On-Premises connector
:   Crawl SharePoint 2016 On-Premises systems. For more information, see [SharePoint 2016 On-Premises](/docs/discovery-data?topic=discovery-data-connector-sharepoint-onprem-cloud).

The Box connector does not run on Safari
:   For more information, see [Box connector](/docs/discovery-data?topic=discovery-data-connector-box-cloud).

Metadata conversion
:   If the `metadata` property is converted to an array in the index, the document cannot be deleted by using the *Delete labeled data* API method. For more information, see the [API reference](https://{DomainName}/apidocs/discovery-data#deletedocument){: external}.

## 30 October 2020
{: #discovery-30october2020}
{: release-note}

New language support for Bosnian, Croatian, Hindi, and Serbian
:   Basic language support now available for Bosnian, Croatian, Hindi, and Serbian. For more information, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

New beta Patterns enrichment
:   The beta release of Patterns enrichment uses pattern induction to help you teach {{site.data.keyword.discoveryshort}} to recognize patterns in your data. Pattern induction generates extraction patterns from the examples you specify. After you specify a small number of examples, {{site.data.keyword.discoveryshort}} will suggest additional rules that you verify to complete the pattern. You can use pattern induction as an enrichment or to create a facet. For more information, see [Patterns](/docs/discovery-data?topic=discovery-data-domain-pattern) and [Creating a facet by identifying a pattern](/docs/discovery-data?topic=discovery-data-facets#facetpattern). For a statement explaining beta features, see [Beta features](/docs/discovery-data?topic=discovery-data-release-notes#beta-features).


Change to Document Retrieval projects
:   In new **Document Retrieval** projects, the `suggested refinements` query setting is now set to `false` by default. It was previously set to `true`.

## 14 September 2020
{: #discovery-14september2020}
{: release-note}

New pre-trained model for SDU
:   A new pre-trained model is available in Smart Document Understanding for Document Retrieval projects. This model is ideal if you need to extract data from documents that include a large number of tables. For more information, see [Identifying fields](/docs/discovery-data?topic=discovery-data-configuring-fields#identify-fields).

## 30 August 2020
{: #discovery-30august2020}
{: release-note}

Update to API version
:   The current API version (v2) is now 2020-08-30. The following change was made with this version:

Change to 'options' object
:   The List enrichments method no longer returns the `options` object per enrichment. Use the Get enrichment method to return the `options` object for a single enrichment.

## 16 July 2020
{: #discovery-16july2020}
{: release-note}

New release for Premium instances
:   This release is available for Premium instances of {{site.data.keyword.discoveryshort}} on {{site.data.keyword.cloud_notm}} created after 16 July 2020. For Premium instances created before that date and for all Lite and Advanced plans, see [Getting started with {{site.data.keyword.discoveryshort}}](/docs/discovery?topic=discovery-getting-started).

Change to **IBM Cloud Premium** 
:   The Premium plan is now generally available.

New Project-based interface
:   The project-based UI includes configurations optimized for three common use cases: Document Retrieval, Conversational Search, and Content Mining. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).

New Content Mining app
:   This entirely new capability of Watson {{site.data.keyword.discoveryshort}} allows you to find insights in your data when you may not even know the question to ask. The powerful correlation tooling will help you unlock value from large unstructured data sets. For details, see [Analyzing your data with the Content Mining application](/docs/discovery-data?topic=discovery-data-contentminerapp).

New tables as answers
:   Snippets of text aren't helpful if they are found in a table, so {{site.data.keyword.discoveryshort}} instead returns a formatted table as an answer if your question is best answered by a table. For more information, see [Table retrieval](/docs/discovery-data?topic=discovery-data-query-parameters#table_retrieval).

New dynamic faceted search feature
:   Underspecified queries are common. Dynamic Faceted Search automatically categorizes your search results into intelligence facets without training by understanding how they are used in the sentences. See [Facets in Document retrieval projects](/docs/discovery-data?topic=discovery-data-facets#facetdr).

New reusable components
:   You no longer need to build a {{site.data.keyword.discoveryshort}} application from scratch. We now ship out of the box with reusable, open source, React components. As you configure your {{site.data.keyword.discoveryshort}} application, you are using the real components. From there you simply deploy to get a custom {{site.data.keyword.discoveryshort}} application. See [Building and deploying components](/docs/discovery-data?topic=discovery-data-deploy).

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

Cloud Object Storage connector limitation
:   When connecting to an {{site.data.keyword.cos_full}} data source, only the first 75 buckets for a given credential are displayed.

Current API version
:   The API version (v2) is `2019-11-29`.

Change to features in this release
:   Deduplication is not available in this release.
:   Anomaly Detection is not offered.
:   {{site.data.keyword.discoveryfull}} News is no longer included.
:   Several Watson Natural Language Understanding enrichments are not available at this time (Entity extraction, Relation extraction, Keyword extraction, Category classification, Concept tagging, Semantic Role extraction, Sentiment analysis, Emotion analysis)
:   The SharePoint 2016 On-Premises and Box data sources are not available at this time.
