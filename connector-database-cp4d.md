---

copyright:
  years: 2019, 2024
lastupdated: "2023-04-05"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Database
{: #connector-database-cp4d}

Crawl documents that are stored in a database that supports the Java Database Connectivity (JDBC) API.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

## What documents are crawled
{: #connector-database-cp4d-docs}

- Each row in the database is crawled and added to the collection as one document. The columns are indexed as metadata.
- The crawler attempts to crawl and index content, such as BLOB/BINARY, that is stored in the database. File types that are supported by {{site.data.keyword.discoveryshort}} are indexed. For more information, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
- When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index.
- All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

## Data source requirements
{: #connector-database-cp4d-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements) for all installed deployments, your database data source must meet the following requirements:

-   {{site.data.keyword.discoveryshort}} supports the following data source versions:

    -   Data Virtualization on {{site.data.keyword.icp4dfull_notm}} 1.8.0, 1.8.3 which use Db2 11.5
    -   IBM Db2: 10.5, 11.1, 11.5
    -   Microsoft SQL Server: 2012, 2014, 2016, 2017
    -   Oracle Database: 12c, 18c, 19c
    -   PostgreSQL: 9.6, 10, 11

    Support for Data Virtualization was added with {{site.data.keyword.icp4dfull_notm}} 4.5.x releases
    {: note}

-   You must obtain any required service licenses for the data source that you want to connect to. For more information about licenses, contact the system administrator of the data source.

## Prerequisite step
{: #connector-database-cp4d-prereq}

-   Decide which database tables you want to crawl. You can crawl multiple tables in a collection, and you can specify tables that have different schemas, or sets of columns. You must know the following information:

    -   Schema names
    -   Table names

    For Data Virtualization on {{site.data.keyword.icp4dfull_notm}}, you can get these details from the {{site.data.keyword.icp4dfull_notm}} web client. Click the main menu icon, expand Data, and then select *Data virtualization*. At the start of the page, choose to show *Virtualized data*.

    ![Shows the Data virtualization view from Cloud Pak for Data](images/connector-db-dv.png){: caption="Virtualized data view in Cloud Pak for Data" caption-side="bottom"}

-   Be careful if you plan to crawl multiple tables that have columns with the same name but different data types. In Content Mining projects, columns with the same name but different data types are assigned to fields that have a data type suffix in the name, such as `DATA_string`. In all other project types, the data in one of the tables is excluded from the index. For example, if you have two tables that have columns that are called `DATA` and the `DATA` column in one table is populated with dates and the column in the other table is populated with strings, the data in one of the tables is excluded from the index.
-   Get the user credentials for a user who has permission to access the tables that you want to crawl.
-   Before you can connect to a database, you must get the JDBC driver library for the database. When you set up the database data source, you are asked to specify the JDBC driver class path.
-   Before you can connect to the Data Virtualization service by using JDBC, you must install IBM Data Server driver packages. For more information, see [Connecting applications to the Data Virtualization service](https://www.ibm.com/docs/SSQNUZ_4.5.x/svc-dv/connecting_apps_dv_service.html){: external}.
-   If you want to connect to an instance of Data Virtualization that is hosted in a different cluster from your {{site.data.keyword.discoveryshort}} service, you must forward traffic that is routed for Data Virtualization from an external infrastructure node to the master nodes of your cluster. For more information, see [Updating HAProxy configuration file](https://www.ibm.com/docs/SSQNUZ_4.5.x/svc-dv/dv-netreqs.html){: external}.

1.  Download the JAR files for the JDBC driver library from the database server or vendor's website.

    The following files are associated with each database:

    -   Db2 and Data Virtualization: `db2jcc4.jar`
    -   Oracle: `ojdbc8.jar`
    -   SQL Server: `mssql-jdbc-7.2.2.jre8.jar`
    -   PostgreSQL: `postgresql-42.2.6.jar`

1.  Compress the JAR files into a single compressed file.

    If you have a JDBC driver that has only one JAR file, skip this step.

1.  Make a note of where the driver is stored. You must specify the directory where you store this JAR or compressed file in the next procedure so that {{site.data.keyword.discoveryshort}} can upload it.

## Connecting to a database data source
{: #connector-database-cp4d-task}

Before you begin, if you plan to apply enrichments to your data, create the collection in a Content Mining project type. If you are using a different project type and plan to apply enrichments, stop here. For more information, see [Applying enrichments to content from a database](#connector-database-cp4d-enrich-db).
{: important}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Database**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents in the database is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  Complete the following fields in the *Enter your credentials* section:

    Database URL
    :   The URL of the database server.

        The following table shows example database URLs:

        | Database | Syntax | Example |
        |----------|--------|---------|
        | Data virtualization (same cluster) | `jdbc:db2://{fully-qualified-hostname-of-dv-service}:{jdbc-nonssl-internal-port}/bigsql` | `jdbc:db2://c-db2u-dv-db2u-engn-svc.myproject.svc.cluster.local:50000/bigsql` |
        | Data virtualization (separate cluster) | jdbc:db2://{cluster-address}:{jdbc-nonssl-external-port}/bigsql | jdbc:db2://api.conn.cp.example.com:30269/bigsql |
        | Db2 | `jdbc:db2://{server}:{port}/{database_name}` | `jdbc:db2://localhost:50000/sample:sslConnection=true;` |
        | Oracle | `jdbc:oracle:thin:@//{host}:{TCPport}/{service_name}` | `jdbc:oracle:thin:@localhost:1521/sample` |
        | SQL Server | `jdbc:sqlserver://{serverName}[\{instanceName}]:{port}[;property=value]` | `jdbc:sqlserver://localhost:1433;DatabaseName=sample` |
        | Postgresql | `jdbc:postgresql://{host}:{port}/{database}` | `jdbc:postgresql://localhost/sample` |
        {: caption="Example database URLs"}

    User
    :   The username that you obtain from the database you selected. You use this username to crawl the source. Your username is different from database to database.

    Password
    :   The password that is associated with your username. Your password is different from database to database.

1.  Complete the following fields in the *Connection settings* section:

    JDBC driver type
    :   Choose the database.

        **Db2** is selected by default. If you want to crawl from a database type that is not listed, select **OTHER**. To crawl data that is  managed by Data Virtualization on {{site.data.keyword.icp4dfull_notm}}, keep `Db2` selected.

    JDBC driver classname
    :   The JDBC driver class name that is associated with the database you selected. This field is autofilled, unless you select **OTHER**.

    JDBC driver classpath
    :   Upload a JDBC driver file, which can have a .jar or .zip file extension. Alternatively, you can reuse a .jar or .zip file that you uploaded previously.

1.  Complete the following fields in the *Specify what you want to crawl* section, and then click **Add**:

    Schema Name
    :   The schema that you want to crawl.
    
    Table Name
    :   The table within a schema that you want to crawl.

    Click the edit icon to specify more table crawl settings, including:

    Primary key
    :   The primary key of the target database table. If the primary key is not configured in the target database table, you must specify the key in this field. The JDBC database crawler appends this primary key value to the URL of each crawled row to keep its uniqueness. When the primary key is a composite key, concatenate the key names by using a comma, for example `key1,key2`. If unspecified, the project defaults to the primary key fields of the table. If the primary key is configured in the target database table, this key is automatically detected.

    Row filter
    :   Optional. Specify the `SQL WHERE` clause to designate which table rows to crawl. You must specify a Boolean expression that can be the condition of a `WHERE` clause in a `SELECT` statement. If there is an error in syntax or column names, the table is excluded from the crawl, and no documents are indexed.

    Column with data to extract
    :   Name of the column with data that you want to crawl. If you don't specify the column, a column with text or with a single large object is chosen to be crawled.

    MIME type of data
    :   Optional. The MIME type is detected if not specified.

    The values that you specify in the table crawl settings dialog are not displayed with the schema and tables names, but the values are applied to the database connection.

    The *Column with data to extract* and *MIME type of data* fields were added with the 4.6.5 release.
    {: note}

1.  If you want the crawler to extract text from images in documents, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.

### Using Windows Authentication on Linux
{: #connector-database-cp4d-ms-workaround}

The JDBC driver from Microsoft does not support Windows Authentication on Linux. If you want to use Microsoft Windows authentication to access your SQL Server on Linux, you can use a third-party JDBC driver called jTDS from [Sourceforge](http://jtds.sourceforge.net/){: external}. Specify the following values during the configuration:

- Database URL: `jdbc:jtds:sqlserver://<host>:<port>;databaseName=<database>;domain=<domain>;useNTLMv2=true;`
- JDBC driver type: `OTHER`
- JDBC driver class name: `net.sourceforge.jtds.jdbc.Driver`

## Applying enrichments to content from a database
{: #connector-database-cp4d-enrich-db}

If you use a database as your data source and want to apply enrichments to the nested fields that are indexed from the database, you must use a Content Mining project type.

If your goal is to create a search application by using a Document Retrieval project type, create a Content Mining project type first. From the Content Mining project, you can connect to the database and enrich the data. Then, you can reuse the enriched collection from a Document Retrieval project.

To enrich database content for use in a Document Retrieval project, complete the following steps:

1.  Create a Content Mining project.

    For more information, see [Creating a project](/docs/discovery-data?topic=discovery-data-projects).
1.  Connect to a database data source.

    For more information, see [Configuring a data source: Database](/docs/discovery-data?topic=discovery-data-collection-types#databaseconnect).
1.  Apply enrichments.

    For more information, see the following topics:

    -   [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain)
    -   [Applying prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu).
1.  Create a Document Retrieval project.

    For more information, see [Creating a project](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-projects).

    When you are prompted to choose a collection, choose **Reuse data from an existing collection**. If necessary, scroll to see this option.
    {: note}

1.  Select the collection that you created and enriched by using the Content Mining project, and then click **Finish**.
