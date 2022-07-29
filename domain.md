---

copyright:
  years: 2019, 2022
lastupdated: "2022-07-29"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Adding custom enrichments
{: #domain}

Add resources that can teach {{site.data.keyword.discoveryshort}} about terms or patterns that have special meaning to your application.
{: shortdesc}

The following table shows you the correct resources to add to address common needs.

| Goal | Resource | Notes |
|------|----------|-------|
| Define categories by which your documents can be classified. | [Classifier](/docs/discovery-data?topic=discovery-data-domain-classifier) | N/A |
| Recognize terms and synonyms for terms that are significant to you, such as the names of products that you sell. | [Dictionary](/docs/discovery-data?topic=discovery-data-domain-dictionary) | Term suggestions are displayed if the *Parts of Speech* enrichment is applied to the collection. |
| Define regular expressions that capture patterns of significance, such as that `AB10045` is the syntax that is used for your order numbers. | [Regular expressions](/docs/discovery-data?topic=discovery-data-domain-regex) | N/A |
| Recognize and tag entities and relationships that are defined in a custom Machine Learning model. | [Machine Learning models](/docs/discovery-data?topic=discovery-data-domain-ml) | Requires a model that is built and exported from another IBM tool. |
| Apply rules to fields that are based on rules you defined by creating an advanced rule model in {{site.data.keyword.knowledgestudiofull}}. | [Advanced rule models](/docs/discovery-data?topic=discovery-data-domain-pattern#advanced-rules) |  Requires an advanced rule model that is built and exported from {{site.data.keyword.knowledgestudiofull}} or that uses an exported Patterns resource. |
| ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Recognize terms that are mentioned in sentences that match a syntactic pattern that you teach {{site.data.keyword.discoveryshort}} to recognize. | [Patterns (beta)](/docs/discovery-data?topic=discovery-data-domain-pattern) | Available as a beta feature for English-language collections in managed deployments only. The enrichment that is derived by defining patterns cannot be applied to Content Mining projects. You can export the resource and use it as an advanced rule model. |
| ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: Recognizes entities that you identify as being significant by training an entity extractor machine learning model. | [Entity extractor (beta)](/docs/discovery-data?topic=discovery-data-entity-extractor) | Available as a beta feature in managed deployments only. |
{: caption="Domain tools overview" caption-side="top"}

Dictionaries and classifiers that you add to one project can be used by other projects. In fact, you can add them to a Content Mining project from the deployed Content Mining application.

For more information about how to apply built-in enrichments to your collection, see [Applying prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu).

For more information about how to get the most from enrichments, read the [Enriching your documents can make search more effective](https://community.ibm.com/community/user/watsonai/blogs/bill-murdock1/2022/01/14/enriching-your-documents-can-make-search-more-effe){: external} blog post.

## Choosing the right enrichment type
{: #domain-choose-enrichment}

The following diagram helps you to choose the right enrichment for your use case.

![If you want to tag significant information in your data, find the right enrichment to use by answering these questions: Do you want to tag terms, passages, or documents? If passages or documents, create a classifier enrichment. If terms, are the terms expressed in a finite list? If yes, create a dictionary enrichment. If not, does the term syntax follow a pattern? If so, do all of the variations of the term fit a single pattern? If so, create a regular expression enrichment. If not, create a patterns enrichment which uses term examples that you provide to find patterns in term variations. If no set of patterns can capture the terms, create an entity extractor to identify terms based on the context in which they're used. ](images/enrichment-flowchart-plus-text-revision.drawio.png)

## Using enrichments together
{: #domain-enrichments-together}

You can use many enrichments together to tackle various challenges that you might encounter as you develop a search application. 

Many teams start by creating a **dictionary** enrichment. Dictionaries are a great tool for identifying important terms and tagging them so they can be retrieved later. Let's say you're building a search application that needs to extract ingredients from recipes. A dictionary enrichment can recognize mentions of most ingredients. However, the dictionary enrichment might partially match against two-word terms. For terms such as `olive oil` or `mustard greens`, it might incorrectly recognize only `olive` and `mustard` respectively. To improve the accuracy of the search, you can augment the dictionary enrichment with a **pattern** enrichment that can recognize two-word ingredient mentions. Maybe a small number of recipes mention food coloring codes in European format (`E104`). You can add a **regular expression** enrichment to recognize occurrences of codes with the syntax `E1nn`. Finally, to catch terms that no other enrichment can recognize, you can use a **machine learning** enrichment, either one that you build in an external tool and import to {{site.data.keyword.discoveryshort}}, or one that you build in {{site.data.keyword.discoveryshort}} by creating an **entity extractor** enrichment.

The entity extractor enrichment is more sophisticated than the other enrichments. For example, a dictionary enrichment recognizes only exact matches of dictionary terms and synonyms that occur in your documents. A regular expression enrichment recognizes only specific patterns. In contrast, occurrences of an entity are recognized based on the context in which an entity example is mentioned in a sentence.

For example, maybe you want to recognize locations and the document you want to process contains the following types of sentences:

-   I live in `Massachusetts`.
-   We're traveling from `New York City` to `Paris` next week.

To use a dictionary enrichment to recognize location names successfully, the dictionary must list every possible location. However, if you use an entity extractor enrichment, you can identify when a location is mentioned based on how the location is referenced in a sentence. With phrases such as, “I live in `x`” or “I'm from `x`” or “I'm traveling to `x`” in its training data, the entity extractor can learn that `x` is a reference to a location.

When you need to choose between using a dictionary or an entity extractor enrichment, follow these guidelines:

-   If the list of possible examples is short, use a dictionary.

    It is more efficient to define a dictionary term `planet` with synonyms such as `Earth` and `Saturn`, than to create a `planet` entity because only 8 planets exist in our solar system. However, defining a list of every possible location on Earth is not feasible. An entity extractor can recognize more location mentions.
-   If the list of possible examples is static, use a dictionary.

    Controversy over Pluto aside, the `planet` category is a good example here too because the list of planets in our solar system is static. Or maybe you want to monitor general customer sentiment about your products. You need to be able to recognize product name mentions, but might not need specifics. If you have a large variety of product names, you can create a `product name` entity. As new products are added to your portfolio, or product names change over time, you do not need to maintain an overall product list. The entity extractor can continue to recognize general feedback about your products based on the context of the sentences in which products are mentioned.

## Add a resource
{: #domain-task}

When you add a custom enrichment to a project it is available to any collection in the project.

To add a resource, complete the following steps:

1.  Open your project and go to the *Improve and customize* page.
1.  On the **Improvement tools** panel, expand **Teach domain concepts**, and then choose the resource that you want to add.

    After you create the resource, it becomes a new type of enrichment that you can apply to your data.
1.  Specify the collection and field in which to apply the enrichment.

    You can apply enrichments to the `text` and `html` fields, and to custom fields that were added from uploaded JSON or CSV files or from the Smart Document Understanding (SDU) tool.
    {: tip}

    For example, if you add a dictionary and choose to apply it to the `text` field of a collection, the documents in the collection are reprocessed. If the term `vehicle` is specified as a synonym of the `car` dictionary entry and occurs in the document text, `vehicle` is tagged as a mention of the `car` dictionary entry type. If a customer later searches for `car`, the passage that contains the `vehicle` mention is included in the search results.

    If the field that you choose comes from a JSON file, after you apply the enrichment, the field data type is converted to an array. The field is converted to an array even if it contains a single value. For example, `"field1": "Discovery"` becomes `"field1": ["Discovery"]`. Only the first 50,000 characters of a custom field from a JSON file are enriched.
    {: note}

You can choose to apply resource-derived enrichments to your data later. Enrichments that you add to a project are available for use from any collection in the project. Go to the *Manage collections* page, choose the collection where you want to apply the enrichment, and then open the **Enrichments** tab. Make sure the status of the enrichment shows that it is *Ready*, and then apply the enrichment to a field in the collection. For more information, see [Managing enrichments](/docs/discovery-data?topic=discovery-data-manage-enrichments).

From the deployed Content Mining application, you can create a classifier or a custom annotator from a dictionary, regular expression, Machine Learning, or PEAR file and use it as an enrichment in collections that are stored in other project types.
