---

copyright:
  years: 2015, 2023
lastupdated: "2023-03-23"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Adding collections
{: #cm-add-collection}

You can add a collection directly to the Content Mining application.
{: shortdesc}

You might want to add a collection from within the Content Mining application to make data available for use as training data for a document classifier, for example.

The collection can contain an uploaded CSV file only. For information about file guidelines, see [Analyzing CSV files](/docs/discovery-data?topic=discovery-data-cm-csv-file).

The collection that you create is not added to your existing Content Mining project. A new Content Mining project is created to store the collection. The project that is generated is given the name that you specify for the collection.

To add a collection, complete the following steps:

1.  From the analysis view of your collection, click the **Collections** link in the breadcrumb to open the *Create a collection for your analytics solutions* page of the Content Mining application.

1.  Click **Create collection**.

1.  Drag your CSV file to the *Import your files* dialog, or click Open, to browse for the file. When the button is available, click **Next**.

1.  You can optionally customize the columns that you want to include or exclude from the collection, and adjust the data types of the fields from the *Fields* page. Click **Next**.

1.  From the *Enrichments* page, you can optionally apply or remove any enrichments from the collection, and then click **Next**.

    The *Part of Speech* enrichment is applied automatically.

1.  On the *Facets* page, you can optionally customize the data that is displayed for facets. Click **Next**.

1.  Click **Save** to save and index the collection.
