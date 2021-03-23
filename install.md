---

copyright:
  years: 2019, 2021
lastupdated: "2021-03-23"

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

Requirements and installation information for {{site.data.keyword.discovery-data_short}}.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{:note}

You should install {{site.data.keyword.icp4dfull}} before installing the {{site.data.keyword.discovery-data_short}} service.

| Service version | {{site.data.keyword.icp4dfull}} version 
| ---- | ---- | ---- |
| {{site.data.keyword.discoveryshort}} 2.2.1 | {{site.data.keyword.icp4dfull}} 3.5.0 or 3.0.1 on Red Hat OpenShift 3.11.188 or later </br> {{site.data.keyword.icp4dfull}} 3.5.0 or 3.0.1 on Red Hat OpenShift 4.6 or later |
| {{site.data.keyword.discoveryshort}} 2.2.0 | {{site.data.keyword.icp4dfull}} 3.5.0 or 3.0.1 on Red Hat OpenShift 3.11.188 or later </br> {{site.data.keyword.icp4dfull}} 3.5.0 or 3.0.1 on Red Hat OpenShift 4.5 or later | 
| {{site.data.keyword.discoveryshort}} 2.1.4 | {{site.data.keyword.icp4dfull}} 3.0.1 on Red Hat OpenShift 3.11.188 or later </br> {{site.data.keyword.icp4dfull}} 2.5 on Red Hat OpenShift 3.11 |   
| {{site.data.keyword.discoveryshort}} 2.1.3 | {{site.data.keyword.icp4dfull}} 3.0.1 on Red Hat OpenShift 3.11.188 or later </br> {{site.data.keyword.icp4dfull}} 2.5 on Red Hat OpenShift 3.11 |   

{{site.data.keyword.icp4dfull_notm}} 3.0.1 deprecated support for Red Hat OpenShift 4.3 on 1 September 2020. {{site.data.keyword.icp4dfull_notm}} supports Red Hat OpenShift 4.5. The [IBM Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external} will work with any customers who have already installed {{site.data.keyword.icp4dfull_notm}} 3.0.1 on Red Hat OpenShift 4.3. New customers who want to install on Red Hat OpenShift 4.x are instructed to install Red Hat OpenShift 4.5.
{: important}

Full installation instructions: 

-  [Installing {{site.data.keyword.discoveryfull}} on {{site.data.keyword.icp4dfull}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-discovery/discovery-install.html){: external}

Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.discovery-data_short}} offerings purchased on or after August 30, 2019. FISMA support is also available to those who purchased the June 28, 2019 version and upgrade to the August 30, 2019 (or later) version. {{site.data.keyword.discoveryfull}} is FISMA High Ready.

For complete information about **Cloud Pak for Data administration**, see [Administering the cluster for Cloud Pak for Data](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/cpd/admin/admin-cluster.html){: external} and [Administering the Cloud Pak for Data platform](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/cpd/admin/admin-web-client.html){: external}.
{: important}


