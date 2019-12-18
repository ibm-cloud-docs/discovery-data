---

copyright:
  years: 2019
lastupdated: "2019-11-27"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'} 
{:url: data-credential-placeholder='url'}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}
{:xml: .ph data-hd-programlang='xml'}
{:properties: .ph data-hd-programlang='properties'}

# Using a custom connector with the {{site.data.keyword.discovery-data_short}} tooling 
{: #ccs-tooling}

After you have built and deployed a custom connector, you can configure and run it in the {{site.data.keyword.discovery-data_short}} tooling to create a collection.
{: shortdesc}

You create and manage a collection as described in [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections). You can use a successfully deployed custom connector during this process as follows. These instructions enable you to use a custom connector instead of one of the pre-built connectors listed in [Configuring data sources](docs/discovery-data?topic=discovery-data-collections#collection-types).

  1. After you create a new project, including a name and project type, look on the **Select data source** page for your custom connector. Select the custom connector and click **Next**. The **Configure collection** page opens.

  The following steps apply specifically to the example custom connector that is shipped with the `custom_crawler_docs.zip` file.
  {: note}

  1. Enter values for the following fields on the **Configure collection** page. If a field is already populated with a value, verify and change the value if needed. A prepopulated value indicates that a value was specified in the custom connector's `template.xml` or `message.properties` file.
    - **General**
      - **Collection name**
      - **Collection language**
    - **Crawler properties**
      - **Crawler name**
      - **Crawler description**
      - **Time to wait between retrieval requests (milliseconds)** (default `0`)
      - **Maximum number of active crawler threads** (default `10`)
      - **Maximum number of documents to crawl** (default `2000000000`)
      - **Maximum document size (KB)** (default `32768`)
      - **When the crawler session is started**
        Selections include:
        - **Start crawling updates (look for new, modified, and deleted content)**
        - **Start crawling new and modified content**
        - **Start a full crawl**
      - **`{connector_name}`_GENERAL_SETTINGS_CUSTOM_CONFIG_CLASS_LABEL** (default `com.ibm.es.ama.custom.crawler.sample.sftp.SftpCrawler`)
      - **`{connector_name}`_GENERAL_SETTINGS_CUSTOM_CRAWLER_CLASS_LABEL** (default `com.ibm.es.ama.custom.crawler.sample.sftp.SftpCrawler`)
      - **`{connector_name}`_GENERAL_SETTINGS_CUSTOM_SECURITY_CLASS_LABEL** (default `com.ibm.es.ama.custom.crawler.sample.sftp.SftpCrawler`)
      - **`{connector_name}`_GENERAL_SETTINGS_DOCUMENT_LEVEL_SECURITY_SUPPORTED_LABEL** (default `On`)
      - **`{connector_name}`_GENERAL_SETTINGS_DOCUMENT_LEVEL_SECURITY_SSO_ENABLED_LABEL** (default `Off`)
      - **`{connector_name}`_GENERAL_SETTINGS_DOCUMENT_LEVEL_SECURITY_SCOPE_LABEL** (default `{host}:{:port}`)
    - **Data Source Properties**
      - **Host name** (default `localhost`)
      - **Port** (default `22`)
      - **User name**
      - **Use key file (or input password)** (default `On`)
      - **Key file location**
      - **passphrase**
      - **Password**
    - **Space filter**
      - **Path filter** (default `/`)
      - **Level** (default `1`)
    - **Crawl space Properties**
  1. Click **Finish** to create the collection with the custom connector and the values specified for it.
  1. Continue with the instructions in [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections) and its subsequent topics.