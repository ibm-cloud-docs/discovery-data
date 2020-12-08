---

copyright:
  years: 2019, 2020
lastupdated: "2020-12-04"

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
{:curl: .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}
{:external: target="_blank" .external}


# Installing Discovery for Cloud Pak for Data
{: #install}

![Cloud Pak for Data only](images/cpdonly.png) Requirements and installation information for {{site.data.keyword.discovery-data_short}}.
{: shortdesc}

You should install {{site.data.keyword.icp4dfull}} before installing the {{site.data.keyword.discovery-data_short}} service.

| Service version | {{site.data.keyword.icp4dfull}} version |
| ---- | ----|
| {{site.data.keyword.discoveryshort}} 2.2.0, 2.1.4 | {{site.data.keyword.icp4dfull}} 3.5.0 |
| {{site.data.keyword.discoveryshort}} 2.1.4, 2.1.3 | {{site.data.keyword.icp4dfull}} 3.0.1 |
| {{site.data.keyword.discoveryshort}} 2.1.2, 2.1.1, 2.1.0 | {{site.data.keyword.icp4dfull}} 2.5.0 |

{{site.data.keyword.icp4dfull_notm}} 3.0.1 deprecated support for Red Hat OpenShift 4.3 on 1 September 2020. {{site.data.keyword.icp4dfull_notm}} supports Red Hat OpenShift 4.5. The [IBM Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external} will work with any customers who have already installed {{site.data.keyword.icp4dfull_notm}} 3.0.1 on Red Hat OpenShift 4.3. New customers who want to install on Red Hat OpenShift 4.x are instructed to install Red Hat OpenShift 4.5.
{: important}

Full installation instructions: 

-  [Installing {{site.data.keyword.discoveryfull}} on {{site.data.keyword.icp4dfull}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-discovery/discovery-install-overview.html){: external}

Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.discovery-data_short}} offerings purchased on or after August 30, 2019. FISMA support is also available to those who purchased the June 28, 2019 version and upgrade to the August 30, 2019 (or later) version. {{site.data.keyword.discoveryfull}} is FISMA High Ready.

For complete information about **Cloud Pak for Data administration**, see [Administering the cluster for Cloud Pak for Data](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/cpd/admin/admin-cluster.html){: external} and [Administering the Cloud Pak for Data web client](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/cpd/admin/admin-web-client.html){: external}.
{: important}


## Before you begin
{: #beforebegin}

Review the security information in:

  -  [Security on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/support/knowledgecenter/SSQNUZ_latest/cpd/plan/security.html){: external} and [Installing the {{site.data.keyword.discoveryfull}} service](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-discovery/discovery-install-overview.html){: external}
  
  
Encryption of data at rest must be handled by the storage provider.
{: important}

Review the {{site.data.keyword.discoveryshort}} release notes and known issues:

  -  [Release notes](/docs/discovery-data?topic=discovery-data-release-notes)
  -  [Known issues](/docs/discovery-data?topic=discovery-data-known-issues)

## Software requirements
{: #prereqs}

{{site.data.keyword.icp4dfull_notm}} 2.1.0.2 or 2.5.0.0 or later, including the {{site.data.keyword.icp4dfull_notm}} CLI.

See the general software requirements listed here:

  -  [Software requirements](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/cpd/plan/rhos-reqs.html#rhos-reqs__software){: external} 
  

Portworx **must** be installed before you install {{site.data.keyword.discoveryshort}}. A Portworx license is included with {{site.data.keyword.icp4dfull}} 2.5.0.0 or later.
{: important}

## System requirements
{: #system-requirements}

See the system requirements listed here:

  -  [System requirements for IBM Cloud Pak for Data](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/cpd/plan/rhos-reqs.html){: external} 
  

Gluster File System (GlusterFS) is not a supported storage option for {{site.data.keyword.discoveryfull}}.
{: note}

## Upgrading Discovery for Cloud Pak for Data
{: #upgrade-discovery}

To upgrade {{site.data.keyword.discoveryfull}}, you must uninstall the current version, then install the newer version.

For uninstall instructions, see:

  -  [Uninstalling {{site.data.keyword.discovery-data_short}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-discovery/discovery-uninstall.html){: external}

  
See [Backing up and restoring data](/docs/discovery-data?topic=discovery-data-backup-restore) for the procedures to back up and restore user data in {{site.data.keyword.discovery-data_short}}.