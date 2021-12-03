---

copyright:
  years: 2019, 2021
lastupdated: "2021-12-01"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Overview of Cloud Pak for Data data sources
{: #collection-types}

<!-- 2.1.3 c/s help for the *Select a Data Source* page CP4D. Do not delete. -->

In {{site.data.keyword.discovery-data_short}}, you can crawl documents from a local source that you upload or from a remote data source that you connect to. Learn more about the supported data sources and how to configure them.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments. For more information about {{site.data.keyword.cloud_notm}} data sources, see [Overview of the {{site.data.keyword.cloud_notm}} data sources](/docs/discovery-data?topic=discovery-data-sources).
{: note}

All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.
{: important}

You can use {{site.data.keyword.discovery-data_short}} to crawl from the following data sources:

- [Box](/docs/discovery-data?topic=discovery-data-connector-box-cp4d)
- [Database](/docs/discovery-data?topic=discovery-data-connector-database-cp4d)
- [FileNet P8](/docs/discovery-data?topic=discovery-data-connector-filenet-cp4d)
- [LDAP directory](/docs/discovery-data?topic=discovery-data-connector-ldap-cp4d)
- [Local File System](/docs/discovery-data?topic=discovery-data-connector-lfs-cp4d)
- [Notes](/docs/discovery-data?topic=discovery-data-connector-notes-cp4d)
- [Salesforce](/docs/discovery-data?topic=discovery-data-connector-salesforce-cp4d)
- [SharePoint Online](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cp4d)
- [SharePoint OnPrem](/docs/discovery-data?topic=discovery-data-connector-sharepoint-onprem-cp4d)
- [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cp4d)
- [Windows File System](/docs/discovery-data?topic=discovery-data-connector-wfs-cp4d)

*Your data source isn't listed?* You can work with a developer to create a custom connector. For more information, see [Building a Cloud Pak for Data custom connector](/docs/discovery-data?topic=discovery-data-build-connector).

If you have special requirements when adding source documents, such as a need to exclude certain files, you can work with a developer to create a custom crawler plug-in. The crawler plug-in can apply more nuanced rules to what documents and what fields in the documents get added. For more information, see [Building a Cloud Pak for Data custom crawler plug-in](/docs/discovery-data?topic=discovery-data-crawler-plugin-build).

## Data source requirements
{: #requirements}

The following requirements and limitations are specific to {{site.data.keyword.discoveryfull}}:

- The individual file size limit is 32 MB per file, which includes compressed archive files (ZIP, CZIP, TAR). When decompressed, the individual files within compressed files cannot exceed 32 MB per file. This limit is the same for collections in which you upload your own data.
- When optical character recognition (OCR) is enabled, images must meet the minimum image quality requirement of 75 DPI (dots per inch) to be processed successfully.
- Depending on the type of installation (default or production mode), the number of collections you can ingest simultaneously varies. A default installation includes one crawler pod, which allows three collections to be processed simultaneously. A production installation includes two crawler pods, which can process six collections simultaneously.

     If you are running a default installation and you want to process more than three collections simultaneously, you must increase the number of crawler pods by running the following commands:

     ```bash
     oc patch wd wd --type=merge --patch='{"spec": {"ingestion": {"crawler": {"replicas": <number-of-replicas> } } } }'
     ```
     {: pre}

     In a default installation, the maximum number of simultaneous collections that can perform a crawl is 3. If you start a fourth, that collection does not start to process until the prior three crawls finish.
     {: note}

     Each `number-of-replicas` allows 3 simultaneous crawls, so `number-of-replicas=2` increases the replicas to 6, and `number-of -replicas=3` increases them to 9.

## Crawler plug-in settings
{: #plugin-settings}

When you deploy one or more crawler plug-ins, you can configure your collection to use one of the plug-ins.

These settings are only available when crawler plug-ins are deployed.

- For more information about building a plug-in, see [Building a Cloud Pak for Data crawler plug-in](/docs/discovery-data?topic=discovery-data-crawler-plugin-build).
- For more information about deploying a crawler plug-in, see [Commands and options for managing your crawler plug-ins](/docs/discovery-data?topic=discovery-data-manage-plugin#mng-plugin-cmd-opt).

When you are ready to configure a collection to use a crawler plug-in that was created by using the `scripts/manage_crawler_plugin.sh` script, you can see a *Plug-in settings* section with the following options:

- **Enable plug-in**: By default, this switch is set to **Off**. Enable this option if you want to use a crawler plug-in to process documents.
- **Plug-in**: Lists the names of available crawler plug-ins. Select a plug-in to use.

## Supporting document-level security
{: #configuredls}

If document-level security is activated, you can use the security settings from your source documents to control the search results that are returned to different users.

{{site.data.keyword.discoveryshort}} supports prefiltering only. To prefilter, {{site.data.keyword.discoveryshort}} replicates the document's source access control list (ACL) at crawl time into the index. The search engine must compare user credentials to the replicated document ACLs. {{site.data.keyword.discoveryshort}} is faster when documents are prefiltered and when you control which documents you add to the index. However, it is difficult to model all of the security policies of the various data sources in the index and implement comparison logic uniformly. Also, prefiltering is not as responsive to changes that occur in the source ACLs after the most recent crawl.

Document-level security is supported by the following data source types:

- Box
- FileNet P8
- HCL Notes
- Microsoft SharePoint Online
- Microsoft SharePoint OnPrem
- Microsoft Windows File System

To enable document-level security, you must complete the following steps:

1.  [Create {{site.data.keyword.discoveryshort}} users that match the users available on the source system](#createusersdls).
1.  [Associate users with your {{site.data.keyword.discoveryshort}} instance](#associateusersdls).
1.  Enable document-level security for the data source when you connect to it.

### Creating users for document-level security
{: #createusersdls}

You must create users that match the users available on the source system that {{site.data.keyword.discoveryshort}} is connecting to so that they can query with document-level security enabled.
{: shortdesc}

1. Log in to {{site.data.keyword.discoveryshort}} as an administrator.
1. Create users who match the users available on your source or who are connected to the LDAP server that your source system uses. If you create users for document-level security, keep the following points in mind:

   - Optional: For each user who you want to access query results, you must add users. The username must match the username that the source uses. This option is only for development and testing purposes. To create users individually, see [Managing users](https://www.ibm.com/docs/en/cloud-paks/cp-data/3.5.0?topic=platform-managing-users){: external}.
   - To connect to an LDAP server that the source is using, see [Connecting to your LDAP server](https://www.ibm.com/docs/en/cloud-paks/cp-data/3.5.0?topic=users-connecting-your-ldap-server){: external}.

### Associating users with an instance
{: #associateusersdls}

1. Click the main menu icon, expand **Services**, and then click **Instances**.
1. Find instance that you want to add users to. Click the overflow menu, and then select **Manage Access**.
1. Click **Add users**.
1. Add the users that you want from the list by clicking **Add user**, and then select the user from the list. Assign them to the **User** role, and then click **Add**.

When you query collections where document-level security is enabled, no results are returned if the users associated with your {{site.data.keyword.discoveryshort}} instance are not present in the source system. For more information about querying these collections, see [Querying with document-level security enabled](/docs/discovery-data?topic=discovery-data-query-concepts#querydls).
{: important}

{{site.data.keyword.discoveryshort}} does not synchronize changes that are made to the users in the LDAP server with the user list for the service. {{site.data.keyword.discoveryshort}} administrators must ensure that the user list is current and remove any non-current users.
{: note}
