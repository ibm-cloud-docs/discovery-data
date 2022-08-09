---

copyright:
  years: 2019, 2022
lastupdated: "2022-08-09"

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

    If {{site.data.keyword.discoveryshort}} cannot discern a consistent and valid pattern based on the information you provided, the **Save pattern** button is never enabled. A pattern might not be created if you provide contradictory examples, for example. To start over, click the **Reset** button. The documents are returned to their original state and any examples that you identified previously are removed.
    {: note}

1.  To apply the pattern immediately, choose the collection and field where you want to apply the enrichments from the model, and then click **Apply**.

When Discovery finds text in a document that matches a pattern that you defined, it is annotated in the `enriched_{fieldname}.entities` field. You can find it by checking the `enriched_{fieldname}.entities.model_name` field for your pattern name.

## Downloading a pattern
{: #patterns-download}

To download a pattern, complete the following step:

1.  In the **Patterns view**, click the download icon.

    A pattern model is downloaded as a ZIP file.

You can import the downloaded ZIP file as the source for an advanced rules model resource. For more information, see [Advanced rules models](/docs/discovery-data?topic=discovery-data-domain-advanced-rules).

### Pattern limits
{: #patterns-limits}

The number of patterns that you can define per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Patterns per service instance |
|--------------|--------------------------------:|
| Premium      |                             100 |
| Enterprise |                               100 |
| Plus (includes Trial)  |                    20 |
{: caption="Pattern plan limits" caption-side="top"}
