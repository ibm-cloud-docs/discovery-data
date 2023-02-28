---

copyright:
  years: 2019, 2023
lastupdated: "2023-02-28"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Use imported ML models to find custom terms
{: #domain-ml}

Use custom Machine Learning models that use rules or context to recognize and tag entities.
{: shortdesc}

Add Machine Learning models that you created with IBM tools that you can use to define your own type system.

The type of models you can add depend on your deployment:

-   [IBM Cloud Pak for Data]{: tag-cp4d} You can add models that were created with Watson Explorer Content Analytics Studio models, or with an instance of {{site.data.keyword.knowledgestudiofull}} that is hosted on {{site.data.keyword.icp4dfull}} or {{site.data.keyword.cloud_notm}}. Starting with the 4.6.2 release, you can also add custom entity extractor models that were created in and exported from another instance of {{site.data.keyword.discoveryshort}}.
-   [IBM Cloud]{: tag-ibm-cloud} You can add models that were created with a {{site.data.keyword.knowledgestudiofull}} instance that is hosted in {{site.data.keyword.cloud_notm}} only.

    To use a {{site.data.keyword.knowledgestudioshort}} model that was built with {{site.data.keyword.knowledgestudioshort}} on {{site.data.keyword.icp4dfull_notm}}, migrate the ground truth to a {{site.data.keyword.cloud_notm}} instance of {{site.data.keyword.knowledgestudioshort}}. and then retrain the model.
    {: tip}

The following types of models are supported:

-  Rule-based models created in {{site.data.keyword.knowledgestudioshort}} that find entities in documents based on rules that you define. (File format: .pear)
-  Machine learning models created in {{site.data.keyword.knowledgestudioshort}} that understand the linguistic nuances, meaning, and relationships specific to your industry (file format: .zip)
-  Custom entity extractors that are created in and exported from {{site.data.keyword.discoveryshort}}. (File format: .ent)
-  [IBM Cloud Pak for Data]{: tag-cp4d} Custom UIMA text analysis models created in Watson Explorer Content Analytics Studio. (File format: .pear)

From installed deployments, support for importing entity extractor models was added with the 4.6.2 release.

Discovery cannot identify entity subtypes that are defined by a {{site.data.keyword.knowledgestudioshort}} model.
{: note}

To add a Machine Learning model, complete the following steps:

1.  Create the model and export it from the tool you use to create it.

    For more information, see the following documentation:

    -   {{site.data.keyword.knowledgestudioshort}} for {{site.data.keyword.icp4dfull}}

        -   [Creating a rule-based model](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-rule-annotator)
        -   [Creating a machine learning model](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-ml_annotator)
    -   {{site.data.keyword.knowledgestudioshort}} for {{site.data.keyword.cloud_notm}}

        -   [Creating a rule-based model](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-rule-annotator)
        -   [Creating a machine learning model](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-ml_annotator)
    -   [Watson Explorer Content Analytics Studio](https://www.ibm.com/docs/en/watson-explorer/12.0.x?topic=analytics-content-studio-advanced-text){: external}

        You must export the model from Watson Explorer Content Analytics Studio as a UIMA PEAR file. For more information, see: [Creating Custom PEAR Files for use with Lexical Analysis Streams](https://www.ibm.com/docs/en/watson-explorer/12.0.x?topic=las-creating-custom-pear-files-use-lexical-analysis-streams){: external}.
    
    -   [{{site.data.keyword.discoveryshort}} entity extractor](/docs/discovery-data?topic=discovery-data-entity-extractor#entity-extractor-export)

1.  From the *Teach domain concepts* section of the *Improvement tools* panel, choose **Machine learning**.
1.  Specify a name for the model, and then choose the language that was used to define the model.
1.  Click **Upload** to browse for the file that you exported earlier.
1.  Click **Create**.
1.  Choose the collection and field where you want to apply the enrichments from the model, and then click **Apply**.

## Rule-based model example
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

As a result, if someone [uses the API](/docs/discovery-data?topic=discovery-data-query-concepts) to submit a {{site.data.keyword.discoveryshort}} Query Language query to look for occurrences of the `enriched_{field_name}.entities.type:jobtitle` enrichment, any passages that discuss a person's job title are returned.

## Machine learning model example
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

## Machine learning model limits
{: #machinelearning-limits}

The number of Machine Learning (ML) models you can create per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan      | ML models per service instance |
|-----------|-------------------:|
| Cloud Pak for Data | Unlimited |
| Premium | 10 |
| Enterprise | 10 |
| Plus (includes Trial) | 3 |
{: caption="ML model plan limits" caption-side="top"}

For each {{site.data.keyword.knowledgestudioshort}} machine learning model, the maximum number of entities that can be detected is 50.

## Advanced rules models
{: #advanced-rules}

Add an advanced rules model to apply a text extraction model that was created and exported from the Advanced Rule editor of {{site.data.keyword.knowledgestudiofull}} to your collection.

Your model must be created with the appropriate {{site.data.keyword.knowledgestudioshort}} deployment:

-   [IBM Cloud Pak for Data]{: tag-cp4d} You can add models that were created and exported from the following places:

    -   {{site.data.keyword.knowledgestudiofull}} that was built with a {{site.data.keyword.icp4dfull}} deployment earlier than the 4.5 release.
    -   {{site.data.keyword.knowledgestudiofull}} that is hosted on {{site.data.keyword.cloud_notm}}
    -   NLP Editor that is built by contributors to the Center for Open-source Data & AI Technologies

-   [IBM Cloud]{: tag-ibm-cloud} You can add models that were created with a {{site.data.keyword.knowledgestudiofull}} instance that is hosted on {{site.data.keyword.cloud_notm}} only.

### Removal from {{site.data.keyword.knowledgestudioshort}}
{: #advanced-rules-eos}

Support for building models with the beta Advanced Rules Editor in {{site.data.keyword.knowledgestudioshort}} ended. Any rules models that were exported from {{site.data.keyword.knowledgestudioshort}} prior to the end of support date can continue to be used in {{site.data.keyword.discoveryshort}}. 

End of support dates differ based on the deployment type:

-   [IBM Cloud]{: tag-ibm-cloud} 30 June 2022
-   [IBM Cloud Pak for Data]{: tag-cp4d} {{site.data.keyword.icp4dfull_notm}} release 4.5.1 on 3 August 2022.

[IBM Cloud]{: tag-ibm-cloud} As an alternative to using a model that is generated by the {{site.data.keyword.knowledgestudioshort}} Advanced Rules Editor, you can define a rule by [adding a Patterns enrichment](/docs/discovery-data?topic=discovery-data-domain-pattern).

### Adding an existing model
{: #advanced-rules-task}

To add an advanced rule model, complete the following steps:

1.  Create the model and export the ZIP file that contains the model resources. 

    For more information about how to export the model, see the instructions for your model source:

    -   [{{site.data.keyword.knowledgestudioshort}} for {{site.data.keyword.icp4dfull}}](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-create-advanced-rules-model){: external}
    -   [{{site.data.keyword.knowledgestudioshort}} for {{site.data.keyword.cloud_notm}}](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-create-advanced-rules-model){: external}
    -   [Open source NLP Editor](https://github.com/CODAIT/nlp-editor){: external}

1.  From the *Teach domain concepts* section of the *Improvement tools* panel, choose **Advanced rules model**.
1.  Click **Upload**.
1.  Specify a name for the model, and then choose the language that was used to define the model.
1.  Specify a name for the result field, which is the field in the index where the output of this enrichment will be stored.
1.  Click **Upload** to browse for the ZIP file that you exported earlier.
1.  Click **Create**.
1.  Choose the collection and field where you want to apply the enrichments from the model, and then click **Apply**.

### Output format for advanced rules
{: #advanced-rules-analysis-output}

{{site.data.keyword.knowledgestudioshort}} uses the Annotation Query Language (AQL) to define the rules in an advanced rules model. Each model is defined by one or more views. Each view is a relational data structure that contains multiple data records. Each record is composed of values in columns that are defined by the view’s schema. To facilitate representing these models, which are custom and therefore have various schemas, a uniform JSON output schema is used.

-   Each JSON object represents an Annotation Query Language (AQL) view.
-   The name-and-value pairs in the JSON objects represent the names and values of the attributes in the view.
-   The tuples in an AQL view are represented as an array of JSON objects, with one object for each tuple in the view.

The following table describes how AQL data types are represented in JSON syntax.

| AQL data type | JSON syntax | JSON example |
|---------------|-------------|--------------|
| Integer | number | `5` |
| Float | number | `4.13` |
| Boolean | boolean | `true` |
| Text | string | `"some string"` |
| Span | object with the form `{"text": String, "location": {"begin": Integer, "end": Integer}}` | `{ "text": "Jane", location": {"begin": 5, "end": 9} }` |
| Special case: null value | null | `null` |
| List of Integer| array of number values | `[ 1, 2, 3, 4, 5]` |
| List of Float| array of number values |  `[ 4.13, 4.5 ]` |
| List of Boolean | array of boolean values |  `[ true, true, false]` |
| List of Text | array of string values |  `[ "some string", "another string" ]` |
| List of Span  | array of objects with the form `{"text":String, "location": {"begin": Integer, "end": Integer}}` | `[{ "text":"Jane", "location": {"begin": 5, "end": 9} }, { "text":"...", "location": {"begin": 15, "end": 40} }]` |
| Special case: empty List | array with 0 elements |  `[ ]` |
{: caption="Advanced rules model JSON output schema" caption-side="top"}

### Advanced rules model limits
{: #advanced-rules-limits}

The number of advanced rules models that you can define per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Advanced rules models per service instance |
|--------------|--------------------------------:|
| Cloud Pak for Data  |                Unlimited |
| Premium  |                      3 |
| Enterprise |                                3 |
| Plus (includes Trial) |                     1 |
{: caption="Advanced rules model plan limits" caption-side="top"}
