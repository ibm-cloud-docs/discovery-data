---

copyright:
  years: 2015, 2022
lastupdated: "2022-09-07"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Creating custom annotators
{: #cm-custom-annotator}

You can create a dictionary, regular expression, or machine learning annotator to generate new facets that can help you to analyze your data.
{: shortdesc}

Before you begin, have the following data ready.

| Annotator type | Description | Data |
|----------------|-------------|------|
| Dictionary | Assigns facets to terms that match dictionary entries that you define or upload. | You can optionally upload a file of dictionary terms. |
| Machine learning | Assigns facets to mentions that are recognized by a machine learning model that you upload. | A compressed file of a machine learning model is required. |
| Regular expression | Assigns facets to text that matches Java regular expression patterns that you define or upload. | You can optionally upload a JSON file that contains regular expression patterns. |
{: caption="Custom annotator prerequisite data" caption-side="top"}

To create a custom annotator, complete the following steps:

1.  From the analysis view of your collection, click the **Collections** link in the breadcrumb to open the *Create a collection for your analytics solutions* page of the Content Mining application.

1.  To create an annotator, click **collection**, and then select **custom annotator** from the list.

    ![Shows the collection menu](images/cm-collection-menu.png)

1.  Click **Create custom annotator**.
1.  Name your annotator, and then optionally add a description.
1.  Choose the annotator type, and then click **Next**.
1.  Follow the on-screen instructions.

    For more information about how to configure each annotator type, see one of the following sections:

    -   [Dictionary](#cm-custom-annotator-dictionary)
    -   [Machine learning model](#cm-custom-annotator-ml)
    -   [Regular expressions](#cm-custom-annotator-regex)

### Dictionary configuration
{: #cm-custom-annotator-dictionary}

You can import an existing dictionary by uploading it or you can create a dictionary by adding terms one at a time.

If you plan to import a dictionary, the dictionary terms must be defined in a CSV file. Specify each term and its synonyms in a separate line. Use the following syntax to specify each term:

```
{term},{synonym},{synonym},...
```
{: codeblock}

To add a dictionary, complete the following steps:

1.  Do one of the following things:

    -   To import the dictionary terms:
    
        1.  Click **Import**, and then browse for the file with your dictionary terms.
        1.  Click **Import**.

    -   To define the dictionary terms:

        1.  Click **Add**.
        1.  Click *Word list* to add the dictionary terms.
        1.  Click **Add**, and then add the term in the **Base word** field and any synonyms that you want to define for the term in the **Other words** field. Separate multiple synonyms with commas. Click **OK**.
        1.  Repeat the previous step to add another dictionary term.
        1.  After you finish adding dictionary terms, click *Basic settings*.

1.  Name the dictionary.
1.  If you plan to define terms with a part of speech other than a noun, specify the part of speech.
1.  If you want the terms to be case-sensitive, deselect the **Ignore case** checkbox.
1.  Identify the facet name to use for this dictionary.

    You can create a hierarchical facet by including a period (.) in the facet name. For example, you might create one dictionary with the facet path `Weather.Rain` and others with the facet paths `Weather.Storm` and `Weather.Lightning`.

    The facet name that you specify for the annotator is the facet name that is displayed from the collection search view.

1.  If you want documents that are returned for a subfacet to be included when a user filters on the root facet, select **Lift up words**.

    For example, you might enable *Lift up words* for `Weather.Rain` and `Weather.Storm` but not `Weather.Lightning`. As a result, when a user clicks the Weather facet, the returned documents include documents that mention *rain* and *storm*. However, a user must click the *Weather>Lightning* facet explicitly to get documents that mention *lightning* to be returned.

1.  Click **Save**.

From the custom annotator page, you can see dictionaries that were created in other projects, including non-Content Mining projects. Dictionaries from other project types show the enrichment name as the annotator name. The *Ignore case* and *Lift up words* settings are disabled and the dictionary is named  `custom dict`.

#### Dictionary limits
{: #dictionary-limits}

| Plan | Number of dictionaries per service instance | Number of term entries per dictionary | Number of terms for which suggestions can be generated |
|-----------|-------------------:|------------------------:|--------------------------:|
| Cloud Pak for Data | Unlimited | Unlimited | 1,000 |
| Premium | 100 | 10,000 | 1,000 |
| Enterprise | 100 | 10,000 | 1,000 |
{: caption="Dictionary plan limits" caption-side="top"}

Totals include enrichments that you create in this Content Mining project and in other projects in the same service instance.

### Machine learning configuration
{: #cm-custom-annotator-ml}

You can import an existing machine learning model. 

To use {{site.data.keyword.discoveryshort}} to create a model, see [Entity extractor](/docs/discovery-data?topic=discovery-data-entity-extractor).

To import a model, complete the following steps:

1.  Click **Select file**, and then browse for the machine learning model file.
1.  In the **Facet path** field, specify the root facet name to use for the model.

    The facet name that you specify for the annotator is the facet name that is displayed from the collection search view.

1.  Click **Save**.

#### Machine learning model limits
{: #ml-model-limits}

| Plan      | ML models per service instance |
|-----------|-------------------:|
| Cloud Pak for Data | Unlimited |
| Premium | 10 |
| Enterprise | 10 |
{: caption="ML model plan limits" caption-side="top"}

Totals include enrichments that you create in this Content Mining project and in other projects in the same service instance.

### Regular expressions configuration
{: #cm-custom-annotator-regex}

You can import existing patterns by uploading them in a JSON file or you can add patterns.

To add patterns, complete the following steps:

1.  Add the regular expression pattern to the **New pattern** field, and then click **Add**.
1.  Specify a name for the pattern, and then identify the facet name to use for this pattern. 

    The facet name that you specify for the annotator is the facet name that is displayed from the collection search view.
1.  **Optional**: Specify a facet value. You can specify a value from the options that are described in the table.

    | Facet value | Description |
    |-------------|-------------|
    | `$0` | Displays the matched text as-is. | If the matched text is `212-555-1234`, then the facet value is displayed as `212-555-1234`. |
    | `$n` | If your regular expression pattern contains groups, you can specify a group number to return the matched text from the pattern group only. For example, if your regular expression consists of 3 groups that define a US phone number pattern, such as `(\d{3})-(\d{3})-(\d{4})`, and you want to return only the area code portion of the phone number, you can specify `$1`. If the matched text is `212-555-1234`, then the facet value is displayed as `212`. |
    | `{prefix-text}:$0` | Adds hardcoded text in front of the facet name. You might want to use this option if you want to distinguish facets that are generated by this regular expression from facets that are similar but generated in some other way. For example, `MyRegex:$0` results in a facet named `MyRegex:212-555-1234`.
    {: caption="Regular expression facet value options" caption-side="top"}

1.   Click **Save**.

To import patterns, complete the following steps:

1.  Define the patterns that you want to add in a JSON file.

    The pattern definition must use the following syntax:

    ```json
    [
      {
        "name": "US Phone number",
        "description": "US mobile phone number",
        "pattern": "(\\d{3})-(\\d{3})-(\\d{4})",
        "facetPath": ".regex.usphonenumber",
        "facetValue": "$0"
      }
    ]
    ```
    {: codeblock}

    Keep the following notes in mind:

    -   The patterns must be defined in an array, even if you plan to define only one pattern.
    -   Escape any backslash (`\`) characters with a backslash.
    -   For more information about the facet value options, see the *Regular expression facet value options* table.

1.  Click **Import**, and then choose the JSON file where the patterns are defined.
1.  Click **Save**.

#### Regular expression limits
{: #regex-limits}

| Plan | Regex enrichments per service instance | Regex patterns per service instance | 
|------|------------------------------------:|---------------------------------------:|
| Cloud Pak for Data | Unlimited | Unlimited |
| Premium | 100 | 50 |
| Enterprise | 100 | 50 |
{: caption="Regular expression plan limits" caption-side="top"}

Totals include enrichments that you create in this Content Mining project and in other projects in the same service instance.

## Applying the annotator
{: #cm-custom-annotator-deploy}

After the annotator is created, you must apply it to your collection. 

1.  From the *Create a custom annotator for your analytics solutions* page of the Content Mining application, click **custom annotator**, and then select **collection** from the list.
1.  In the tile for your collection, click the *options* icon, and choose **Edit collection**.

    ![Collection tile overflow menu](images/cm-edit-colxn-icon.png){: caption="Figure 1. Collection menu" caption-side="bottom"}

1.  Click the **Enrichment** tab, and then select the annotator that you created. 

    You might need to scroll to find it.
1.  Click **Save**, and then confirm the action.

Give the index time to rebuild.

## Filtering documents with your facet
{: #cm-custom-annotator-use}

1.  Click the collection tile to open your collection in the data analysis page.
1.  Do one of the following things:

    -   Your custom facets are listed in the *Facets* view. Scroll and click **Load more** repeatedly until your facets are displayed.
    -   Submit an empty search to return all documents. In the *Facet analysis* pane, select the facet that you created.
    -   To access your custom facets more quickly, add them to a custom view. Select **Custom** as the view, and then click **Edit**. Select one or more facets to add to the view, and then click **Save**.

        ![Custom view](images/cm-custom-view.png){: caption="Figure 2. Collection menu" caption-side="bottom"}
