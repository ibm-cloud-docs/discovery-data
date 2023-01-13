---

copyright:
  years: 2019, 2023
lastupdated: "2022-09-28"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Local File System
{: #connector-lfs-cp4d}

Crawl documents that are stored in a local file system.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} **{{site.data.keyword.icp4dfull_notm}} only**

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

### Creating and mounting a persistent volume claim on the crawler pod
{: #mount-persistent-volume}

Before you can crawl a local file system, you must create a persistent volume claim and mount it on the `crawler` pod. You also need to copy the files that you want to crawl to the {{site.data.keyword.discoveryshort}} cluster that you are working on. If you have multiple {{site.data.keyword.discoveryshort}} clusters, you must copy the files along with the `crawler-pvc-portworx.yaml` file that you will create in this task to each cluster.

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

1.  Enter the following command to mount the persistent volume claim to the `crawler` pod:

    ```bash
    oc patch wd wd --type=merge \
    --patch='{"spec": {"ingestion": {"crawler": {"mount": {"enabled": true, "persistentVolumeClaimName": "<name-of-portworx-pvc>" } } } } }'
    ```
    {: pre}

    Replace `<name-of-portworx-pvc>` with the name of your dynamic Portworx persistent volume claim. For example, `jdoe-pvc-portworx`.

1.  Enter the following command to copy the files that you want to crawl to your dynamic Portworx persistent volume claim.

    You only need to run this command one time against one of the existing `crawler` pods. The persistent volume claim is shared among all `crawler` and `ingestion-api` pods. Replace the variables in the command with the appropriate information.

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

Choose one of the following methods to enable the `crawler` pod to access the file system:

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

1.  Enter the following command to mount the persistent volume claim to the `crawler` pod.

    This command also mounts the persistent volume claim to all `ingestion-api` pods. Replace `<persistent-volume-claim-name>` with the name of your persistent volume claim. For example, `jdoe-nfs-pvc`.

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

1.  Enter the following command to mount the persistent volume claim to the `crawler` pod.

    This command also mounts the persistent volume claim to all `ingestion-api` pods.

    ```bash
    oc patch wd wd --type=merge \
    --patch='{"spec": {"ingestion": {"crawler": {"mount": {"enabled": true, "persistentVolumeClaimName": "<name-of-dynamic-pvc>" } } } } }'
    ```
    {: pre}

    Replace `<name-of-dynamic-pvc>` with the name of your dynamic NFS persistent volume claim in the previous step. For example, `jdoe-dynamic-pvc`.

1.  Enter the following command to copy the files that you want to crawl to your dynamic NFS persistent volume claim.

    You must run this command only one time against one of the existing `crawler` pods. The persistent volume claim is shared among all `crawler` and `ingestion-api` pods. Replace the variables in the command with the appropriate information.

    ```bash
    oc rsync <path-to-local-file-system-folder> <crawler-pod>:/mnt
    ```
    {: pre}

You mounted the persistent volume claim (PVC) and copied all of the files that you want to crawl to the PVC.
