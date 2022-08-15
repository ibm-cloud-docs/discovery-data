---

copyright:
  years: 2015, 2022
lastupdated: "2022-08-15"

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

1.  From the *Documents* view, click the *Export* icon in the toolbar.

    ![Export icon](images/cm-export-icon.png){: caption="Figure 1. Export icon" caption-side="bottom"} 

1.  Choose the format in which to export the data. The options include:

    -   JSON:  Generates one JSON file for each record.
    -   CSV: Generates a CSV file.
    <!---   CSV with advanced options: Generates a CSV file that excludes any fields or facets that you choose to exclude from the export.-->

1.  You can optionally change the following values:

    -   Name. The file is named `export_document_{today's_date}` by default.
    -   Encoding. `UTF-8` is used by default.
    -   For CSV files only, you can specify the date and time format. `Unix epoch time` is used by default.
    -   For JSON files only, you can choose to include fields and facets. They are excluded by default.

1.  Click **Export**.
