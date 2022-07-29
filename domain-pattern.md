---

copyright:
  years: 2019, 2022
lastupdated: "2022-07-29"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Patterns ![IBM Cloud only](images/ibm-cloud.png)
{: #domain-pattern}

Recognize terms that are mentioned in sentences that match a syntactic pattern that you teach {{site.data.keyword.discoveryshort}} to recognize.
{: shortdesc}

Patterns is a beta feature that is available in managed deployments only. The feature is available for English-language documents only.
{: beta}

Add a Patterns resource to teach {{site.data.keyword.discoveryshort}} to recognize patterns in your data. The Patterns feature uses pattern induction, which generates extraction patterns from examples that you provide as training data. After you specify a few examples, {{site.data.keyword.discoveryshort}} suggests more rules that you can review and accept to complete the pattern.

Patterns produces a model by using a human-in-the-loop process. You aren't asked to build a large set of training data up front. Instead, you provide a few examples, and then participate in an interactive process to define the training data. You passively accept or reject smart suggestions that are proposed by the system.

Pattern recognition works best on text with consistent structure in casing, length, text, or numeric values. Examples of patterns you can teach {{site.data.keyword.discoveryshort}} to identify in your documents:

- Standards numbers, such as `ISO 45001`, `ISO 22000`.
- Currency references, such as `$50.5 million`, `$29 million`.
- Date references, such as `8 September 2019`, `12 June 2020`.

If you need to identify specific terms or text, such as product names, add a [dictionary](#dictionary).

Patterns cannot be used in a Content Mining application.
{: note}

For more information, read the following blog posts:

-   [Extracting Text Patterns with User Highlights with Pattern Induction](https://towardsdatascience.com/pattern-induction-what-is-a-pattern-part-1-79ee1bd5adc6)
-   [Pattern Induction: Best Practices for Extracting Text Patterns](https://maeda-han.medium.com/pattern-induction-best-practices-for-extracting-text-patterns-part-3-2c0ee6481a3c)

To define a pattern, complete the following steps:

1.  From the *Teach domain concepts* section of the *Improvement tools* panel, choose **Patterns**.
1.  Click **New**.
1.  Pick how you want to choose documents.

    - Allow {{site.data.keyword.discoveryshort}} to choose 10 random documents for you.
    - Choose the documents yourself (up to 20 can be selected).

      Each document must be under 5,000 characters in length. Documents that exceed the limit are truncated to 5,000 characters.

1.  Click **Next**.
1.  Start selecting example words or phrases that fit the pattern you want to define.

    For example, if you have a collection of articles that discuss `ISO` standards, you might start highlighting the numbers of the standards in each document.

    If you annotate something, and then change your mind, hover over the selection, and then click `x` to delete it.
1.  Continue selecting examples.

    After you identify enough examples, {{site.data.keyword.discoveryshort}} shows a list of suggested examples for you to review and determine to be valid or not valid examples. Suggested examples are taken from the field that is configured to be used in search results. If the source of result content is configured to be passages, the `text` field is used. For more information, see [Changing the result content](/docs/discovery-data?topic=discovery-data-query-results#query-results-content).

1.  Choose **Yes** or **No** for each suggestion.

    Click the **Preview document** icon if you want to see the example in context before you make a choice.
1.  Continue highlighting examples and validating suggestions until a message is displayed to inform you that you identified enough examples.
1.  Click the **Review examples** tab to review the lists of examples that were identified by you and {{site.data.keyword.discoveryshort}}.
1.  If the examples are correct, click **Save pattern**.
1.  To apply the pattern immediately, choose the collection and field where you want to apply the enrichments from the model, and then click **Apply**.

If {{site.data.keyword.discoveryshort}} cannot discern a consistent and valid pattern based on the information you provided, the **Save pattern** button is never enabled. A pattern might not be created if you provide contradictory examples, for example. To start over, click the **Reset** button. The documents are returned to their original state and any examples that you identified previously are removed.
{: note}

To download a pattern, complete the following step:

1.  In the **Patterns view**, click the download icon.

    A pattern model is downloaded as a ZIP file.

You can import the downloaded ZIP file as the source for an advanced rules model resource. For more information, see [Advanced rules models](#advanced-rules).

### Pattern limits
{: #patterns-limits}

The number of patterns that you can define per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Patterns per service instance |
|--------------|--------------------------------:|
| Premium      |                             100 |
| Enterprise |                               100 |
| Plus (includes Trial)  |                    20 |
{: caption="Pattern plan limits" caption-side="top"}

### Advanced rules models
{: #advanced-rules}

Add an advanced rules model to apply a text extraction model that was created and exported from the Advanced Rule editor of {{site.data.keyword.knowledgestudiofull}} to your collection.

Your model must be created with the appropriate {{site.data.keyword.knowledgestudioshort}} deployment:

- ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: You can add models that were created with an instance of {{site.data.keyword.knowledgestudiofull}} that is hosted on {{site.data.keyword.icp4dfull}} or {{site.data.keyword.cloud_notm}}.
- ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: You can add models that were created with a {{site.data.keyword.knowledgestudiofull}} instance that is hosted on {{site.data.keyword.cloud_notm}} only.

{{site.data.keyword.knowledgestudioshort}} support for building models with the beta Advanced Rules Editor in instances that are managed by {{site.data.keyword.cloud_notm}} ended on 30 June 2022. Any rules models that were exported from {{site.data.keyword.knowledgestudioshort}} before that date can continue to be run in {{site.data.keyword.discoveryshort}}.
{: note}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: As an alternative to using a model that is generated by the {{site.data.keyword.knowledgestudioshort}} Advanced Rules Editor, you can define a rule by [adding a Patterns enrichment](#patterns).

To add an advanced rule model, complete the following steps:

1.  Create the model and export the ZIP file that contains the model resources from {{site.data.keyword.knowledgestudiofull}}.

    For more information, see the following documentation:

    - [{{site.data.keyword.knowledgestudioshort}} for {{site.data.keyword.icp4dfull}}](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-create-advanced-rules-model)
    - [{{site.data.keyword.knowledgestudioshort}} for {{site.data.keyword.cloud_notm}}](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-create-advanced-rules-model)

1.  From the *Teach domain concepts* section of the *Improvement tools* panel, choose **Advanced rules model**.
1.  Click **Upload**.
1.  Specify a name for the model, and then choose the language that was used to define the model.
1.  Specify a name for the result field, which is the field in the index where the output of this enrichment will be stored.
1.  Click **Upload** to browse for the ZIP file that you exported earlier.
1.  Click **Create**.
1.  Choose the collection and field where you want to apply the enrichments from the model, and then click **Apply**.

### Advanced rules model limits
{: #advanced-rules-limits}

The number of advanced rules models that you can define per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Advanced rules models per service instance |
|--------------|--------------------------------:|
| Cloud Pak for Data  |                Unlimited |
| Premium  |                      3 |
| Enterprise |                                3 |
| Plus (includes Trial) |                     1 |
{: caption="Pattern plan limits" caption-side="top"}
