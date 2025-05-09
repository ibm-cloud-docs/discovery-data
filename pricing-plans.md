---

copyright:
  years: 2021, 2025
lastupdated: "2024-02-15"

keywords: plans, pricing, service instances, billing

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.discoveryshort}} pricing plans
{: #pricing-plans}


Learn more about the {{site.data.keyword.discoveryfull}} service plans, so you can pick the plan type that best meets your needs.
{: shortdesc}

## Plus
{: #plusplan}

Find targeted answers and insights across many document types.

The first Plus plan that is created includes a 30-day trial at no cost.
You must pay for each additional Plus plan (and for use of the first plan after the 30-day trial ends).

If you continue to use a Plus plan service instance after the 30-day trial ends, you are charged for it. To avoid being charged after 30 days, you must delete the Plus plan service instance.
{: important}

### What's included
{: #plusplan-features}

For subscription accounts, the monthly fee per instance is $500.

The plan includes the following features:

-   10,000 documents per month ($50 for every additional 1,000 documents per month)
-   10,000 queries per month ($20 for every additional 1,000 queries per month)
-   Up to 5 queries per second
-   Optical Character Recognition(OCR)
-   Out of the box data source connectors
-   Table Retrieval
-   Custom NLP models
-   Custom Relevance Model
-   Entity extractor

### Artifact limits
{: #plusplan-limits}

-   Up to 500,000 queries per month
-   Up to 500,000 documents
-   Up to 20 projects
-   Up to 40 collections (Up to 5 collections per project)
-   Up to 10 MB document size
-   Up to 3 custom models [Learn more](#custom-models)
-   Up to 40 custom fields for Smart Document Understanding model and model import and export
-   Up to 20 custom dictionaries
-   Up to 20 custom pattern extraction models
-   Up to 20 custom regular expression models
-   Up to 20 custom text classification models

## Enterprise
{: #enterpriseplan}

Scale and secure your {{site.data.keyword.discoveryshort}} application with enterprise-grade support and performance, and address more use cases including contract analysis and content mining to explore insights across documents.

### What's included
{: #enterpriseplan-features}

For subscription accounts, the monthly fee per instance is $5,000.

The plan includes the following features:

-   100,000 documents per month ($5 for every additional 1,000 documents per month)
-   100,000 query or analyze API calls per month ($5 for every additional 1,000 calls per month)
-   Up to 3 custom models [Learn more](#custom-models)
-   Up to 10 entity extractor models
-   Up to 5 queries per second
-   Everything that's available in Plus
-   Analyze API
-   Content Intelligence
-   Content Mining
-   Document classification (Text classification is available in all plans. Document classification is available with Enterprise and higher-level plans only.)

Your bill labels requests that are generated from both query searches and analyze API calls as "Queries".
{: note}

### Artifact limits
{: #enterpriseplan-limits}

-   Unlimited queries per month
-   Unlimited documents
-   Up to 100 projects
-   Up to 300 collections (Up to 5 collections for all project types except Content Mining, which supports 1)
-   Up to 10 MB document size
-   Up to 10 custom {{site.data.keyword.knowledgestudioshort}} models
-   Up to 10 entity extractor models
-   Up to 100 custom fields for Smart Document Understanding model and model import and export
-   Up to 200 custom dictionaries
-   Up to 100 custom pattern extraction models
-   Up to 100 custom regular expression models
-   Up to 20 custom text classification models
-   Up to 20 custom document classification models

Autocompletion, curation, and notice requests are not billed in any plan type.
{: note}

## How is document pricing calculated?
{: #pricing-docs}

IBM uses the maximum number of documents per day and then prorates the document price to calculate the cost for a month.

For example, imagine that 300,000 documents are added to a collection in the first 6 days (6/30) of the month, and then another 1 million documents are added over a two-day span. In the first day (1/30) of the two-day span, 700,000 documents are added. All of the documents (1 million + 300,000 = 1,300,000) remain in the collection index for the rest of the month (23/30). The number of documents for the month might be calculated by using an equation like this: 

`300K * (6/30) + 700K * (1/30) + 1300K * (23/30)`

Document pricing counts the number of indexed documents in each collection. If you reuse data in a second collection, it generates a second set of documents in the index, which are counted separately.

For more information about what counts as a document, see [Document limits](/docs/discovery-data?topic=discovery-data-collections#collections-doc-limits).

## What is a custom model?
{: #custom-models}

Custom models include any of the following model types:

-   {{site.data.keyword.discoveryshort}} entity extractor
-   {{site.data.keyword.knowledgestudioshort}} machine learning
-   {{site.data.keyword.knowledgestudioshort}} rule-based

Advanced rules models are not counted as custom models.
{: note}

{{site.data.keyword.discoveryshort}} entity extractor models that are trained and published as an enrichment count toward the model limit for the plan. The entity extractor enrichment is what incurs charges, not the workspace or model. The entity extractor enrichment incurs charges whether or not it is applied to a collection.

## Premium
{: #premiumplan}

Premium plans offer developers and organizations a single tenant instance of one or more Watson services for better isolation and security. These plans offer compute-level isolation on the existing shared platform, as well as end-to-end encrypted data while in transit and at rest.

For more information, or to purchase a Premium plan, contact [Sales](https://ibm.biz/contact-wdc-premium){: external}.

## Other plans
{: #otherplans}

Features and limitations are similar between instances that you deploy on installed deployments in {{site.data.keyword.icp4dfull_notm}} and Premium plan instances that are managed by {{site.data.keyword.cloud_notm}}.

## Additional information
{: #pricingadd}

-   For more information about how queries are counted, see [Query limits](/docs/discovery-data?topic=discovery-data-query-concepts#query-limits).
-   For more information about pricing or to create a service instance, see the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog/services/watson-discovery){: external}.

{{site.data.keyword.cloud_notm}} resources:

-   [How you're charged](/docs/billing-usage?topic=billing-usage-charges){: external}.
-   [{{site.data.keyword.cloud_notm}} Cost estimator](https://cloud.ibm.com/estimator/review){: external}
-   [{{site.data.keyword.cloud_notm}} Services terms](https://www-03.ibm.com/software/sla/sladb.nsf/sla/saas?OpenDocument){: external}
-   For more information about {{site.data.keyword.cloud_notm}} security, see [IBM terms](https://www.ibm.com/support/customer/csol/terms/){: external}.
