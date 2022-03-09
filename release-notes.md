---

copyright:
  years: 2019, 2022
lastupdated: "2022-03-09"

keywords: discovery release notes,discovery cloud pak for data release notes,watson discovery release notes,what's new,new features,improvements,change log,changelog

subcollection: discovery-data
content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.discoveryshort}} for {{site.data.keyword.cloud_notm}}
{: #release-notes}

Learn about features and changes that were included for each release and update of the product software.
{: shortdesc}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed instances of {{site.data.keyword.discoveryfull}} that are hosted on {{site.data.keyword.cloud_notm}} or that were provisioned with [IBM Cloud Pak for Data as a Service](https://dataplatform.cloud.ibm.com/docs/content/wsj/landings/watsondisc.html){: external}. For information about releases and updates for installed deployments, see [Release notes for {{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}}](/docs/discovery-data?topic=discovery-data-release-notes-data).
{: note}

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
:   Lite and Advanced plans are discontinued. You cannot create **new** service instances that use the Lite or Advanced plan types in the Dallas, Frankfurt, London, Seoul, Sydney, Tokyo, and Washington DC locations. Any existing Lite and Advanced plans continue to function properly and continue to be supported. You can upgrade from a Lite plan to an Advanced plan. Use the new Plus plan and its associated 30-day free trial to explore new features and a simpler way to build that is available with the latest version of the product.

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
:   The beta release of Patterns enrichment uses pattern induction to help you teach {{site.data.keyword.discoveryshort}} to recognize patterns in your data. Pattern induction generates extraction patterns from the examples you specify. After you specify a small number of examples, {{site.data.keyword.discoveryshort}} will suggest additional rules that you verify to complete the pattern. You can use pattern induction as an enrichment or to create a facet. For more information, see [Patterns](/docs/discovery-data?topic=discovery-data-domain#patterns) and [Creating a facet by identifying a pattern](/docs/discovery-data?topic=discovery-data-facets#facetpattern). For a statement explaining beta features, see [Beta features](/docs/discovery-data?topic=discovery-data-release-notes#beta-features).


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
:   This entirely new capability of Watson {{site.data.keyword.discoveryshort}} allows you to find insights in your data when you may not even know the question to ask. The powerful correlation tooling will help you unlock value from large unstructured data sets. For details, see [Using the Content Mining application](/docs/discovery-data?topic=discovery-data-contentminerapp).

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
