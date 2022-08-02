---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-02"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Migrating enrichments from Watson Explorer
{: #enrichmig}

If you have resources from IBM Watson Explorer, some of them can be migrated to {{site.data.keyword.discoveryfull}}.
{: shortdesc}

## Types of resources that can be migrated
{: #enrichty}

The following types of resources can be migrated from Watson Explorer to {{site.data.keyword.discoveryshort}}:

- From Watson Explorer Analytical Components: [User dictionaries](https://www.ibm.com/support/knowledgecenter/en/SS8NLW_12.0.0/com.ibm.discovery.es.ad.doc/iiysatauserdict.html){: external}
- From Watson Explorer oneWEX: [Dictionaries](https://www.ibm.com/support/knowledgecenter/en/SS8NLW_12.0.0/com.ibm.watson.wex.ee.doc/c_ce_adm_dict_ann.html){: external}, [character patterns](https://www.ibm.com/support/knowledgecenter/en/SS8NLW_12.0.0/com.ibm.watson.wex.ee.doc/c_ce_adm_char_ann.html){: external}, and [facets](https://www.ibm.com/docs/en/watson-explorer/12.0.x?topic=las-creating-custom-pear-files-use-lexical-analysis-streams){: external}.

To analyze data with these migrated enrichments, you can use a Content Mining project. The tools in the associated Content Mining application are similar to tools that are available in Watson Explorer. 

-   For more information about how to create a Content Mining project, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).
-   For more information about how to apply enrichments to a collection in the Content Mining application, see [Applying the annotator](/docs/discovery-data?topic=discovery-data-cm-custom-annotator#cm-custom-annotator-deploy).

## Importing dictionaries from Watson Explorer Analytical Components
{: #enrichdictca}

You can import [user dictionaries](https://www.ibm.com/support/knowledgecenter/en/SS8NLW_12.0.0/com.ibm.discovery.es.ad.doc/iiysatauserdict.html){: external} from IBM Watson Explorer Analytical Components.

The default file location and name for dictionaries that are saved in Watson Explorer Analytical Components is `${primary_server_node}/{primary_configuration}/{collection_ID}/{dictionary_name}.fdic.xml`.
{: tip}

1.  Download your user dictionaries from Watson Explorer Analytical Components.
1.  From your {{site.data.keyword.discoveryshort}} Content mining project, open the Content Mining application.
1.  From the analysis view of your collection, click the **Collections** link in the breadcrumb to open the *Create a collection for your analytics solutions* page of the Content Mining application.

1.  To create an annotator, click **collection**, and then select **custom annotator** from the list.

    ![Shows the collection menu](images/cm-collection-menu.png)

1.  Click **Create custom annotator**.
1.  Name your annotator, and then optionally add a description.
1.  From the **Annotator Type** menu, select **Dictionary**, and then click **Next**.
1.  Click the **Import** button, and then select the `{name}.fdic.xml` dictionary file that you want to import.
1.  Click **Save**.

## Uploading dictionaries from Watson Explorer oneWEX
{: #enrichdictow}

You can import [dictionaries](https://www.ibm.com/support/knowledgecenter/en/SS8NLW_12.0.0/com.ibm.watson.wex.ee.doc/c_ce_adm_dict_ann.html){: external} from IBM Watson Explorer oneWEX.

1.  From Watson Explorer oneWEX, Version 12.0.0 or later modifications or fix packs, download the dictionary CSV file.

    -   Log in to the oneWEX administrator console.
    -   Open the **Resource** tab.
    -   Select dictionary enrichments, open the dictionary tab, and click the download icon. The dictionary is downloaded as a CSV file.

1.  From your {{site.data.keyword.discoveryshort}} Content mining project, open the Content Mining application.
1.  From the analysis view of your collection, click the **Collections** link in the breadcrumb to open the *Create a collection for your analytics solutions* page of the Content Mining application.

1.  To create an annotator, click **collection**, and then select **custom annotator** from the list.

    ![Shows the collection menu](images/cm-collection-menu.png)

1.  Click **Create custom annotator**.
1.  Name your annotator, and then optionally add a description.
1.  From the **Annotator Type** menu, select **Dictionary**, and then click **Next**.
1.  Click the **Import** button, and then upload the CSV file of the dictionary that was downloaded from oneWEX.
1.  Click **Import**, and then click **Save**.

## Importing character patterns from Watson Explorer oneWEX
{: #enrichcpow}

You can import [character patterns](https://www.ibm.com/support/knowledgecenter/en/SS8NLW_12.0.0/com.ibm.watson.wex.ee.doc/c_ce_adm_char_ann.html){: external} from IBM Watson Explorer oneWEX.

1.  From your {{site.data.keyword.discoveryshort}} Content mining project, open the Content Mining application.
1.  From the analysis view of your collection, click the **Collections** link in the breadcrumb to open the *Create a collection for your analytics solutions* page of the Content Mining application.

1.  To create an annotator, click **collection**, and then select **custom annotator** from the list.

    ![Shows the collection menu](images/cm-collection-menu.png)

1.  Click **Create custom annotator**.
1.  Name your annotator, and then optionally add a description.
1.  From the **Annotator Type** menu, select **Regular expression**, and then click **Next**.
1.  Click the **Import** button.
1.  Select the JSON file that you want to import, and then click **Save**.

## Importing facets from Watson Explorer Content Analytics Studio
{: #enrichml}

You can show Content Analytics Studio facets in the Content Mining application. Only facets with a UIMA Feature of type `Literal Value` are displayed.

For more information about how to import Content Analytics Studio machine learning models for use in other project types, see [Machine learning models](/docs/discovery-data?topic=discovery-data-domain-ml).

1.  From the Watson Explorer Content Analytics Studio, export the machine learning model that defines the facets that you want to use. The model file must have a `.pear` extension.
1.  In the export configuration, remove the facet path, but keep the subfacet value. Set the Index Field name to the Facet Tree Path in Content Analytics Studio.

    For more information, see [Creating Custom PEAR Files for Use with Lexical Analysis Streams](https://www.ibm.com/docs/en/watson-explorer/12.0.x?topic=las-creating-custom-pear-files-use-lexical-analysis-streams){: external}.
1.  From your {{site.data.keyword.discoveryshort}} Content mining project, open the Content Mining application.
1.  From the analysis view of your collection, click the **Collections** link in the breadcrumb to open the *Create a collection for your analytics solutions* page of the Content Mining application.

1.  To create an annotator, click **collection**, and then select **custom annotator** from the list.

    ![Shows the collection menu](images/cm-collection-menu.png)

1.  Click **Create custom annotator**.
1.  Name your annotator, and then optionally add a description.
1.  From the **Annotator Type** menu, select **Machine learning**, and then click **Next**.
1.  Click **Select file** to find the .pear file that you exported.
1.  Specify a facet path, and then click **Save**.
