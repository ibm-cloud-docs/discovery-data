---

copyright:
  years: 2019, 2023
lastupdated: "2022-08-11"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Advanced rules models
{: #domain-advanced-rules}

Add an advanced rules model to apply a text extraction model that was created and exported from the Advanced Rule editor of {{site.data.keyword.knowledgestudiofull}} to your collection.

Your model must be created with the appropriate {{site.data.keyword.knowledgestudioshort}} deployment:

-   ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: You can add models that were created and exported from the following places:

    -   {{site.data.keyword.knowledgestudiofull}} that is hosted on {{site.data.keyword.icp4dfull}}
    -   {{site.data.keyword.knowledgestudiofull}} that is hosted on {{site.data.keyword.cloud_notm}}
    -   NLP Editor that is built by contributors to the Center for Open-source Data & AI Technologies

-   ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: You can add models that were created with a {{site.data.keyword.knowledgestudiofull}} instance that is hosted on {{site.data.keyword.cloud_notm}} only.

{{site.data.keyword.knowledgestudioshort}} support for building models with the beta Advanced Rules Editor in instances that are managed by {{site.data.keyword.cloud_notm}} ended on 30 June 2022. Any rules models that were exported from {{site.data.keyword.knowledgestudioshort}} before that date can continue to be run in {{site.data.keyword.discoveryshort}}.
{: note}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: As an alternative to using a model that is generated by the {{site.data.keyword.knowledgestudioshort}} Advanced Rules Editor, you can define a rule by [adding a Patterns enrichment](/docs/discovery-data?topic=discovery-data-domain-pattern).

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

## Output format for advanced rules
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

## Advanced rules model limits
{: #advanced-rules-limits}

The number of advanced rules models that you can define per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Advanced rules models per service instance |
|--------------|--------------------------------:|
| Cloud Pak for Data  |                Unlimited |
| Premium  |                      3 |
| Enterprise |                                3 |
| Plus (includes Trial) |                     1 |
{: caption="Advanced rules model plan limits" caption-side="top"}
