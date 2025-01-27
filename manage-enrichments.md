---

copyright:
  years: 2020, 2025
lastupdated: "2024-05-27"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Manage enrichments
{: #manage-enrichments}

Apply enrichments to fields in your documents to make meaningful information easier to find and return in searches.
{: shortdesc}

You typically apply enrichments to fields at the time that you create the enrichment. However, you can apply enrichments to fields later. You might want to apply an existing enrichment to a new custom field that you create by using the SDU tool, for example. You can remove enrichments that you applied to fields also.

For more information about available enrichments, see the following topics:

- [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain)
- [Applying prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu)

To apply enrichments to a Content Mining project, you should use the Content Mining application instead of using the Discovery user interface. When you use the Content Mining application, it ensures that the enrichments are accepted in the Content Mining project. For more information about applying enrichments such as a dictionary or phrase sentiment to a Content Mining project, see [Enrich your collection](/docs/discovery-data?topic=discovery-data-cm-edit-collection#cm-enrichments).
{: note}

To manage enrichments, complete the following steps:

1.  From the navigation pane, open the **Manage collections** page, and then click a collection to open it.
1.  Click the **Enrichments** tab.

    A list of available enrichments is displayed. 
    
    You can identify built-in enrichments because they are categorized as type `System`. The list also includes any custom enrichments that were created in any of the projects in your service instance.
1.  Find the enrichment that you want to apply or remove.
1.  Click the twistie in the associated field to expand a list of fields.
1.  Do one of the following things:

    -   To apply an enrichment to documents, select the field or fields that you want to enrich. You can apply enrichments to the `text` and `html` fields, and to custom fields that were added from uploaded JSON or CSV files or from the Smart Document Understanding (SDU) tool.

        If the field that you choose comes from a JSON file, after you apply the enrichment, the field data type is converted to an array. The field is converted to an array even if it contains a single value. For example, `"field1": "Discovery"` becomes `"field1": ["Discovery"]`. Only the first 50,000 characters of a custom field from a JSON file are enriched.
        {: note}

    -   To remove an enrichment, clear the checkboxes for fields that you want to remove the enrichment from.

1. Click **Apply changes and reprocess** to apply your changes to the collection.

## Deleting an enrichment
{: #enrichments-delete}

You can delete a custom enrichment that you built to teach {{site.data.keyword.discoveryshort}} about your service. Custom enrichments include dictionaries, regular expressions, patterns, and so on. For more information, see [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain).

You cannot delete a prebuilt enrichment. Prebuilt enrichments include the Natural Language Understanding enrichments, such as the Entities enrichment, that are built into the product. To determine which enrichments are built in, check the *Type* column of the *Enrichments* page for a collection. Prebuilt enrichments have the `System` type.

To delete a custom enrichment, complete the following steps:

1.  Open a project that uses the custom enrichment. 
1.  Click *Manage collections*, and then open a collection where the enrichment is in use.
1.  From the *Enrichments* page of a collection, remove the enrichment from any fields where it is applied.
1.  Click **Apply changes and reprocess**, and then wait for the system to process the documents in your collection without the enrichment.
1.  Repeat the previous step for every collection in every project where the enrichment is used.

    Remember, a custom enrichment can be used by any collection in any project within a single {{site.data.keyword.discoveryshort}} service instance.
1.  From any of the collections that used the enrichment, open the *Enrichments* page, and then click the delete icon to delete the enrichment.

The custom enrichment is removed from the *Enrichments* list everywhere in this service instance.

## Using the API to manage enrichments
{: #enrichments-api}

To apply an enrichment to data by using the API, complete the following steps:

1.  First, you must know the unique ID of the enrichment that you want to apply. For more information, see [Enrichment IDs](#enrichments-id).
1.  Use the *Create collection* or *Update collection* methods to apply an enrichment to the documents in a collection. For more information, see [Apply enrichment by using the API](#enrichments-api-task)

### Enrichment IDs
{: #enrichments-ids}

If you want to apply a custom enrichment that you created for one collection to another collection, you must know the unique ID that was generated for the enrichment when it was created. Use the API to [list enrichments](https://cloud.ibm.com/apidocs/discovery-data#listenrichments){: external} from the project where the custom enrichment is in use. The list that is returned includes enrichment ID information.

For prebuilt enrichments, the unique IDs do not change. The following table lists the IDs that are associated with each prebuilt enrichment type and identifies the collection languages for which the enrichment is supported. An enrichment cannot be applied to a collection unless the collection language is supported by the enrichment.

| Name | Enrichment ID | Supported languages |
|------|---------------|---------------------|
| Contracts | 701db916-fc83-57ab-0000-000000000014 | en |
| Entities | 701db916-fc83-57ab-0000-00000000001e | ar, de, en, es, fr, it, ja, ko, nl, pt, zh-CN |
| Keywords | 701db916-fc83-57ab-0000-000000000018 | ar, de, en, es, fr, it, ja, ko, nl, pt, zh-CN |
| Part of Speech | 701db916-fc83-57ab-0000-000000000002 | All supported languages|
| Sentiment of Document | 701db916-fc83-57ab-0000-000000000016 | ar, de, en, es, fr, it, ja, ko, nl, pt, zh-CN |
| Table Understanding | 701db916-fc83-57ab-0000-000000000012 | All supported languages |
{: caption="Prebuilt enrichment IDs" caption-side="top"}

For more information about all of the supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

### Apply enrichments by using the API
{: #enrichments-api-task}

To apply an enrichment by using the API, complete the following steps:

1.  Determine the base URL for the endpoint and the token or API key for your deployment.

    For more information, see [Building custom applications with the API](/docs/discovery-data?topic=discovery-data-api-use).

1.  Get the project ID for your project.

    From the product user interface, go to the **Integrate and Deploy** > **View API information** page, and then copy the project ID.

1.  If you don't know the ID of the collection that you want to apply the enrichment to, get a list of your collections to find it.

    For example:

    ```sh
    GET $authentication $url/v2/projects/$project_id/collections?version=2019-11-22
    ```
    {: codeblock}

    The `collection_id` is returned.

1.  Send a GET request to return the configuration of the collection that lists the applied enrichments.

    For example:

    ```sh
    GET $authentication $url/v2/projects/$project_id/collections/$collection_id?version=2019-11-22
    ```
    {: codeblock}

    For the enrichment IDs for the prebuilt enrichments, see [Enrichment IDs](#enrichments-ids).

1.  Add the enrichment that you want to apply.

    For example, to add the *Keywords* enrichment, you can include the enrichment in the enrichments list. First, get its ID from the table. 

    The Keywords enrichment ID is `701db916-fc83-57ab-0000-000000000018`. To indicate that you want to apply the Keywords enrichment to the content in the `text` field of the documents in the collection, you can represent it in JSON format as follows:

    ```json   
    {
        "enrichment_id" : "701db916-fc83-57ab-0000-000000000018",
        "fields" : [ "text" ]
    }
    ```
    {: codeblock}

    Any enrichments that you specify replace the default enrichments. Therefore, if you want to retain a default enrichment, don't forget to include it in the list of enrichments that you apply to the collection. For a list of default enrichments per project type, see [Default enrichments per project type](#enrichments-defaults).
    {: note}

    For example, to retain the *Entities* enrichment and add the *Keywords* enrichment, you might specify the following in the request body. 

    ```json
    "enrichments": [
      {
        "enrichment_id": "701db916-fc83-57ab-0000-00000000001e",
        "fields": [
          "text"
        ]
      },
      {
        "enrichment_id": "701db916-fc83-57ab-0000-000000000018",
        "fields": [
          "text"
        ]
      } 
    ]
    ```
    {: codeblock}

1.  Submit the updated JSON request body with the [update collection](https://cloud.ibm.com/apidocs/discovery-data#updatecollection){: external} method to apply the enrichment to your collection.

    For example:

    ```sh
    POST $authentication -d '$requestBody' $url/v2/projects/$project_id/collections/$collection_id?version=2019-11-22
    ```
    {: codeblock}

{{site.data.content.enrichment-defaults-reuse}}
