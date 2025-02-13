---

copyright:
  years: 2019, 2025
lastupdated: "2025-02-13"

keywords: JSON, JSON representation, result JSON

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Testing and sharing your project
{: #test}

As you improve your project, periodically test how enrichments and search setting changes impact the query results.
{: shortdesc}

For all project types except Conversational Search, you can see the fields that are associated with an indexed document by looking at the JSON view of a document that is returned by a query. Checking the JSON structure of a document can be useful if you want to check whether certain types of information are being captured.

After you enrich your collection, you can use the JSON view of a query result to check whether your enrichments are being applied and retrieved properly. For example, you can check the JSON to confirm that a synonym that you defined in a dictionary is being tagged as an occurrence of the corresponding dictionary term.

To test your project, complete the following steps:

1.  From the navigation panel, open the **Improve and customize** page.
1.  Retrieve query results by doing one of the following things:

    -   *Content Mining* project: Choose or add a facet to apply to the documents, and then click **View filtered documents**. To analyze your data in more depth, open the Content Mining application in a new window or tab by clicking **Launch application**.
    -   Other project types: Enter a test query to submit or leave the field empty and press Enter to submit an empty query.
1.  From the query result list, click the link to view the document.

    A representation of the original document is displayed. 
    
1.  [IBM Cloud]{: tag-ibm-cloud} Click **Open advanced view** to see useful summary information, such as the number of occurrences of any enrichments that are detected in the document.

    **Optional**: Select an enrichment to highlight every occurrence of the element within the document text.

    For a *Document Retrieval for Contracts* project, the *Contract Data* page is displayed. For more information about Contract filter options, see [Understanding contracts](/docs/discovery-data?topic=discovery-data-contracts-schema#contracts-elements).

1.  You can learn more about information that is identified by the enrichments that are applied to your documents by reviewing the JSON representation of a document that is returned in a search result.

    [IBM Cloud]{: tag-ibm-cloud}

      1.  Click the *Display options* menu from the advanced view header, and then select **JSON**.

    [IBM Cloud Pak for Data]{: tag-cp4d} [IBM Software Hub]{: tag-teal}

      1.  Click **JSON**.

          For a *Document Retrieval for Contracts* project, click the **Contract Data** tab. For more information about Contract filter options, see [Understanding contracts](/docs/discovery-data?topic=discovery-data-contracts-schema#contracts-elements).

## Sharing your project
{: #test-preview}

Try out your project and share it with others on your team for testing purposes. A test implementation of your project is created and hosted by IBM. Use this application preview to test your search results.

To preview and share your project, complete the following steps:

1.  From the **Integrate and Deploy** > **Preview Link** page, follow the instructions to give your team members access to your project. (In Content Mining projects, the page is named **Share Link**.)

    [IBM Cloud]{: tag-ibm-cloud} For more information about access in {{site.data.keyword.cloud_notm}}, see [Managing access to resources](/docs/account?topic=account-assign-access-resources&interface=ui){: external}.

1.  Click the copy icon for the **Copy Link** field to copy the URL of the preview application.

1.  Paste the URL into a web browser to test it yourself or send the URL to team members.

    Don't forget to send any login credentials that are needed to access the project when you send the link to your colleagues.