## Before you begin
{: #beforebegin}

Review the security information in:

  -  [Security on {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/cpd/plan/security.html){: external} and [Installing the {{site.data.keyword.discoveryfull}} service](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-discovery/discovery-install.html){: external}
  
  
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

## Custom scaling in Watson Discovery
{: #scaling-discovery}

You can perform custom scaling on pods in {{site.data.keyword.discoveryshort}} 2.2.0. For more information, see [Scaling services](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/cpd/admin/scaling-svcs.html){: external} 

1. To update the replicas, create a yaml file that specifies the number of replicas for the target pods. For example, to increase the number of replicas of the `API gateway` pod, create the following yaml file:
   
   ```
   spec:
     api:
       replicas: 2
   ```
   {: codeblock}

1. Apply the file by using the `oc patch` command:
   
   ```bash
   oc patch wd wd --patch "$(cat $file_name)" --type='merge'
   ```
   {: codeblock}

**Parameters list for each pod:**

**UI pods**
   
   ```
   spec:
     tooling:
       minerapp:
         replicas:
       tooling:
         replicas:
   ```
   {: codeblock}

**API gateway pod**
   
   ```
   spec:
     api:
       replicas:
   ```
   {: codeblock}

**Elastic search pods**
   
   ```
   spec:
     elasticsearch:
       clientNode:
         replicas:
       dataNode:
         replicas:
       masterNode:
         replicas:
   ```
   {: codeblock}

**Hadoop worker pod**
   
   ```
   spec:
     hdp:
       worker:
         replicas:
   ```
   {: codeblock}

**Crawler pod**
   
   ```
   spec:
     ingestion:
       crawler:
         replicas:
   ```
   {: codeblock}

**Analyze API pod**
   
   ```
   spec:
     statelessapi:
       runtime:
         replicas:
   ```
   {: codeblock}

**Watson Knowledge Studio model enrichment pod**
   
   ```
   spec:
     wksml:
       replicas:
   ```
   {: codeblock}

## Upgrading Discovery for Cloud Pak for Data
{: #upgrade-discovery}

To upgrade versions of {{site.data.keyword.discoveryfull}} that are earlier than 2.2.0, you must uninstall the current version and then install the newer version.

For uninstall instructions, see:

  -  [Uninstalling {{site.data.keyword.discovery-data_short}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-discovery/discovery-uninstall.html){: external}

{{site.data.keyword.discovery-data_short}} supports an in-place upgrade from version 2.2.0 to 2.2.1 only, so you do not need to uninstall version 2.2.0 and install version 2.2.1. For information about preparing your {{site.data.keyword.discovery-data_short}} clusters for the upgrade, upgrading your {{site.data.keyword.discovery-data_short}} instance, and verifying that the upgrade was successful, see [Preparing to upgrade your Watson Discovery clusters](/docs/discovery-data?topic=discovery-data-install#prepare-clusters), [Upgrading your Watson Discovery instance](/docs/discovery-data?topic=discovery-data-install#upgrade-instance), and [Verifying that your upgrade completed successfully](/docs/discovery-data?topic=discovery-data-install#verify-upgrade), respectively.
  
For the procedures to back up and restore user data in {{site.data.keyword.discovery-data_short}}, see [Backing up and restoring data](/docs/discovery-data?topic=discovery-data-backup-restore).

### Preparing to upgrade your Watson Discovery clusters
{: #prepare-clusters}

Before you upgrade your {{site.data.keyword.discovery-data_short}} 2.2.0 instance, you must prepare your {{site.data.keyword.discovery-data_short}} clusters for the upgrade so that you know if you need to create or update any resources on the clusters. If you do not prepare your clusters, your upgrade will fail.
{: shortdesc}

As you prepare your clusters for the upgrade, you do not need to pause or stop any in-flight operations, such as crawling, ingesting documents, or training a query model. This upgrade performs a rolling update of each component in your instance without any downtime.
{: note}

Complete the following steps to prepare your {{site.data.keyword.discovery-data_short}} clusters that are connected to the internet for the upgrade from version 2.2.0 to 2.2.1:

1. From your installation node, navigate to the directory where you placed the {{site.data.keyword.icp4dfull}} CLI and the `repo.yaml` file.
1. Enter the following command to log in to your Red Hat OpenShift cluster as an administrator:
   
   ```
   oc login <OpenShift_URL:port>
   ```
   {: pre}

   where `<OpenShift_URL:port>` is the URL that you use when you log in to your OpenShift cluster.
1. Enter the following command to verify that {{site.data.keyword.discovery-data_short}} 2.2.0 is already installed and is in a `Ready` state:

   ```
   ./cpd-cli status -a watson-discovery -n <Project>
   ```
   {: pre}

   in which `<Project>` is the namespace where your {{site.data.keyword.discovery-data_short}} 2.2.0 instance is installed.
1. Enter the following command to view the list of resources that you must create or update on the cluster:

   ```
   ./cpd-cli adm \
   --repo ./repo.yaml \
   --assembly watson-discovery \
   --arch x86_64 \
   --version 2.2.1 \
   --namespace <Project> \
   --latest-dependency
   ```
   {: pre}

   where `<Project>` is the namespace where your {{site.data.keyword.discovery-data_short}} 2.2.0 instance is installed.

1. Re-enter the command in step 4, and include the `--apply` flag to create or update the necessary resources on your cluster:

   ```
   ./cpd-cli adm \
   --repo ./repo.yaml \
   --assembly watson-discovery \
   --arch x86_64 \
   --version 2.2.1 \
   --namespace <Project> \
   --latest-dependency
   --apply
   ```
   {: pre}

Now that you made the necessary changes to your cluster, you can upgrade your {{site.data.keyword.discovery-data_short}} 2.2.0 instance to 2.2.1. For more information, see [Upgrading your Watson Discovery instance](/docs/discovery-data?topic=discovery-data-install#upgrade-instance).

### Upgrading your Watson Discovery instance
{: #upgrade-instance}

Before you upgrade, you do not need to pause or stop any in-flight operations, such as crawling, ingesting documents, or training a query model. This upgrade performs a rolling update of each component in your instance without any downtime.
{: note}

You can perform an in-place upgrade of your {{site.data.keyword.discovery-data_short}} instance only from version 2.2.0 to 2.2.1. After you complete the task in [Preparing to upgrade your Watson Discovery clusters](/docs/discovery-data?topic=discovery-data-install#prepare-clusters), complete the following steps to upgrade your instance of {{site.data.keyword.discovery-data_short}} from version 2.2.0 to 2.2.1:

1. From your installation node, navigate to the directory where you placed the {{site.data.keyword.icp4dfull}} CLI and the `repo.yaml` file.
1. Enter the following command to log in to your Red Hat OpenShift cluster as an administrator:
   
   ```
   oc login <OpenShift_URL:port>
   ```
   {: pre}

   where `<OpenShift_URL:port>` is the URL that you use when you log in to your OpenShift cluster.
1. Enter the following command to view a summary of changes that take effect after you upgrade the service:
   
   ```
   ./cpd-cli upgrade \
   --repo ./repo.yaml \
   --assembly watson-discovery \
   --version 2.2.1
   --arch x86_64 \
   --namespace <Project> \
   --transfer-image-to <Registry_location> \
   --cluster-pull-prefix <Registry_from_cluster> \
   --ask-pull-registry-credentials \
   --ask-push-registry-credentials \
   --latest-dependency \
   --dry-run
   ```
   {: pre}

   where `<Project>` is the namespace where your {{site.data.keyword.discovery-data_short}} 2.2.0 instance is installed, where `<Registry_location>` is the location of the images that you pushed to the registry server, and where `<Registry_from_cluster>` is the location from which pods on the cluster can pull images.
   
   If you want to obtain the internal name of the Red Hat OpenShift registry service, enter the following command: `oc registry info --internal=true`. If you have Red Hat OpenShift 4.5 or later, the default service name is `image-registry.openshift-image-registry.svc:5000/<Project>`, and if you have Red Hat OpenShift 3.11, the default service name is `docker-registry.default.svc:5000/<Project>`. When you enter a value for the `<Registry_from_cluster>` variable, append the `<Project>` name to the end of the route, as shown in the previous service name examples.

   If you are using the internal Red Hat OpenShift registry and the default self-signed certificate, enter the `--insecure-skip-tls-verify` flag to prevent 509 errors.
   {: important}

   If you are using `cpd-cli` version 3.5.1 or earlier, enter the `--storageclass Storage_class_name` option. You do not need to enter this option for `cpd-cli` versions 3.5.2 and later.
   {: important}

   If you used the override file when you installed {{site.data.keyword.discovery-data_short}}, enter the `--override` option, and specify the same override file that you used during installation.
   {: important}

1. Re-enter the command from step 3 without the `--dry-run` flag to upgrade your {{site.data.keyword.discovery-data_short}} instance.

### Verifying that your upgrade completed successfully
{: #verify-upgrade}

1. From your installation node, enter the following command to obtain the {{site.data.keyword.discovery-data_short}} assembly status:

   ```
   ./cpd-cli status \
   --assembly watson-discovery \
   --namespace <Project>
   ```
   {: pre}

   in which `<Project>` is the namespace where your {{site.data.keyword.discovery-data_short}} 2.2.1 instance is installed. If the status is `Not Ready`, it might take several minutes before the assembly status indicates `Ready`. If the status is `Failed`, you can get help by creating a case from [IBM Cloud Support](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.
1. Enter the following command to verify the `WatsonDiscovery` custom resource status:

   ```
   oc get WatsonDiscovery wd
   ```
   {: pre}
   
   If the value of `Ready` equals `True` and the value of `Updating` equals `False`, the upgrade is complete.
