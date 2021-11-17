---

copyright:
  years: 2020, 2021
lastupdated: "2021-11-17"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Managing enrichments
{: #manage-enrichments}

Apply enrichments to fields in your documents to make meaningful information easier to find and return in searches.
{: shortdesc}

You typically apply enrichments to fields at the time that you create the enrichment. However, you can apply enrichments to fields later. You might want to apply an existing enrichment to a new custom field that you create by using the SDU tool, for example. You can remove enrichments that you applied to fields also.

For more information about available enrichments, see the following topics:

- [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain)
- [Applying prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu)

To manage enrichments, complete the following steps:

1.  From the navigation pane, open the **Manage collections** page, and then click a collection to open it.
1.  Click the **Enrichments** tab.

    A list of available enrichments is displayed. 
    
    You can identify built-in enrichments because they are categorized as type `System`. The list also includes any custom enrichments that were created in any of the projects in your service instance.
1.  Find the enrichment that you want to apply or remove.
1.  Click the twistie in the associated field to expand a list of fields.
1.  Do one of the following things:

    -   To apply an enrichment to documents, select the field or fields that you want to enrich.

        If the field that you choose comes from a JSON file, after you apply the enrichment, the field data type is converted to an array. The field is converted to an array even if it contains a single value. For example, `"field1": "Discovery"` becomes `"field1": ["Discovery"]`.
    -   To remove an enrichment, clear the checkboxes for fields that you want to remove the enrichment from.

1. Click **Apply changes and reprocess** to apply your changes to the collection.

## Applying enrichments by using the API
{: #enrichments-api}

To apply an enrichment by using the API, you must know the unique ID of the enrichment. If you have another project that uses the enrichment already, you can use the API to [get a list of the enrichments](https://cloud.ibm.com/apidocs/discovery-data#listenrichments){: external}. The list that is returned includes enrichment ID information.

To apply an enrichment by using the API, complete the following steps:

1.  Determine the base URL for the endpoint and the token or API key for your deployment.

    For more information, see [Building custom applications with the API](/docs/discovery-data?topic=discovery-data-api-use).

1.  Get the project ID for your project.

    From the product user interface, go to the **Integrate and Deploy** > **View API information** page, and then copy the project ID.

1.  If you don't know the ID of the collection that you want to apply the enrichment to, get a list of your collections to find it.

    For example:

    ```curl
    GET $authentication $url/v2/projects/$project_id/collections?version=2019-11-22
    ```
    {: codeblock}

    The `collection_id` is returned.

1.  Send a GET request to return the configuration of the collection that lists the applied enrichments.

    For example:

    ```curl
    GET $authentication $url/v2/projects/$project_id/collections/$collection_id?version=2019-11-22
    ```
    {: codeblock}

1.  Add the enrichment that you want to apply.

    You can also replace an enrichment. For example, if you want to use the Entities v1 legacy enrichment instead of the Entities v2 enrichment, you can find the Entities v2 enrichment definition (it has the ID `701db916-fc83-57ab-0000-00000000001e`), and then replace it with the Entities v1 legacy enrichment ID (with the ID `701db916-fc83-57ab-0000-000000000017`).

    For example, to apply the Entities v1 legacy enrichment:

    ```json
    {
        "enrichment_id" : "701db916-fc83-57ab-0000-000000000017",
        "fields" : [ "text" ]
    }
    ```
    {: codeblock}

1.  Submit the updated JSON request body with the [update collection](https://cloud.ibm.com/apidocs/discovery-data#updatecollection){: external} method to apply the enrichment to your collection.

    For example:

    ```curl
    POST $authentication -d '$requestBody' $url/v2/projects/$project_id/collections/$collection_id?version=2019-11-22
    ```
    {: codeblock}
