---

copyright:
  years: 2019
lastupdated: "2019-11-27"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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


# Installing Discovery bundle for Cloud Pak for Data
{: #install}

Follow these instructions to install and configure {{site.data.keyword.discovery-data_long}}.
{: shortdesc}

If you have already installed {{site.data.keyword.icp4dfull}}, and have purchased {{site.data.keyword.discovery-data_short}} as an add-on, follow the [instructions listed here](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/svc/watson/discovery-install.html){: external}

Gluster File System (GlusterFS) is not a supported storage option for {{site.data.keyword.discovery-data_long}}.
{: note}

## Before you begin
{: #beforebegin}

Review the following topics that relate to cluster security:

[Security in {{site.data.keyword.icp4dfull}}](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/svc/watson/discovery-install.html){: external}

Encryption of data at rest must be handled by the storage provider.
{: important}

## Software requirements
{: #prereqs}

- {{site.data.keyword.icp4dfull_notm}} 2.5.0.0 or later, including the IBM Cloud Pak CLI
- Kubernetes 1.12.4 or later
- Helm 2.9.1 or later

Because the installation of the chart needs to be performed from the command line, you must install and configure the following command-line tools:

  - [`cloudctl`](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_cli.html){: external}
  - [`kubectl`](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}
  - [`helm`](https://helm.sh){: external}

See the general software requirements listed in [Pre-installation tasks](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/install/preinstall-overview.html){: external}.

## System requirements
{: #system-requirements}

See the system requirements listed in [Pre-installation tasks](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/install/preinstall-overview.html){: external}.

{{site.data.keyword.discovery-data_short}} has the following specific requirements:
  - Minimum CPU: 20 for dev, 40 for HA
  - Minimum RAM: 92GB for dev, 124GB for HA
  - Cluster configuration:
       -  Dev: 1 load balancing node, 3 master nodes, 3 worker nodes
       -  HA: 1 load balancing node, 3 master nodes, 4 worker nodes

## Installing the service bundle
{: #installing}

Perform the following steps to install {{site.data.keyword.discovery-data_short}}.

1. Download and install the {{site.data.keyword.icp4dfull_notm}} package as described in [Installing IBM Cloud Pak for Data](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/svc/watson/discovery-install.html){: external}
1. Download the IBM Watson {{site.data.keyword.discovery-data_short}} package in `.tgz` format from [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/){: external} and follow the [installation instructions listed here](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.5.0/cpd/svc/watson/discovery-install.html){: external}
