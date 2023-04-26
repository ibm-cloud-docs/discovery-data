---

copyright:
  years: 2020, 2023
lastupdated: "2023-04-24"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Getting the most from {{site.data.keyword.discoveryshort}}
{: #version-choose}

{{site.data.keyword.discoveryshort}} was redesigned to introduce new features and a simpler way to build solutions.
{: shortdesc}

The redesigned product is referred to as {{site.data.keyword.discoveryshort}} v2. When you create an instance on {{site.data.keyword.cloud_notm}} or install and provision an instance on {{site.data.keyword.icp4dfull_notm}}, you get the new and improved version of {{site.data.keyword.discoveryshort}}.

## Advantages of using the latest version
{: #version-choose-v2-highlights}

{{site.data.keyword.discoveryshort}} v2 offers the following features and enhancements:

- A project-based experience that supports many different use cases within a single environment.
- Built-in customization tools for adding dictionaries, patterns, and classifiers to help business users build projects that understand the language of their domain.
- Connectors to popular data sources that can quickly access valuable data where it resides.
- Smart Document Understanding that learns from the structure of human-readable documents, such as PDFs.
- Natural language query support across all document types, optimized with machine learning to find targeted answers.
- Advanced search capabilities, such as answer finding, curations, and table retrieval.
- An out-of-the-box contract understanding function that helps you search and interpret legal contracts.
- A full-featured Content Mining application that you can use to conduct in-depth analysis of unstructured text.
- Customizable user interface components that help you to deploy custom applications.

For more information, see [Migrating to {{site.data.keyword.discoveryshort}} v2](/docs/discovery-data?topic=discovery-data-migrate-to-v2).

## Comparing v1 and v2 features
{: #version-choose-comparison}

If you are already familiar with {{site.data.keyword.discoveryshort}} v1, learn more about how {{site.data.keyword.discoveryshort}} v2 compares.

{{site.data.keyword.discoveryshort}} v2 has new features that were previously unavailable. The following table describes feature support in both versions.

| Feature | Product redesign (v2) | Earlier version (v1) |
|---------|-----------------------|----------------------|
| Use projects to organize your work | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Use the Smart Document Understanding (SDU) to annotate your documents | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Leverage intuitive user interface tools to add domain-specific artifacts, such as dictionaries and custom machine learning models | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Create a content mining project type and then use the built-in Content Mining application to do in-depth data analysis (*{{site.data.keyword.icp4dfull_notm}}, Enterprise, and Premium plans only*) | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Perform real-time NLP with the Analyze API (*{{site.data.keyword.icp4dfull_notm}} and Enterprise plans only*) | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Apply a pretrained Smart Document Understanding model to your collection for similar benefits with less effort | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Process text from scanned documents or other images | ![checkmark icon](../icons/checkmark-icon.svg) |![checkmark icon](../icons/checkmark-icon.svg) |
| Extract meaning from tables | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Get insights from contracts (*{{site.data.keyword.icp4dfull_notm}}, Enterprise, and Premium plans only*) | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Apply the *Part of Speech* enrichment to your data | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Use the Entity Extraction, Document and Phrase Sentiment Analysis, and Keyword Extraction enrichments | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Use the Category classification, Concept tagging, Relation Extraction, Emotion Analysis, and Semantic Role Extraction, Sentiment of Keywords and Entities enrichments, which are available with the [Natural Language Understanding](/docs/natural-language-understanding?topic=natural-language-understanding-about){: external} service | | ![checkmark icon](../icons/checkmark-icon.svg) |
| Build a custom entity type system | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Apply Watson Knowledge Studio NLP models to your data | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Support for more connectors from a {{site.data.keyword.icp4dfull_notm}} deployment, including databases, file systems, FileNet P8, and HCL Notes | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Some connectors support document-level security from a {{site.data.keyword.icp4dfull_notm}} deployment | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Programmatically configure external data source crawls | | ![checkmark icon](../icons/checkmark-icon.svg) |
| Configure the normalization process of ingestion by document type. Configuration options include things like document segmentation, HTML file inclusion or exclusion rules, and JSON normalization | | ![checkmark icon](../icons/checkmark-icon.svg) |
| Configure dictionary tokenization | | ![checkmark icon](../icons/checkmark-icon.svg) |
| Advanced question-answering capabilities, such as returning the exact answer | ![checkmark icon](../icons/checkmark-icon.svg) | |
| {{site.data.keyword.discoveryshort}} Query Language (DQL) API support | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Retrieve passages from documents | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Perform relevancy training to improve query results | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Configure continuous relevancy training | | ![checkmark icon](../icons/checkmark-icon.svg) |
| Retrieve tables | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Query result deduplication | | ![checkmark icon](../icons/checkmark-icon.svg) |
| Identify document similarity in query results | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Indicate a preference (bias) in queries | | ![checkmark icon](../icons/checkmark-icon.svg) |
| Review query logging and metrics | | ![checkmark icon](../icons/checkmark-icon.svg) |
{: row-headers}
{: class="comparison-table"}
{: caption="Feature support details" caption-side="top"}
{: summary="This table has row and column headers. The row headers identify features. The column headers identify the different versions of the product. To understand which features are supported by a product version, go to the row that describes the feature, and find the column for the product version that you are interested in."}

## Limit details
{: #plan-limit-links}

For more information about artifact limits per plan, see the feature documentation:

-   [Advanced rules model limits](/docs/discovery-data?topic=discovery-data-domain-pattern#advanced-rules-limits)
-   [Classifier limits](/docs/discovery-data?topic=discovery-data-domain-classifier#classifier-limits)
-   [Collection limits](/docs/discovery-data?topic=discovery-data-collections#collections-limits)
-   [Dictionary limits](/docs/discovery-data?topic=discovery-data-domain-dictionary#dictionary-limits)
-   [Document limits](/docs/discovery-data?topic=discovery-data-collections#collections-doc-limits)
-   [Entity extractor limits](/docs/discovery-data?topic=discovery-data-entity-extractor#entity-extractor-limits)
-   [Machine Learning model limits](/docs/discovery-data?topic=discovery-data-domain-ml#machinelearning-limits)
-   [Pattern limits](/docs/discovery-data?topic=discovery-data-domain-pattern#patterns-limits)
-   [Project limits](/docs/discovery-data?topic=discovery-data-projects#projects-limits)
-   [Query limits](/docs/discovery-data?topic=discovery-data-query-concepts#query-limits)
-   [Regular expression limits](/docs/discovery-data?topic=discovery-data-domain-regex#regex-limits)
-   [SDU limits](/docs/discovery-data?topic=discovery-data-configuring-fields#sdu-limits)

The following limits apply only to Content Mining project types:

-   [Document classifier limits](/docs/discovery-data?topic=discovery-data-cm-doc-classifier#doc-classifier-limits)
-   [Regular expression pattern limits](/docs/discovery-data?topic=discovery-data-cm-custom-annotator#regex-limits)

To check the current status of the limits and usage for your plan type, you can open the *Plan limits and usage* page at any time. 

1.  From the product page header, click the user icon ![User icon](images/user--avatar.svg). 

    The *Usage* section shows a short summary. 
1.  Click **View all** to see usage information for all of the plan limit categories. 

To leave the page, click the web browser back button or the *My Projects* tab.
