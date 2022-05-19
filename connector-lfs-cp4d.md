---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-19"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Local File System
{: #connector-lfs-cp4d}

Crawl documents that are stored in a local file system.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

## What documents are crawled
{: #connector-lfs-cp4d-docs}

- Only documents that are supported by {{site.data.keyword.discoveryshort}} in your file path are crawled; all others are ignored. For more information, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
- When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index.
- All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

## Prerequisite steps
{: #connector-lfs-cp4d-prereq}

Before you connect to the Local File System data source, complete the following step:

- [Create a persistent volume claim on the crawler pod](#mount-persistent-volume)

The service uses Portworx storage by default. However, if you are using Network File System (NFS) storage, see [Prerequisite steps for NFS storage](#connector-lfs-cp4d-prereq-nfs) instead.

If you're using {{site.data.keyword.discoveryshort}} for {{site.data.keyword.icp4dfull_notm}} 2.1.4, see [Prerequisite steps for version 2.1.4 and earlier](#connector-lfs-cp4d-prereq-214).

### Creating and mounting a persistent volume claim on the crawler pod
{: #mount-persistent-volume}

Before you can crawl a local file system, you must create a persistent volume claim and mount it on the crawler pod. You also need to copy the files that you want to crawl to the {{site.data.keyword.discoveryshort}} cluster that you are working on. If you have multiple {{site.data.keyword.discoveryshort}} clusters, you must copy the files along with the `crawler-pvc-portworx.yaml` file that you will create in this task to each cluster.

Complete the following steps:

1.  Enter the following command to check the `storageclass` name of the Portworx provisioner:

    ```bash
    oc get storageclass | grep portworx-gp3-sc
    ```
    {: pre}

    You might see output similar to the following:

    ```bash
    NAME             PROVISIONER                    RECLAIMPOLICY  VOLUMEBINDINGMODE  ALLOWVOLUMEEXPANSION  AGE
    portworx-gp3-sc  kubernetes.io/portworx-volume  Retain         Immediate          true                  51d
    ```
    {: codeblock}

1.  Create a file named `crawler-pvc-portworx.yaml` to define the persistent volume claim (PVC) with the following content:

    ```yaml
    kind: PersistentVolumeClaim
    apiVersion: v1
    metadata:
      name: <name-of-portworx-pvc>
    spec:
      accessModes:
        - ReadWriteMany
      resources:
        requests:
          storage: 10Gi
      storageClassName: portworx-gp3-sc
    ```
    {: codeblock}

    Replace `<name-of-portworx-pvc>` with the name of your dynamic Portworx persistent volume claim. For example, `jdoe-pvc-portworx`

1. Enter the following command to create the persistent volume claim:

   ```bash
   oc create -f crawler-pvc-portworx.yaml
   ```
   {: pre}

   A message is displayed:

   ```bash
   persistentvolumeclaim/jdoe-pvc-portworx created
   ```
   {: codeblock}

1.  Enter the following command to mount the persistent volume claim to the crawler pod:

    ```bash
    oc patch wd wd --type=merge \
    --patch='{"spec": {"ingestion": {"crawler": {"mount": {"enabled": true, "persistentVolumeClaimName": "<name-of-portworx-pvc>" } } } } }'
    ```
    {: pre}

    Replace `<name-of-portworx-pvc>` with the name of your dynamic Portworx persistent volume claim. For example, `jdoe-pvc-portworx`.

1.  Enter the following command to copy the files that you want to crawl to your dynamic Portworx persistent volume claim.

    You only need to run this command one time against one of the existing crawler pods. The persistent volume claim is shared among all crawler and ingestion-api pods. Replace the variables in the command with the appropriate information.

    ```bash
    oc rsync <path-to-local-file-system-folder> <crawler-pod>:/mnt
    ```
    {: pre}

You mounted the persistent volume claim (PVC) and copied the files that you want to crawl to the PVC.

## Connecting to a local file system data source
{: #connector-lfs-cp4d-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Local File System**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents that you want to crawl is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1. In the *Specify what you want to crawl* section, enter the file path that you want to crawl in the **Path** field, and then click **Add**.

    The file path is case-sensitive.
1.  Optionally, add more file paths.
1.  If you want the crawler to extract text from images in documents, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1. Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.

## Prerequisite steps for NFS storage
{: #connector-lfs-cp4d-prereq-nfs}

Choose one of the following methods to enable the crawler pod to access the file system:

- [Configure an external NFS server](#use-external-nfs)
- [Configure dynamic provisioning with an NFS storage class](#dyn-prov-nfs)

### Configuring an external NFS server
{: #use-external-nfs}

If the local file system files or folders that you want to crawl are stored in an external Network File System (NFS), you can use the external NFS server to create the persistent volume claim.

1.  Create a file named `crawler-pv-nfs.yaml` with the following content:

    ```yaml
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: <persistent-volume-name>
      labels:
        pv-name: <persistent-volume-name>
    spec:
      capacity:
        storage: 10Gi
      accessModes:
        - ReadWriteMany
      persistentVolumeReclaimPolicy: Retain
      nfs:
        server: <NFS server hostname or IP address>
        path: <Path of NFS exported folder>
     ```
     {: codeblock}

    Replace references to `<persistent-volume-name>` with the name of your persistent volume. For example, `jdoe-nfs-pv` and add the missing external NFS details.

1.  Enter the following command to create the persistent volume claim:

    ```bash
    oc create -f crawler-pv-nfs.yaml
    ```
    {: pre}

    The following message is displayed:

    ```bash
    persistentvolume/jdoe-nfs-pv created
    ```
    {: codeblock}

1.  Create a file called `crawler-pvc-nfs.yaml` with the following content:

    ```yaml
    kind: PersistentVolumeClaim
    apiVersion: v1
    metadata:
      name: <persistent-volume-claim-name>
    spec:
      accessModes:
        - ReadWriteMany
      resources:
        requests:
          storage: 10Gi
      selector:
        matchLabels:
          pv-name: <persistent-volume-name>
    ```
    {: codeblock}

    Replace the following variables:

    - `<persistent-volume-claim-name>`: Specify the name of your persistent volume claim. For example, `jdoe-nfs-pvc`.
    - `<persistent-volume-name>`: Specify the name of your persistent volume. For example, `jdoe-nfs-pv`.

1.  Enter the following command to create the persistent volume claim:

    ```bash
    oc create -f crawler-pvc-nfs.yaml
    ```
    {: pre}

    The following message is displayed:

    ```bash
    persistentvolumeclaim/jdoe-nfs-pvc created
    ```
    {: codeblock}

1.  Enter the following command to mount the persistent volume claim to the crawler pod.

    This command also mounts the persistent volume claim to all ingestion-api pods. Replace `<persistent-volume-claim-name>` with the name of your persistent volume claim. For example, `jdoe-nfs-pvc`.

    ```bash
    oc patch wd wd --type=merge \
    --patch='{"spec": {"ingestion": {"crawler": {"mount": {"enabled": true, "persistentVolumeClaimName": "<persistent-volume-claim-name>" } } } } }'
    ```
    {: pre}

### Configuring dynamic provisioning with an NFS storage class
{: #dyn-prov-nfs}

If you want to crawl your local file system files or folders but you do not want to prepare an extra NFS server to store those files or folders, you can configure dynamic storage by using an NFS storage class.

For more information about storage providers that {{site.data.keyword.discoveryshort}} supports and for storage comparisons, see [Storage considerations](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/plan/storage_considerations.html){: external}.

Before you complete this task, copy the files that you want to crawl to the {{site.data.keyword.discoveryshort}} cluster that you are working on. If you have multiple {{site.data.keyword.discoveryshort}} clusters, you must copy the files along with the `crawler-pvc-dynamic.yaml` file that you create in this task to each cluster.

Complete the following steps:

1.  Enter the following command to check the `storageclass` name of the NFS provisioner:

    ```bash
    oc get storageclass
    ```
    {: pre}

    A message is displayed.

    ```bash
    NAME        PROVISIONER                                     RECLAIMPOLICY  VOLUMEBINDINGMODE  ALLOWVOLUMEEXPANSION  AGE
    nfs-client  cluster.local/innocence-nfs-client-provisioner  Delete         Immediate          true                  177m
    ```
    {: codeblock}

1.  Create a file that is named `crawler-pvc-dynamic.yaml` and add the following content to it:

    ```yaml
    kind: PersistentVolumeClaim
    apiVersion: v1
    metadata:
      name: <name-of-dynamic-pvc>
    spec:
      accessModes:
        - ReadWriteMany
      resources:
        requests:
          storage: 10Gi
      storageClassName: nfs-client
    ```
    {: codeblock}

    Replace `<name-of-dynamic-pvc>` with the name of your dynamic NFS persistent volume claim. For example, `jdoe-dynamic-pvc`.

1.  Enter the following command to create the persistent volume claim:

    ```bash
    oc create -f crawler-pvc-dynamic.yaml
    ```
    {: pre}

    A message is displayed.

    ```bash
    persistentvolumeclaim/jdoe-dynamic-pvc created
    ```
    {: codeblock}

1.  Enter the following command to mount the persistent volume claim to the crawler pod.

    This command also mounts the persistent volume claim to all ingestion-api pods.

    ```bash
    oc patch wd wd --type=merge \
    --patch='{"spec": {"ingestion": {"crawler": {"mount": {"enabled": true, "persistentVolumeClaimName": "<name-of-dynamic-pvc>" } } } } }'
    ```
    {: pre}

    Replace `<name-of-dynamic-pvc>` with the name of your dynamic NFS persistent volume claim in the previous step. For example, `jdoe-dynamic-pvc`.

1.  Enter the following command to copy the files that you want to crawl to your dynamic NFS persistent volume claim.

    You must run this command only one time against one of the existing crawler pods. The persistent volume claim is shared among all crawler and ingestion-api pods. Replace the variables in the command with the appropriate information.

    ```bash
    oc rsync <path-to-local-file-system-folder> <crawler-pod>:/mnt
    ```
    {: pre}

You mounted the persistent volume claim (PVC) and copied all of the files that you want to crawl to the PVC.

## Prerequisite steps for version 2.1.4 and earlier
{: #connector-lfs-cp4d-prereq-214}

If you have {{site.data.keyword.discoveryshort}} for {{site.data.keyword.icp4dfull_notm}} 2.1.4, choose one of the following methods to enable the crawler pod to access the file system:

- [Mount a persistent volume on the crawler pod](#mount-pv-orig)
- [Copy files from the crawler pod](#copy-local-folders)

### Mounting a persistent volume on the crawler pod on versions 2.1.4 and earlier
{: #mount-pv-orig}

If you do not want to copy your [Local File System](#configurelocalfilesystem) files or folders to the crawler pod, you can establish a link from your cluster to a remote Network File System (NFS), which you can configure to serve as a persistent volume and mount on the crawler pod. After you establish this link and after {{site.data.keyword.discoveryshort}} crawls your files, you can edit these files later so that, after the next crawl, your edits are automatically reflected in the index.
{: shortdesc}

If you plan to install {{site.data.keyword.discoveryshort}} version 2.1.4 and earlier, you must create and configure the persistent volume _before_ you install {{site.data.keyword.discoveryshort}}.
{: important}

Complete the following steps to create and mount a persistent volume on the crawler pod on your {{site.data.keyword.discoveryshort}} instance version 2.1.4 and earlier:

1. Create a file called `crawler-pv.yaml`. The content of the file looks like the following. Replace the `<>` and the content inside with the required information:

   ```yaml
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: "<label-name>"
     labels:
       "<label-name>": "<label-value>"
   spec:
     capacity:
       storage: "10Gi"
     accessModes:
       - ReadWriteMany
     persistentVolumeReclaimPolicy: Retain
     nfs:
       server: <NFS server hostname or IP address>
       path: <Path of NFS exported folder>
   ```
   {: codeblock}

1. Enter the following command to set `crawler-pv.yaml` as the persistent volume:

   ```bash
   create -f crawler-pv.yaml
   ```
   {: pre}

1. If you are using version 2.1.3 or 2.1.4, mount the persistent volume to the crawler pod by editing `override.yaml` to include the following input. This file overrides any default settings that you choose. In the `label` and `value` fields, you must use the same string that you specified when you created the `crawler-pv.yaml` file in step 1. Replace the `<>` and the content inside with the required information:

   ```yaml
   core:
     ingestion:
       mount:
         useDynamicProvisioning: false
         storageClassName: ""
         accessModes: "ReadWriteMany"
         selector:
           label: "<label-name>"
           value: "<label-value>"
   ```
   {: codeblock}

   If you are using a version earlier than 2.1.3, mount the persistent volume to the crawler pod by creating a file called `override.yaml` in `ibm-watson-discovery-ppa/deploy/`. You might see the following content in `override.yaml`:

   ```yaml
   core:
     ingestion:
       mount:
         useDynamicProvisioning: false
         storageClassName: ""
         selector:
           label: "<label-name>"
           value: "<label-value>"
   ```
   {: codeblock}

1. Install {{site.data.keyword.discoveryshort}} along with `override.yaml`. For more information about installing {{site.data.keyword.discoveryshort}}, see [Installing the Watson Discovery service](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_3.0.1/cpd/svc/watson/discovery-install.html){: external}. For more information about overriding values in `override.yaml` when you install {{site.data.keyword.discoveryshort}}, see [Override values for Watson Discovery installation](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_3.0.1/cpd/svc/watson/discovery-override.html){: external}.

   If you are using a version earlier than 2.1.3, from the `deploy` subdirectory, run the `deploy.sh` script by entering the `-d` flag, the file path to the files that you want to make accessible to `ibm-watson-discovery`, the `-O` flag, and your `override.yaml` file. You can also enter the `-e` flag with your `release-name-prefix`. If you do, your `release-name-prefix` must be 13 characters or fewer, or the installation will fail. If you do not enter the `-e` flag, the default `release-name-prefix` is `disco`. See the following example. Replace the `<>` and the content inside with the required information:

   ```bash
   ./deploy.sh -d </local root directory/subdirectory/>ibm-watson-discovery \
   -O ./override.yaml -e <release-name-prefix>
   ```
   {: codeblock}

   For a list of flags and their descriptions or for help, run `./deploy.sh -h`.
   {: tip}

For more information about copying your local files that you want to crawl to the crawler pod, see [Copying local file system files to the crawler pod on versions 2.1.4 and earlier](#copy-local-folders). For more information about the different ways of creating and mounting a persistent volume in all {{site.data.keyword.discoveryshort}} versions, see [Creating and mounting a persistent volume claim on the crawler pod](#mount-persistent-volume).

### Copying local file system files to the crawler pod on versions 2.1.4 and earlier
{: #copy-local-folders}

You can also copy your local files that you want to crawl to the crawler pod. Before you create a [Local File System collection](#configurelocalfilesystem), you must have the Red Hat OpenShift CLI, or `oc`, installed. For more information about installing the Red Hat OpenShift Origin CLI, see [Installing the Red Hat OpenShift Origin CLI (`oc`)](/docs/openshift?topic=openshift-openshift-cli#cli_oc).
{: shortdesc}

Complete the following steps to copy your local file system files to the crawler pod on an instance of {{site.data.keyword.discoveryshort}} versions 2.1.4 and earlier, replacing the `<>` and the content inside with the required information:

1.  Enter the following command to log on to your {{site.data.keyword.discoveryshort}} cluster:

    ```bash
    oc login https://<OpenShift administrative console URL> \
    -u <cluster-administrator> -p <password>
    ```
    {: pre}

1.  Enter the following command to switch to the proper namespace:

    ```bash
    oc project <discovery-install namespace>
    ```
    {: pre}

1.  Enter `oc get pods|grep crawler` to find the crawler pod. If you are using a version earlier than 2.1.3, enter `oc get pods|grep ingestion` to find the ingestion pod.
1. Enter the following command to copy the local file system folders that you want to crawl to the `/mnt` directory on the crawler pod:

    ```bash
    oc rsync <path to local file system folder> <crawler pod>:/mnt
    ```
    {: pre}

    If you are using a version of {{site.data.keyword.discoveryshort}} that is older than 2.1.3, enter the following command:

    ```bash
    oc rsync <path to local file system folder> <ingestion pod>:/mnt
    ```
    {: pre}

    In versions earlier than 2.1.3, the files that you copy apply to all of the gateway and ingestion pods. The default number of ingestion pods is 1.

    If you edit files that you copied to the ingestion or gateway pod, your changes are not reflected in the index after a recrawl, unless you recopy the edited files to the gateway or ingestion pod.
    {: important}

For more information about creating and mounting a persistent volume on the crawler pod on an instance of {{site.data.keyword.discoveryshort}} versions 2.1.4 and earlier, see [Mounting a persistent volume on the crawler pod on versions 2.1.4 and earlier](#mount-pv-orig). For more information about the different ways of creating and mounting a persistent volume in all {{site.data.keyword.discoveryshort}} versions, see [Creating and mounting a persistent volume claim on the crawler pod](#mount-persistent-volume).
