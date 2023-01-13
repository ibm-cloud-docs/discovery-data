---

copyright:
  years: 2015, 2023
lastupdated: "2022-08-19"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Exporting data
{: #cm-export}

If you discover insights as you analyze your data, you can export the data to share with others or analyze further in another business insights tool, for example.
{: shortdesc}

You can export your data as a CSV file or you can generate a separate JSON file for each record.

![Cloud Pak for Data only](images/desktop.png) For {{site.data.keyword.icp4dfull_notm}} only, you cannot export secured collections. For more information, see [Supporting document-level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).

To export your data, complete the following steps:

1.  From the *Documents* view, click the *Export* icon ![Export icon](images/cm-export-icon.png) in the toolbar.

1.  Complete the appropriate steps for the format in which you want to export the data.

    -   If you want to export the data in JSON format, complete the following steps:

        1.  Choose **Export JSON** to generate one JSON file for each record.
        1.  **Optional**: You can change the following values:

            -   Name. The file is named `export_document_{today's_date}` by default.
            -   Encoding. `UTF-8` is used by default.
            -   Choose whether to include fields and facets. They are excluded by default.

    -   If you want to export the data in CSV format, complete the following steps:

        1.  **Optional**: To customize the CSV output, choose **Export CSV with advanced options**.
        
            You can define the format of the following elements:

            -   Text content field: This is the main body field (or fields, if you configured more than one field with analyzable text). You can choose to exclude it from the export. It is exported as a column for a fact table by default.
            -   All other fields: You can choose to export them as columns for fact tables or export them as dimension tables. They are excluded from the export by default.
            -   Facets: You can choose to export the facets as separate CSV files that can be used as dimension tables. They are excluded from the export by default.

            After customizing the CSV format, click **Save**, and then click the *Export* icon from the toolbar again.

            If you use the same web browser to export data in CSV format again later, your saved settings are applied automatically.
            {: note}

        1.  Choose **Export CSV**.
        1.  **Optional**: You can change the following values:

            -   Name. The file is named `export_document_{today's_date}` by default.
            -   Encoding. `UTF-8` is used by default.
            -   Date and time format. `Unix epoch time` is used by default.

1.  Click **Export**.
