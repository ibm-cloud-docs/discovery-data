---

copyright:
  years: 2019
lastupdated: "2019-07-01"

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

Follow these instructions to install and configure IBM Watson&trade; {{site.data.keyword.discovery-data_short}} for {{site.data.keyword.icp4dfull}}.
{: shortdesc}

If you have already installed {{site.data.keyword.icp4dfull}}, and have purchased {{site.data.keyword.discovery-data_short}} as an add-on, follow the [instructions listed here](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/watson/discovery-install.html)

## Before you begin
{: #beforebegin}

Review the following topics that relate to cluster security:

[Security in {{site.data.keyword.icp4dfull}}](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/watson/discovery-install.html){: external}

Encryption of data at rest must be handled by the storage provider.
{: important}

## Software requirements
{: #prereqs}

- {{site.data.keyword.icp4dfull_notm}} 2.1.0 or later, including the IBM Cloud Pak CLI
- Kubernetes 1.12.4 or later
- Helm 2.9.1 or later

Because the installation of the chart needs to be performed from the command line, you must install and configure the following command-line tools:

  - [`cloudctl`](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_cli.html){: external}
  - [`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}
  - [`helm`](https://helm.sh){: external}

See the general software requirements listed in [Pre-installation tasks](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/preinstall-overview.html){: external}.

## System requirements
{: #system-requirements}

See the system requirements listed in [Pre-installation tasks](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/preinstall-overview.html){: external}.

{{site.data.keyword.discovery-data_short}} has the following specific requirements:
  - Minimum CPU: 2200m
  - Minimum memory: 10.25Gi

## Installing the service bundle
{: #installing}

Perform the following steps to install {{site.data.keyword.discovery-data_short}}.

1. Download and install the {{site.data.keyword.icp4dfull_notm}} package as described in [Installing IBM Cloud Pak for Data](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/ovu.html){: external}.

  When installing {{site.data.keyword.icp4dfull_notm}}, specifying the following in the `wdp.conf` file will automatically configure NFS storage.
    ```
    nfs_server=172.16.28.28
    nfs_dir=/data
    ```
  {: tip}

1. Download the IBM Watson {{site.data.keyword.discovery-data_short}} package in `.tgz` format from [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/){: external} and follow the [installation instructions listed here](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/watson/discovery-install.html) 