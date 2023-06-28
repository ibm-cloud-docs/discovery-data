---

copyright:
  years: 2019, 2023
lastupdated: "2023-06-28"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Classify text
{: #domain-classifier}

Define categories by which text in your documents can be classified.
{: shortdesc}

This topic describes how to classify text. If you want to classify documents, use the Content Mining application. For more information, see [Classifier types](#domain-classifier-difs).

Add a text classifier to assign text from documents in your collection into categories. {{site.data.keyword.discoveryshort}} uses the labels and text examples that you provide to predict the categories of text in your collection.

To create a text classifier, complete the following steps:

1.  Create a CSV file that contains example text followed by its category label per line.

    The CSV file must be in UTF-8 encoding format and must meet the following requirements:

    -   The format must be `text,label`. The `text` is the example text, and the `label` is the category name.

        Add complete sentences as text entries. Do not include any blank lines in the CSV file.

        You can add more `label` columns if you need to apply more than one label to the sentence in the `text` column. For example, `text,label,label`.
    -   The file must have at least two columns with no headers.
    -   Add 10 or more entries for each category that you want to define. The minimum number of entries that are required per category is 3. The more examples that you provide for each category, the better the classifier can predict the categories of other content in your collection.

    The following example is a CSV file that defines two categories, named `facility_temperature` and `catering`. The example text consists of feedback from conference attendees.

    ```text
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

1.  From the *Teach domain concepts* section of the *Improvement tools* panel, and then click **Text classifiers**.
1.  Click **Upload**.
1.  Specify a name for the classifier, and then choose the language that was used in the CSV file.
1.  Click **Upload** to browse for the CSV file that you created earlier.
1.  Click **Create**.

    A classifier enrichment is created based on the training data that you provided.
1.  Choose the collection and field where you want to apply the text classifier enrichment, and then click **Apply**.

The following example shows how an enrichment that is created with the sample CSV file as its training data might classify text in a document. In the output, the classifier enrichment applies the `facility_temperature` label to the document text. The `label` is stored in the `enriched_{field_name}` array, within the `classes` array.

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

## Classifier types
{: #domain-classifier-difs}

The classifier that you add from the {{site.data.keyword.discoveryshort}} user interface is a *text classifier*. A text classifier can classify documents based on words and phrases that are extracted from the body text with their part of speech information taken into account. 

You can create another classifier type, a *document classifier*, only from the deployed Content Mining application. A document classifier can classify documents based on words and phrases that are extracted from the body text fields with information from their part of speech and the other enrichments that are applied to the body text taken into account. The information from the other non-body fields are also used. 

You can apply a document classifier to a collection in a project type other than a Content Mining project. To do so, you must create the classifier in the deployed Content Mining application and export it. You can then import the classifier and apply it to your collection as an enrichment. For more information, see [Creating and applying a document classifier](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-cm-doc-classifier).

The text classifier uses Part of Speech information regardless of whether the Part of Speech enrichment is applied to the project.

Text classifiers that you add to one project can be used by other projects, including Content Mining projects.

A text classifier does not classify the target text field with confidence scores that are lower than 0.5. You cannot change the confidence threshold that is used by the text classifier. If you expected certain types of passages to be classified that weren't, you can add passages with similar characteristics to your training data and train another classifier.
{: tip}

## Text classifier limits
{: #classifier-limits}

The number of text classifiers and labels that you can create per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Limit   | Plus | Enterprise | Premium | Cloud Pak for Data |
|---------|------|------------|---------|--------------------|
| Number of text classifiers per service instance | 5 | 20 | 20 | Unlimited |
| Number of labeled data rows | 2,000 | 20,000 | 20,000 | 20,000 |
| Maximum size in MB of training data after enrichment | 16 | 1,024 | 1,024 | 1,024 |
| Number of labels | 100 | 1,000 | 1,000 | 1,000 |
{: caption="Text classifier plan limits" caption-side="top"}
