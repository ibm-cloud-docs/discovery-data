---

copyright:
  years: 2019, 2021
lastupdated: "2021-07-19"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Using a custom Cloud Pak for Data connector from the Discovery user interface
{: #ccs-tooling}

After you build and deploy a custom connector, you can configure and run it in the {{site.data.keyword.discoveryshort}} user interface to create a collection.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

You create and manage a collection as described in [Creating and managing collections](/docs/discovery-data?topic=discovery-data-collections). You can use a successfully deployed custom connector during this process as follows. Follow these instructions to use a custom connector instead of one of the pre-built connectors that are listed in [Configuring Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types).

1.  After you create a project, look for your custom connector to connect to a data source.
1.  Select the custom connector and then click **Next**.

    The **Configure collection** page opens.

    The following steps apply specifically to the example custom connector that is included with the `custom-crawler-docs.zip` file.
    {: note}

1.  Enter values for the following fields on the **Configure collection** page. If a field is already populated with a value, verify and change the value if needed. A prepopulated value indicates that a value was specified in the custom connector's `template.xml` or `message.properties` file.

    - **General**
      - **Collection name**
      - **Collection language**
      - **Crawl schedule**
    - **Crawler properties**
      - **Crawler name**
      - **Crawler description**
      - **Time to wait between retrieval requests (milliseconds)** (default `0`)
      - **Maximum number of active crawler threads** (default `10`)
      - **Maximum number of documents to crawl** (default `2000000000`)
      - **Maximum document size (KB)** (default `32768`)
    - **Data Source Properties**
      - **Host name** (default `localhost`)
      - **Port** (default `22`)
      - **User name**
      - **Use key file (or input password)** (default `On`)
      - **Key file location**
      - **passphrase**
      - **Password**
    - **Crawl space Properties**

    If the custom crawler supports document-level security and the `document_level_security_supported` value in the `template.xml` is set to `true`, then an **Enable Document Level Security** switch is displayed in a *Security* section of the data source connection setup page. To enable document-level security, set the **Enable Document Level Security** switch to **On**. If the switch is set to Off, then the collection that is created cannot support document-level security even if the custom crawler can support document-level security.

1.  Click **Finish** to create the collection.