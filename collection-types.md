---

copyright:
  years: 2019, 2025
lastupdated: "2024-06-05"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Overview of Cloud Pak for Data data sources
{: #collection-types}



In {{site.data.keyword.discovery-data_short}}, you can crawl documents from a local source that you upload or from a remote data source that you connect to. Learn more about the supported data sources and how to configure them.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} **{{site.data.keyword.icp4dfull_notm}} only**

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
- [SharePoint On Prem](/docs/discovery-data?topic=discovery-data-connector-sharepoint-onprem-cp4d)
- [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cp4d)
- [Windows File System](/docs/discovery-data?topic=discovery-data-connector-wfs-cp4d)

*Your data source isn't listed?* You can work with a developer to create a custom connector. For more information, see [Building a Cloud Pak for Data custom connector](/docs/discovery-data?topic=discovery-data-build-connector).

If you have special requirements when you add source documents, such as a need to exclude certain files, you can work with a developer to create a custom crawler plug-in. The crawler plug-in can apply more nuanced rules to what documents and what fields in the documents get added. For more information, see [Building a Cloud Pak for Data custom crawler plug-in](/docs/discovery-data?topic=discovery-data-crawler-plugin-build).

## Setting up the HTTP proxy configuration in the air gap environment [IBM Cloud Pak for Data]{: tag-cp4d}
{: #sethttpproxyae}

When {{site.data.keyword.discoveryshort}} is running in the air gap environment, you must set up HTTP proxy to connect to the external servers.

You can crawl from the following data sources by using an HTTP proxy server in an air-gapped environment:

- [Box](/docs/discovery-data?topic=discovery-data-connector-box-cp4d)
- [Salesforce](/docs/discovery-data?topic=discovery-data-connector-salesforce-cp4d)
- [SharePoint Online](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cp4d)
- [SharePoint On Prem](/docs/discovery-data?topic=discovery-data-connector-sharepoint-onprem-cp4d)
- [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cp4d)

You can either use the specific proxy settings for each data source type or the system-wide proxy settings that are provided by resource specification injection (RSI) from CPD 5.0.0.

1. Run the following command to install the RSI webhook.
    ```bash
    $ cpd-cli manage install-rsi --cpd_instance_ns=${PROJECT_CPD_INST_OPERANDS}
    ```
    For more information, see [Install RSI](https://www.ibm.com/docs/en/cloud-paks/cp-data/5.0.x?topic=manage-install-rsi){: external}.
1. Run the following command to enable the RSI webhook.
    ```bash
    $ cpd-cli manage enable-rsi --cpd_instance_ns=${PROJECT_CPD_INST_OPERANDS}
    ```
    For more information, see [Enable RSI](https://www.ibm.com/docs/en/cloud-paks/cp-data/5.0.x?topic=manage-enable-rsi){: external}.
1. Run the following command to set up the proxy configuration.
    ```bash
    $ cpd-cli manage create-proxy-config \
        --cpd_instance_ns=${PROJECT_CPD_INST_OPERANDS} \
        --proxy_host=$PROXY_HOST \
        --proxy_port=$PROXY_PORT \
        --proxy_user=$PROXY_USER \
        --proxy_password=$PROXY_PASSWORD
    ```
    For more information, see [Manage proxy configuration](https://www.ibm.com/docs/en/cloud-paks/cp-data/5.0.x?topic=manage-create-proxy-config){: external}.
1. Run the following command to enable the proxy configuration.
    ```bash 
    $ cpd-cli manage enable-proxy --cpd_instance_ns=${PROJECT_CPD_INST_OPERANDS}
    ```
    For more information, see [Enable proxy configuration](https://www.ibm.com/docs/en/cloud-paks/cp-data/5.0.x?topic=manage-enable-proxy){: external}.

For more information about applying proxy settings to an air-gapped cluster, see [Applying cluster HTTP proxy settings to IBM Cloud Pak for Data](https://www.ibm.com/docs/en/cloud-paks/cp-data/5.0.x?topic=environment-applying-cluster-http-proxy-settings){: external}.

Following are the specific requirements and limitations that are related to HTTP proxy servers:
- HTTP proxy servers that require TLS communication are not supported.
- HTTP proxy servers that require authentication are necessary for:
    - SharePoint On Prem
    - SharePoint Online with User principal
- HTTP proxy servers must support NTLM when the target web and SharePoint On Prem servers require NTLM authentication.
- HTTP proxy servers must support the LDAP protocol for SharePoint On Prem document-level security.

## Data source requirements
{: #requirements}

The following requirements and limitations are specific to {{site.data.keyword.discoveryfull}}:

- The individual file size limit is 32 MB per file, which includes compressed archive files (ZIP, CZIP, TAR). When decompressed, the individual files within compressed files cannot exceed 32 MB per file. This limit is the same for collections in which you upload your own data.
- Depending on the type of installation (starter or production mode), the number of collections you can ingest simultaneously varies. A starter installation includes one `crawler` pod, which allows three collections to be processed simultaneously. A production installation includes two `crawler` pods, which can process six collections simultaneously.

     If you are running a starter installation and you want to process more than three collections simultaneously, you must increase the number of `crawler` pods by running the following commands:

     ```bash
     oc patch wd wd --type=merge --patch='{"spec": {"ingestion": {"crawler": {"replicas": <number-of-replicas> } } } }'
     ```
     {: pre}

     In a starter installation, the maximum number of simultaneous collections that can crawl an external data source is 3. If you start a fourth, that collection does not start to process until the prior three crawls finish.
     {: note}

     Each `number-of-replicas` allows 3 simultaneous crawls, so `number-of-replicas=2` increases the replicas to 6, and `number-of -replicas=3` increases them to 9.

## Crawler plug-in settings
{: #plugin-settings}

When you deploy one or more crawler plug-ins, you can configure your collection to use one of the plug-ins.

These settings are only available when crawler plug-ins are deployed.

- For more information about building a plug-in, see [Building a Cloud Pak for Data crawler plug-in](/docs/discovery-data?topic=discovery-data-crawler-plugin-build).
- For more information about deploying a crawler plug-in, see [Commands and options for managing your crawler plug-ins](/docs/discovery-data?topic=discovery-data-manage-plugin#mng-plugin-cmd-opt).

When you are ready to configure a collection to use a crawler plug-in that was created by using the `scripts/manage_crawler_plugin.sh` script, you can see a *Plug-in settings* section with the following options:

- **Enable plug-in**: The switch is set to **Off**. Enable this option if you want to use a crawler plug-in to process documents.
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
- Microsoft SharePoint On Prem
- Microsoft Windows File System

When you query collections where document-level security is enabled, no results are returned if the users associated with your {{site.data.keyword.discoveryshort}} instance are not present in the source system. For more information about querying these collections, see [Querying with document-level security enabled](/docs/discovery-data?topic=discovery-data-query-concepts#querydls).
{: important}

To enable document-level security, you must complete the following steps:

1.  [Create {{site.data.keyword.discoveryshort}} users that match the users available on the source system](#createusersdls).
1.  Associate users with your {{site.data.keyword.discoveryshort}} instance. For more information, see [Giving users access to a Watson Discovery instance](https://www.ibm.com/docs/SSQNUZ_4.6.x/svc-discovery/discovery-admin-add-users.html){: external}.
1.  Enable document-level security for the data source when you connect to it.

### Creating users for document-level security
{: #createusersdls}

You must create users that match the users available on the source system that {{site.data.keyword.discoveryshort}} is connecting to so that they can query with document-level security enabled.
{: shortdesc}

1. Log in to {{site.data.keyword.discoveryshort}} as an administrator.
1. Create users who match the users available on your source or who are connected to the identity provider that your source system uses. If you create users for document-level security, keep the following points in mind:

   - Optional: For each user that you want to have access to query results, you must add users. The username must match the username that the source uses. This option is only for development and testing purposes. To create users individually, see [Managing users](https://www.ibm.com/docs/SSQNUZ_4.6.x/cpd/admin/users.html){: external}.
   - To connect to an identity provider that the source is using, see [Connecting to your identity provider](https://www.ibm.com/docs/SSQNUZ_4.6.x/cpd/admin/ldap.html){: external}.

{{site.data.keyword.discoveryshort}} does not synchronize changes that are made to the users in the identity provider with the user list for the service. {{site.data.keyword.discoveryshort}} administrators must ensure that the user list is current and remove any noncurrent users.
{: note}
