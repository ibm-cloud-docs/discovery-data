---

copyright:
  years: 2015, 2022
lastupdated: "2022-07-22"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Creating custom annotators
{: #cm-custom-annotator}

You can create a dictionary, regular expression, or machine learning annotator to generate new facets that can help you to analyze your data.
{: shortdesc}

Before you begin, have the following data ready.

| Annotator type | Data |
|----------------|------|
| Dictionary | You can optionally upload a CSV file of dictionary terms. For more information about the file format requirements, see [Uploading dictionary terms](/docs/discovery-data?topic=discovery-data-domain#dictionary-csv) |
| Machine learning | A compressed file of a machine learning model that is exported from Watson Knowledge Studio is required. |
| Regular expression | You can optionally upload a JSON file that contains regular expression patterns. |
{: caption="Custom annotator prerequisite data" caption-side="top"}

To create a custom annotator, complete the following steps:

1.  From the analysis view of your collection, click the **Collections** link in the breadcrumb to open the *Create a collection for your analytics solutions* page of the Content Mining application.

1.  To create an annotator, click **collection**, and then select **custom annotator** from the list.

    ![Shows the collection menu](images/cm-collection-menu.png)

1.  Click **Create custom annotator**.
1.  Name your annotator, and then optionally add a description.
1.  Choose the annotator type, and then click **Next**.
1.  Follow the on-screen instructions.

    The facet name value that you specify for the annotator is the facet that is displayed from the collection search view.

## Applying the annotator
{: #cm-custom-annotator-deploy}

After the annotator is created, you must apply it to your collection. 

1.  From the *Create a custom annotator for your analytics solutions* page of the Content Mining application, click **custom annotator**, and then select **collection** from the list.
1.  In the tile for your collection, click the *options* icon, and choose **Edit collection**.

    ![Collection tile overflow menu](images/cm-edit-colxn-icon.png){: caption="Figure 5. Collection menu" caption-side="bottom"}

1.  Click the **Enrichment** tab, and then select the annotator that you created. 

    You might need to scroll to find it.
1.  Click **Save**, and then confirm the action.

Give the index time to rebuild.

## Filtering documents with your facet
{: #cm-custom-annotator-use}

1.  From the analysis view of your collection, submit an empty search.
1.  In the *Facet analysis* pane, select the facet that you created.

## Artifact limits
{: #artifact-limits}

The number of enrichments that you can create per service instance depends on your {{site.data.keyword.discoveryshort}} plan type. Totals include enrichments that you create in this Content Mining project and in other projects in the same service instance.

### Dictionary limits
{: #dictionary-limits}

| Plan | Number of dictionaries per service instance | Number of term entries per dictionary | Number of terms for which suggestions can be generated |
|-----------|-------------------:|------------------------:|--------------------------:|
| Cloud Pak for Data | Unlimited | Unlimited | 1,000 |
| Premium | 100 | 10,000 | 1,000 |
| Enterprise | 100 | 10,000 | 1,000 |
{: caption="Dictionary plan limits" caption-side="top"}

### Regular expression limits
{: #regex-limits}

| Plan | Regex enrichments per service instance | Regex patterns per service instance | 
|------|------------------------------------:|---------------------------------------:|
| Cloud Pak for Data | Unlimited | Unlimited |
| Premium | 100 | 50 |
| Enterprise | 100 | 50 |
{: caption="Regular expression plan limits" caption-side="top"}

### Machine learning model limits
{: #ml-model-limits}

| Plan      | ML models per service instance |
|-----------|-------------------:|
| Cloud Pak for Data | Unlimited |
| Premium | 10 |
| Enterprise | 10 |
{: caption="ML model plan limits" caption-side="top"}
