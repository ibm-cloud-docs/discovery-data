---

copyright:
  years: 2019, 2021
lastupdated: "2021-06-29"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:beta: .beta}
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

# Adding domain-specific resources
{: #domain}

Add resources that can teach {{site.data.keyword.discoveryshort}} about terms or patterns that have special meaning to your application.
{: shortdesc}

The following table shows you the correct resources to add to address common needs.

| Goal | Resource | Notes |
|------|----------|-------|
| Define categories by which your documents can be classified. | [Classifier](#classifier) | N/A |
| Recognize terms and synonyms for terms that are significant to you, such as the names of products that you sell. | [Dictionary](#dictionary) | Term suggestions are displayed if the *Parts of Speech* enrichment is applied to the collection. |
| Define regular expressions that capture patterns of significance, such as that `AB10045` is the syntax that is used for your order numbers. | [Regular expressions](#regex) | N/A |
| Recognize and tag entities and relationships that are defined in a custom Machine Learning model. | [Machine Learning models](#machinelearning) | Requires a model that is built and exported from another IBM tool. |
| Apply rules to fields that are based on rules you defined by creating an advanced rule model in {{site.data.keyword.knowledgestudiofull}}. | [Advanced rule models](#advanced-rules) |  Requires an advanced rule model that is built and exported from {{site.data.keyword.knowledgestudiofull}} or that uses an exported Patterns resource. |
| ![IBM Cloud only](images/ibm-cloud.png) Recognize terms that are mentioned in sentences that match a syntactic pattern that you teach {{site.data.keyword.discoveryshort}} to recognize. | [Patterns (beta)](#patterns) | Available as a beta feature for English-language collections hosted on IBM Cloud only. The enrichment that is derived by defining patterns cannot be applied to Content Mining projects. You can export the resource and use it as an advanced rule model. |
{: caption="Domain tools overview" caption-side="top"}

Dictionaries and classifiers that you add to one project can be used by other projects. In fact, you can add them to a Content Mining project from the deployed Content Mining application.

For more information about how to apply built-in enrichments to your collection, see [Applying prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu).

## Add a resource
{: #domain-task}

To add a resource, complete the following steps:

1.  Open your project and go to the *Improve and customize* page. 
1.  On the **Improvement tools** panel, expand **Teach domain concepts**, and then choose the resource that you want to add.

    After you create the resource, it becomes a new type of enrichment that you can apply to your data.
1.  Specify the collection and field in which to apply the enrichment. 

    You can apply enrichments to the `text` and `html` fields, and to custom fields that were added from uploaded JSON or CSV files or from the Smart Document Understanding (SDU) tool. You cannot apply enrichments to fields that begin with `extracted_metadata`, `enriched_`, or `metadata`.
    {: tip}

    For example, if you add a dictionary and choose to apply it to the `text` field of a collection, the documents in the collection are reprocessed. If the term `vehicle` is specified as a synonym of the `car` dictionary entry and occurs in the document text, `vehicle` is tagged as a mention of the `car` dictionary entry type. If a customer later searches for `car`, the passage that contains the `vehicle` mention is included in the search results.

You can choose to apply resource-derived enrichments to your data later. Go to the *Manage collections* page, choose the collection where you want to apply the enrichment, and then open the **Enrichments** tab. Make sure the status of the enrichment shows that it is *Ready*, and then apply the enrichment to a field in the collection.

From the deployed Content Mining application, you can create a classifier or a custom annotator from a dictionary, regular expression, Machine Learning, or PEAR file and use it as an enrichment in collections that are stored in other project types.

## Classifier
{: #classifier}

Add a classifier to assign documents in your collection into categories. {{site.data.keyword.discoveryshort}} uses the labels and text examples that you provide to predict the categories of documents in your collection.

1.  Create a CSV file that contains example text followed by its category label per line.

    The CSV file must be in UTF-8 encoding format and must meet the following requirements:

    -  The format must be `text,label`. The `text` is the example text, and the `label` is the category name. 
    
       You can add more `label` columns if you need to apply more than one label to the sentence in the `text` column. For example, `text,label,label`.
    -  The file must have at least two columns with no header.
    -  Add at least 10 entries for each category that you want to define. The minimum number of entries that are required per category is 3. The more examples that you provide for each category, the better the classifier can predict the categories of other content in your collection.

    The following example is a CSV file that defines two categories, named `facility_temperature` and `catering`. The example text consists of feedback from conference attendees.

    ```
    The rooms were too cold.,facility_temperature
    Breakfast did not include gluten-free options.,catering
    The rooms were too warm.,facility_temperature
    I was very comfortable in the session rooms.,facility_temperature
    The awards dinner was delicious.,catering
    Coffee ran out during one of the breaks.,catering
    The temperature was not comfortable.,facility_temperature
    I was very happy with the selection at lunch.,catering
    It was nice that you provided tea and coffee. Tea drinkers are often ignored.,catering
    Can you turn up the air conditioning? I was very warm.,facility_temperature
    My teeth were chattering because I was so cold.,facility_temperature
    The speaker left the room to find someone to adjust the temperature.,facility_temperature
    Would you consider an all-vegan menu next year?,catering
    I would like lemonade and iced tea to be served during the breaks.,catering
    The lunch staff was excellent.,catering
    Appreciated the fresh blueberry muffins at breakfast.,catering
    The hotel staff adjusted the temperature in my session room as soon as I asked. Excellent service!,facility_temperature
    Every meal was delicious and there was something for everyone.,catering
    The seats under the skylights were not comfortable. Too hot.,facility_temperature
    I was comfortable everywhere in the conference center. I never needed my emergency sweater.,facility_temperature
    ```
    {: codeblock}

1.  From the *Teach domain concepts* section of the *Improvement tools* panel, choose **Classifiers**.
1.  Click **Upload**.
1.  Specify a name for the classifier, and then choose the language that was used in the CSV file.
1.  Click **Upload** to browse for the CSV file that you created earlier.
1.  Click **Create**.

    A classifier enrichment is created based on the training data that you provided.
1.  Choose the collection and field where you want to apply the enrichment, and then click **Apply**.

In the output, the classifier enrichment applies the `facility_temperature` label to the document in the collection. The `label` is stored in the `enriched_{field_name}` array, within the `classes` array.

```json
{
  "enriched_text": [
    {
      "classes": [
        {
          "confidence": 0.999692440032959,
          "label": "facility_temperature"
        }
      ]
    }
  ],
  "text": [
    "I think more attendees would stay awake in the sessions if the rooms were colder."
  ]
}
```
{: codeblock}

The classifier that you add from the {{site.data.keyword.discoveryshort}} user interface is a *text classifier*. A text classifier can classify documents based on Parts of Speech information only. You can create another classifier type, a *document classifier*, only from the deployed Content Mining application. A document classifier can classify documents based on Parts of Speech information and metadata that is added by other enrichments that are applied to the collection. If you want to apply a document classifier to a collection in a project type other than a Content Mining project, you must create the classifier in the deployed Content Mining application and export it. You can then import the classifier and apply it to your collection as an enrichment. For more information, see [Creating and applying a document classifier](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-contentminerapp#create-doc-classifier).

### Classifier limits
{: #classifier-limits}

The number of text classifiers and labels that you can create per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Limit   | Plus | Premium | Cloud Pak for Data |
|---------|-------------------:|--------:|--------:|
| Number of text classifiers per service instance | 5 | 20 | Unlimited |
| Number of labeled data rows | 2,000 | 20,000 | 20,000 |
| Size of labeled data file (in MB) | 16 | 1,024 | 1,024 |
| Number of labels | 100 | 1,000 | 1,000 |
{: caption="Text classifier plan limits" caption-side="top"}

## Dictionary
{: #dictionary}

Help {{site.data.keyword.discoveryshort}} find terms that have meaning to your use case by adding a dictionary. You can define multiple synonyms for a term or a set of words in the same category.

You can create a dictionary by adding the terms one by one or by uploading a CSV file that lists the terms.

To add dictionary terms one by one, complete the following steps:

1.  From the *Teach domain concepts* section of the *Improvement tools* panel, choose **Dictionaries**.
1.  Click **New**.
1.  Name your dictionary and choose the language.
1.  Optional: Expand Advanced options, and specify a facet path to categorize any text that matches the dictionary entry. The text can be filtered by this facet later. 

    If you use a hierarchy of categories, add a period between category names in the facet path to represent the hierarchy. For example, `automobiles.motorsports`.
1.  Enter a term, and then select the **+** button to add it.

1.  To add synonyms for the term, click the *Edit* icon, and then enter synonyms in the **Other terms** field. Separate multiple synonyms with a comma. Click **Save term**.

1.  Continue adding terms.

    Similar terms from your collection are suggested as new entries.

    Term suggestions are not displayed if the **Parts of Speech** enrichment is not enabled.
    {: note}
1.  Click **Save dictionary**.
1.  Choose the collections and fields where you want to apply the dictionary, and then click **Apply**.

To add dictionary from a CSV file, complete the following steps:

1.  Create a CSV file that contains the dictionary terms that you want to add.

    Use UTF-8 encoding. Specify one entry per line.

    - To define a set of synonymous terms, use the following syntax:

      ```
      <term>,<synonym>,<synonym>,<synonym>
      ```

      For example:

      ```
      car,automobile,vehicle,sedan,convertible,station wagon
      ```

      The enrichment that is created is named after the first term per line. 
      
      For example, the entry in this example creates an enrichment that is named `car`. When the enrichment is applied to a document, any mentions of `car`, `automobile`, `vehicle`, `sedan`, `convertible`, or `station wagon` are tagged as instances of the `car` enrichment.

    - To define a set of terms in the same category, use the following syntax:

      ```
      <category>,<related-term>,<related-term>
      ```

      For example:

      ```
      engine,gasket,carburetor,piston,valves
      ```

      The entry in this example creates an enrichment that is named `engine`. When the enrichment is applied to a document, any mentions of `engine`,`gasket`,`carburetor`,`piston`, or `valves` are tagged as instances of the `engine` enrichment.

1.  From the *Teach domain concepts* section of the *Improvement tools* panel, choose **Dictionaries**.
1.  Click **Upload**.
1.  Name your dictionary and choose the language that was used in the CSV file.
1.  Optional: Expand Advanced options, and specify a facet path to categorize any text that matches the dictionary entry. The text can be filtered by this facet later. 

    If you use a hierarchy of categories, add a period between category names in the facet path to represent the hierarchy. For example, `automobiles.motorsports`.
1.  Click **Upload** to browse for the CSV file that you created earlier.
1.  Click **Create**.
1.  Choose the collections and fields where you want to apply the dictionary, and then click **Apply**.

In the following example, the **Facet Path** is `automobiles.motorsports`, and the field that is selected for enrichment is `text`. The dictionary enrichment in the `enriched_{field_name}` array, within the `entities` array.

```json
{
  "enriched_text": [
    {
      "entities": [
        {
          "path": ".automobiles.motorsports",
          "type": "motorsports",
          "text": "engine"
        }
      ]
    }
  ],
  "text": [
    "I prefer a carburetor to fuel-injection."
  ]
}
```
{: codeblock}

As a result, if someone searches for the term `engine`, {{site.data.keyword.discoveryshort}} finds any passages that are tagged with the `enriched_{field_name}.entities.text:engine` enrichment. Source documents that contain a reference to a `carburetor` or `pistons` are returned in addition to the documents that mention `engine` specifically. 

### Dictionary limits
{: #dictionary-limits}

The number of dictionaries and term entries you can create per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan      | Number of dictionaries per service instance | Number of term entries per dictionary | Number of terms for which suggestions can be generated |
|-----------|-------------------:|------------------------:|--------------------------:|
| Cloud Pak for Data | Unlimited | Unlimited | 1,000 |
| Premium | 100 | 10,000 | 1,000 |
| Plus (includes Trial) | 20 | 1,000 | 50 |
{: caption="Dictionary plan limits" caption-side="top"}

## Regular expressions
{: #regex}

Define regular expressions that can identify and extract information from fields in your collection.

For example, this regular expression finds occurrences of credit card numbers of a specific format and length. 

```
4[0-9]{15}
```

To add a regular expression, complete the following steps:

1.  From the *Teach domain concepts* section of the *Improvement tools* panel, choose **Regular expression**.
1.  Click **Upload**.
1.  Optional: Specify a facet path to categorize any text that matches the regular expression. The text can be filtered by this facet later. 

    If you use a hierarchy of categories, add a period between category names in the facet path to represent the hierarchy. For example, if you are adding a regex that can recognize phone numbers, you might have a facet path such as `international.europe`.
1.  Add the regular expression.

    - Use a Java&trade; regular expression. 

      For more information, see the [Java documentation](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html){: external}. Another useful resource is [Regex 101](https://regex101.com/){: external}.
    - Keep the regular expression as short and understandable as possible.
    - The best regular expressions resolve to a match or non-match quickly.
    - Use common patterns. For example, use `a(b|c|d)` instead of `(ab|ac|ad)`.
    - The regular expression engine might fail if it backtracks because it can't make a negative match toward the end of the string and then attempts too many permutations. To prevent backtracks, consider using a possessive quantifier, such as `(a+b*)++c`.
1.  Click **Create**.
1.  Choose the collection and field to search for occurrences of text that matches this regular expression pattern.


In the output, the information that is extracted by the regular expression enrichment can be found under `enriched_{field_name}`, within the `entities` array.

In this example, the **Facet Path** is `regex.cccardnumber`, and the field that is selected for enrichment is `text`.

```json
{
  "enriched_text": [
    {
      "entities": [
        {
          "path": ".regex.cccardnumber",
          "type": "cccardnumber",
          "text": "4000000000000000"
        }
      ]
    }
  ],
  "text": [
    "He has 2 phones, 090-1234-5678 and 080-1234-5678. His credit card number is 4000000000000000."
  ]
}
```
{: codeblock}

As a result, a customer can filter their results by the credit card number facet that you defined to show passages that include credit card number references.

### Regular expression limits
{: #regex-limits}

The number of regular expressions that you can define per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Regular expressions per service instance |
|--------------|--------------------------------:|
| Cloud Pak for Data |                 Unlimited |
| Premium      |                             100 |
| Plus (includes Trial) |                     20 |
{: caption="Regular expression plan details" caption-side="top"}

## Machine Learning models
{: #machinelearning}

Add Machine Learning models that you created with IBM tools that you can use to define your own type system.

The type of models you can add depend on your deployment:

- ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: You can add models that were created with Watson Explorer Content Analytics Studio models, or with an instance of {{site.data.keyword.knowledgestudiofull}} that is hosted on {{site.data.keyword.icp4dfull}} or {{site.data.keyword.cloud_notm}}.
- ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: You can add models that were created with a {{site.data.keyword.knowledgestudiofull}} instance that is hosted in {{site.data.keyword.cloud_notm}} only.

The following types of models are supported:

-  Rule-based models created in {{site.data.keyword.knowledgestudioshort}} that find entities in documents based on rules that you define. (File format: `.pear`)
-  Machine learning models created in {{site.data.keyword.knowledgestudioshort}} that understand the linguistic nuances, meaning, and relationships specific to your industry (file format: `.zip`)
-  ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: Custom UIMA text analysis models created in Watson Explorer Content Analytics Studio. (File format: `.pear`)

To add a Machine Learning model, complete the following steps:

1.  Create the model and export it from the tool you use to create it.

    For more information, see the following documentation:

    -  {{site.data.keyword.knowledgestudioshort}} for {{site.data.keyword.icp4dfull}}

      -  [Creating a rule-based model](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-rule-annotator)
      -  [Creating a machine learning model](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-ml_annotator)
    -  {{site.data.keyword.knowledgestudioshort}} for {{site.data.keyword.cloud_notm}}
      -  [Creating a rule-based model](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-rule-annotator)
      -  [Creating a machine learning model](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-ml_annotator)
    -  [Watson Explorer Content Analytics Studio](https://www.ibm.com/docs/en/watson-explorer/12.0.x?topic=analytics-content-studio-advanced-text){: external} 
    
        You must export the model from Watson Explorer Content Analytics Studio as a UIMA PEAR file. For more information, see: [Creating Custom PEAR Files for use with Lexical Analysis Streams](https://www.ibm.com/docs/en/watson-explorer/12.0.x?topic=las-creating-custom-pear-files-use-lexical-analysis-streams){: external}.

1.  From the *Teach domain concepts* section of the *Improvement tools* panel, choose **Machine learning**.
1.  Specify a name for the model, and then choose the language that was used to define the model.
1.  Click **Upload** to browse for the .pear or .zip file that you exported earlier.
1.  Click **Create**.
1.  Choose the collection and field where you want to apply the enrichments from the model, and then click **Apply**.

### Rule-based model example
{: #machinelearning-rules}

For example, when a machine learning model is applied as an enrichment to a field, it extracts all entity types in that field that were specified in a {{site.data.keyword.knowledgestudioshort}} rule-based model. If the model recognizes entity types such as `person`, `surname`, and `job title` they are recognized in your documents and tagged.

In the output, the information that is extracted by the Machine Learning enrichment in the `enriched_{field_name}` array, within the `entities` array. In this example, the field that is selected for enrichment is `text`.

```json
{
  "enriched_text": [
    {
      "entities": [
        {
          "path": ".wksrule.entities.PERSON",
          "text": "George Washington",
          "type": "PERSON"
        },
        {
          "path": ".wksrule.entities.GIVENNAME",
          "text": "George",
          "type": "GIVENNAME"
        },
        {
          "path": ".wksrule.entities.SURNAME",
          "text": "Washington",
          "type": "SURNAME"
        },                    
        {
          "path": ".wksrule.entities.POSITION",
          "text": "politician",
          "type": "POSITION"
        },
        {
          "path": ".wksrule.entities.POSITION",
          "text": "soldier",
          "type": "POSITION"
        },
        {
          "path": ".wksrule.entities.JOBTITLE",
          "text": "President of the United States",
          "type": "JOBTITLE"
        }
      ],
      "text": [
        "George Washington (February 22, 1732‚ December 14, 1799) was an American politician and soldier who served as the first President of the United States from 1789 to 1797 and was one of the Founding Fathers of the United States."
      ]
    }
  ]
}
```
{: codeblock}

As a result, if someone [uses the API](/docs/discovery-data?topic=discovery-data-query-concepts) to submit a Discovery Query Language query to look for occurrences of the `enriched_{field_name}.entities.type:jobtitle` enrichment, any passages that discuss a person's job title are returned.

### Machine learning model example
{: #machinelearning-ml}

In this example, a Machine learning model extracts entity types such as `person`, `oranization`, and `date`, and information about relationships between the entities. When this ML model is applied as an enrichment to a field, it uses machine learning to understand the linguistic nuances, meaning, and relationships that are mentioned in the document.

In the output, the information that is extracted by the Machine Learning enrichment in the `enriched_{field_name}` array, within the `entities` and the `relations` arrays. In this example, the field that is selected for enrichment is `text`.

```json
{
  "enriched_text": [
    {
      "entities": [
        {
          "count": 1,
          "text": "Democratic Party",
          "type": "ORGANIZATION"
        },
        {
          "count": 1,
          "text": "March 15, 1767",
          "type": "DATE"
        },
        {
          "count": 1,
          "text": "President",
          "type": "POSITION"
        },
        {
          "count": 1,
          "text": "Andrew Jackson",
          "type": "PERSON"
        }
      ],
      "relations": [
        {
          "sentence": "Andrew Jackson (March 15, 1767‚ June 8, 1845) was an American soldier and statesman who served as the seventh President of the United States from 1829 to 1837 and was the founder of the Democratic Party."
        }
      ]
    }
  ]
}
```
{: codeblock}

### Machine learning model limits
{: #machinelearning-limits}

The number of Machine Learning (ML) models you can create per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan      | ML models per service instance |
|-----------|-------------------:|
| Cloud Pak for Data | Unlimited |
| Premium | 10 |
| Plus (includes Trial) | 3 |
{: caption="ML model plan limits" caption-side="top"}

## Advanced rules models
{: #advanced-rules}

Add an advanced rules model to apply a text extraction model that was created and exported from the Advanced Rule editor of {{site.data.keyword.knowledgestudiofull}} to your collection.

Your model must be created with the appropriate {{site.data.keyword.knowledgestudioshort}} deployment:

- ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: You can add models that were created with an instance of {{site.data.keyword.knowledgestudiofull}} that is hosted on {{site.data.keyword.icp4dfull}} or {{site.data.keyword.cloud_notm}}.
- ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: You can add models that were created with a {{site.data.keyword.knowledgestudiofull}} instance that is hosted in {{site.data.keyword.cloud_notm}} only.

To add an advanced rule model, complete the following steps:

1.  Create the model and export the ZIP file that contains the model resources from {{site.data.keyword.knowledgestudiofull}}.

    For more information, see the following documentation:

    - [{{site.data.keyword.knowledgestudioshort}} for {{site.data.keyword.icp4dfull}}](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-create-advanced-rules-model)
    - [{{site.data.keyword.knowledgestudioshort}} for {{site.data.keyword.cloud_notm}}](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-create-advanced-rules-model)
    - ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: You can define a rule by [adding a Patterns resource](#patterns), and then export the resource as a ZIP file.
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
| Plus (includes Trial) |                     1 |
{: caption="Pattern plan limits" caption-side="top"}

## Patterns ![IBM Cloud only](images/ibm-cloud.png)
{: #patterns}

Patterns is a beta feature that is available in {{site.data.keyword.cloud_notm}} deployments only. The feature is available for English-language documents only.
{: beta}

Add a Patterns resource to teach {{site.data.keyword.discoveryshort}} to recognize patterns in your data. The Patterns feature uses pattern induction, which generates extraction patterns from examples that you provide as training data. After you specify a few examples, {{site.data.keyword.discoveryshort}} suggests more rules that you must review and accept to complete the pattern. 

Pattern recognition works best on text with consistent structure in casing, length, text, or numeric values. Examples of patterns you can teach {{site.data.keyword.discoveryshort}} to identify in your documents:

-  Standards numbers, such as `ISO 45001`, `ISO 22000`.
-  Currency references, such as `$50.5 million`, `$29 million`.
-  Date references, such as `8 September 2019`, `12 June 2020`.

If you need to identify specific terms or text, such as product names, add a [dictionary](#dictionary).

Patterns cannot be used in a Content Mining application.  
{: note}

To define a pattern, complete the following steps:

1.  From the *Teach domain concepts* section of the *Improvement tools* panel, choose **Patterns**.
1.  Click **New**.
1.  Pick how you want to choose documents. 

    - Allow {{site.data.keyword.discoveryshort}} to choose 10 random documents for you.
    - Choose the documents yourself (up to 20 can be selected).
    
      Each document must be under 5,000 characters in length. Documents that exceed the limit are truncated to 5000 characters. 
      
1.  Click **Next**.
1.  Start selecting example words or phrases that fit the pattern you want to define. 

    For example, if you have a collection of articles that discuss `ISO` standards, you might start highlighting the numbers of the standards in each document.

    If you annotate something, and then change your mind, hover over the selection, and then click `x` to delete it.
1.  Continue selecting examples. 

    After you identify enough examples, {{site.data.keyword.discoveryshort}} shows a list of suggested examples that you can review and confirm are valid examples. Choose **Yes** or **No** for each suggestion. Click the **Preview document** icon if you want to confirm the example in context. 
1. Continue highlighting examples and validating suggestions until a message is displayed to inform you that you identified enough examples.
1. Click the **Review examples** tab to review the lists of examples that were identified by you and {{site.data.keyword.discoveryshort}}.
1. If the examples are correct, click **Save pattern**.
1. To apply the pattern immediately, choose the collection and field where you want to apply the enrichments from the model, and then click **Apply**.

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
| Plus (includes Trial)  |                    20 |
{: caption="Pattern plan limits" caption-side="top"}
