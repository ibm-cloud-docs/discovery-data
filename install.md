---

copyright:
  years: 2019, 2020
lastupdated: "2020-05-13"

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

Requirements and installation information for {{site.data.keyword.discovery-data_long}}.
{: shortdesc}

You should install {{site.data.keyword.icp4dfull}} before installing the {{site.data.keyword.discovery-data_short}} service.

{{site.data.keyword.icp4dfull_notm}} is available for download from [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/){: external} 

Full installation instructions for {{site.data.keyword.discovery-data_long}} are available at [Installing {{site.data.keyword.discovery-data_short}}](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/svc/watson/discovery-install.html){: external}


## Before you begin
{: #beforebegin}

Review the security information in:

[{{site.data.keyword.discovery-data_long}} installation](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/svc/watson/discovery-install.html){: external}

[Security considerations in {{site.data.keyword.icp4dfull_notm}} 2.5.0.0](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/plan/security.html){: external}

Encryption of data at rest must be handled by the storage provider.
{: important}

Review the {{site.data.keyword.discovery-data_short}} release notes and known issues:

[Release notes](/docs/discovery-data?topic=discovery-data-release-notes)

## Software requirements
{: #prereqs}

{{site.data.keyword.icp4dfull_notm}} 2.1.0.2 or 2.5.0.0 or later, including the IBM Cloud Pak CLI.

See the general software requirements listed here:

  -  [IBM® Cloud Pak for Data 2.5.0.0](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/plan/rhos-reqs.html#rhos-reqs__software){: external} 
  -  [IBM® Cloud Pak for Data 2.1.0.2](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/preinstall-overview.html){: external}
 

Portworx **must** be installed before you install {{site.data.keyword.discovery-data_short}}. A Portworx license is included with {{site.data.keyword.icp4dfull}} 2.5.0.0.
{: important}

## System requirements
{: #system-requirements}

See the system requirements listed here:

  -  [IBM® Cloud Pak for Data 2.5.0.0](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/plan/rhos-reqs.html){: external} 
  -  [IBM® Cloud Pak for Data 2.1.0.2](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/preinstall-overview.html){: external}


{{site.data.keyword.discovery-data_short}} has the following specific requirements:

|                      | Minimum VPC available | Minimum RAM available |
|----------------------|:---------------------:|:---------------------:|
| Development (non-HA) | 21                    | 86 GB                 |
| Production (HA)      | 26                    | 116 GB                |

Gluster File System (GlusterFS) is not a supported storage option for {{site.data.keyword.discovery-data_long}}.
{: note}

## Upgrading Discovery for Cloud Pak for Data
{: #upgrade-discovery}

To upgrade {{site.data.keyword.discovery-data_long}}, you must uninstall the current version, then install the newer version.

For uninstall instructions, see [Uninstalling Watson Discovery](https://github.com/ibm-cloud-docs/data-readmes/blob/master/discovery-README.md#uninstalling-watson-discovery){: external}.

See [Backing up and restoring data](/docs/discovery-data?topic=discovery-data-backup-restore) for the procedures to back up and restore user data.