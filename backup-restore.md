---

copyright:
  years: 2020, 2023
lastupdated: "2023-05-02"

keywords: backup,restore

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Backing up and restoring data in Cloud Pak for Data
{: #backup-restore}

Use the following procedures to back up and restore data in your {{site.data.keyword.discovery-data_long}} instance.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d}

This information applies only to installed deployments.
{: note}

You use the same set of backup and restore scripts to back up and restore data in any of the supported upgrade paths. The backup script stores the version number of the service with data to back up from the existing deployment. The restore script detects the version of the service that is installed on the new {{site.data.keyword.icp4dfull_notm}} deployment, and then follows the appropriate steps to restore data to the detected version.

The following table lists the upgrade paths that are supported by the scripts.

| Version in use | Version that you can upgrade to |
|----------------|----------------------------|
| 4.6.0 | 4.6.5 |
| 4.5.x | 4.6.0 |
| 4.0.x | 4.6.0 |
| 2.2.1 | 4.6.0 |
{: caption="Supported upgrade paths" caption-side="top"}

If you are upgrading from 4.x to 4.6.x, a simpler way to complete the upgrade is described in the following topics:

-  [Upgrading Watson {{site.data.keyword.discoveryshort}} from Version 4.6](https://www.ibm.com/docs/SSQNUZ_4.6.x/svc-discovery/discovery-upgrade-v46.html){: external}.
-  [Upgrading Watson {{site.data.keyword.discoveryshort}} from Version 4.5.x](https://www.ibm.com/docs/SSQNUZ_4.6.x/svc-discovery/discovery-upgrade-v45.html){: external}.
-  [Upgrading Watson {{site.data.keyword.discoveryshort}} from Version 4.0.x](https://www.ibm.com/docs/SSQNUZ_4.6.x/svc-discovery/discovery-upgrade-v4.html){: external}.

If you use {{site.data.keyword.icp4dfull_notm}} Red Hat OpenShift APIs for Data Protection (OADP) backup and restore utility to back up and restore an entire cluster to 4.6, a few extra steps are required. For more information, see [Using OADP to back up a cluster where {{site.data.keyword.discoveryshort}} is installed](#backup-restore-oadp).

You can do an in-place upgrade from one 4.6.x version to a later 4.6.y version. For more information, see [Upgrading Watson {{site.data.keyword.discoveryshort}} from Version 4.6.x to a later 4.6 refresh](https://www.ibm.com/docs/SSQNUZ_4.6.x/svc-discovery/discovery-upgrade-v46.html){: external}.

You can do an in-place upgrade from one 4.5.x version to a later 4.5.y version. For more information, see [Upgrading Watson {{site.data.keyword.discoveryshort}} to the latest Version 4.5 refresh](https://www.ibm.com/docs/SSQNUZ_4.5.x/svc-discovery/discovery-upgrade-v45x.html){: external}.

You can do an in-place upgrade from one 4.0.x version to a later 4.0.y version. For more information, see [Upgrading Watson {{site.data.keyword.discoveryshort}} to a newer 4.0 refresh](https://www.ibm.com/docs/SSQNUZ_4.0/svc-discovery/discovery-upgrade-v4.html){: external}.

## Process overview
{: #overview}

At a high level, the process includes the following steps:

1.  Back up your {{site.data.keyword.discoveryshort}} data by using the backup script.
1.  Install the latest version of {{site.data.keyword.icp4dfull_notm}}.
1.  Install the latest version of the {{site.data.keyword.discoveryshort}} service on the cluster.
1.  Restore the backed-up {{site.data.keyword.discoveryshort}} data by using the restore script.

## Back up and restore limitations
{: #bnr-restrictions}

You cannot migrate the following data:

-   Dictionary suggestions models. These models are created when you build a dictionary. The dictionary is included in the backup, but the term suggestions model is not. Reprocess the migrated collections to enable dictionary term suggestions.
-   You cannot back up and restore curations or migrate them because curations are a beta feature.

You can back up and restore some data by using the backup and restore scripts, but you must back up and restore other data manually. The following data must be backed up manually:

-   Local file system folders and documents that you can crawl by using the Local file system data source.

The following updates are made when your collections are restored:

-   Any collection that contains documents that were created by uploading data are automatically recrawled and reindexed when restored. These documents are assigned new document ID numbers in the restored collections.
-   Collections that were used in *Content Mining* projects are automatically recrawled and reindexed when restored. Only documents that are added by uploading data are assigned new document ID numbers in the restored collections.

## Back up and restore methods
{: #backup-restore-methods}

You can back up and restore your instance of {{site.data.keyword.discoveryshort}} manually or by using scripts.

-   [Using the backup scripts](#wddata-backup)
-   [Using the restore scripts](#wddata-restore)
-   [Backing up data manually](#backup-user-data)
-   [Restoring data manually](#restore-user-data)

You must have Administrative access to the {{site.data.keyword.discoveryshort}} instance on your {{site.data.keyword.discoveryshort}} cluster (where the data to be backed up is stored) and administrative access to the new instance (where the data will be restored to).

The backup and restore scripts complete many operations and can take quite a bit of time to run. To avoid timeout issues, run a tool that prevents timeouts, such as `nohup`.
{: important}

## Using the backup scripts
{: #wddata-backup}

Because changes to the data stored in {{site.data.keyword.discoveryfull}} during a backup can cause the backup to become corrupted and unusable, no in-flight requests are allowed during the backup period.

An in-flight request is any {{site.data.keyword.discoveryfull}} action that processes data, including the following actions:

-   Source crawl (scheduled or unscheduled)
-   Ingesting documents
-   Training a trained query model

The amount of storage that is available in the node where you run the backup script must be 3 times as large as the largest backup file in the data store that you plan to back up. If your data store is large, consider using a persistent volume claim instead of relying on the node's ephemeral storage. For more information, see [Configuring jobs to use PVC](#pvc).
{: attention}

Complete the following steps to back up {{site.data.keyword.discoveryfull}} data by using the backup scripts:

1.  Enter the following command to set the current namespace where your {{site.data.keyword.discoveryshort}} instance is deployed:

    ```bash
    oc project <namespace>
    ```
    {: pre}

1.  Get the backup script from the [GitHub repository](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/latest){: external}.

    You need all of the files in the repository to complete a backup and restore. Follow the instructions in GitHub Help to clone or download a compressed file of the repository.
    {: important}

1.  Make each script an executable file by running the following command:

    ```bash
    chmod +x <name-of-script>
    ```
    {: pre}

    Replace `<name-of-script>` with the name of the script.

1.  Run the `all-backup-restore.sh` script.

    ```bash
    ./all-backup-restore.sh backup [ -f backup_file_name ] [--pvc]
    ```
    {: pre}    

    The `-f backup_file_name` parameter is optional. The name `watson_discovery_<timestamp>.backup` is used if you don't specify a name.

    The `--pvc` parameter is optional. For more information about when to use it, see [Configuring jobs to use PVC](#pvc). By default, the backup and restore scripts create a `tmp` directory in the current directory that the script uses for extracting or compressing backup files.

    If you run into issues with the backup, rerun the backup command and include the `--use-job` parameter. This parameter instructs the backup script to use a Kubernetes job to back up ElasticSearch and MinIO in addition to Postgres, which uses a Kubernetes job by default. If the size of the data in ElasticSearch and MinIO is large and ephemeral storage is insufficient, include the `--pvc` option. When you do so, the script uses the persistent volume claim that is specified with the `--pvc` option instead of the `emptyDir` ephemeral storage as the temporary working directory for the job.

### Extracting files from the backup archive file
{: #backup-unpack}

The scripts generate an archive file, including the backup files of the services that are listed in Step 1. 

1.  You can extract files from the archive file by running the following command:

    ```bash
    tar xvf <backup_file_name>
    ```
    {: pre}

### Configuring jobs to use PVC
{: #backup-pvc}

The backup and restore process uses Kubernetes jobs. The jobs use ephemeral volumes that use ephemeral storage. It is a temporary storage mount on the pod that uses local storage of a node. In rare cases, the ephemeral storage is not large enough. You can optionally instruct the job to mount a Persistent Volume Claim (PVC) on its pod to use for storing the backup data. To do so, specify the `--pvc` option when you run the script. The scripts use `emptyDir` of Kubernetes otherwise.

In most cases, you don't need to use a persistent volume. If you choose to use a persistent volume, the volume must be 3 times as large as the largest backup file in the data store. The size of the data store's backup file depends on usage. After you create a backup, you can [extract files from the archive file](#backup-unpack) to check the file sizes. 

Also, you must have 2 times as much disk space available on the local system as the size of the data store because the archive of the data is split and then recombined to prevent issues that might otherwise occur when you copy large files from the cluster node to the local system.

### Mapping multitenant clusters
{: #backup-mapping}

When you restore data that was backed up from a version earlier than 4.0.6 to any later release and the backed-up deployment had more than one instance of the service provisioned, an extra step is required. You must create a JSON file that maps the service instance IDs between the backed-up cluster and the cluster where the data is being restored.

This mapping step is not required if the instance IDs did not change between the back up and restore steps. For example, you can skip this step if you are restoring data to the same cluster where it was backed up from or if you are restoring data to a brand new cluster that has no {{site.data.keyword.discoveryshort}} instances.

To create a mapping, complete the following steps:

1.  Extract the mapping template file from the backup archive file.

    ```bash
    tar xf <backup_file_name> tmp/instance_mapping.json -O > <mapping_file_name> 
    ```
    {: pre}    

1.  Make a list of the names and instance IDs of the service instances that are provisioned to the cluster where the data is being restored.

    The instance ID is part of the URL that is specified in the instance summary page. From the {{site.data.keyword.icp4dfull_notm}} web client main menu, expand Services, and then click Instances. Find your instance, and then click it to open its summary page. Scroll to the *Access information* section of the page, and look for the instance ID in the *URL* field.

    For example, `https://<host_name>/wd/<namespace>-wd/instances/<instance_id>/api`.

    Repeat this step to make a note of the instance ID for every instance that is provisioned.

1.  Edit the mapping file. 

    Add the instance IDs for the destination service instances that you listed in the previous step. The following snippet is an example of a mapping file.

    ```json
    {
      "instance_mappings": [
        {
          "display_name": "discovery-1",
          "source_instance_id": "1644822491506334",
          "dest_instance_id": "<new_instance_id>"
        },
        {
          "display_name": "discovery-2",
          "source_instance_id": "1644822552830325",
          "dest_instance_id": "<new_instance_id>"
        }
      ]
    }
    ```
    {: codeblock}

When you run the restore script, include the optional `--mapping` parameter to apply this mapping file when the data is restored.

## Using the restore scripts
{: #wddata-restore}

If you are restoring data from a version earlier than 4.0.6 and you are restoring a multitenant cluster to a multitenant cluster, you must take an extra step before you begin. For more information, see [Mapping multitenant clusters](#backup-mapping).
{: important}

Complete the following steps to restore data in {{site.data.keyword.discoveryfull}} by using the restore scripts:

1.  Enter the following command to set the current namespace where your {{site.data.keyword.discoveryshort}} instance is deployed:

    ```bash
    oc project <namespace>
    ```
    {: pre}

1.  If you haven't already, get the restore script from the [GitHub repository](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/latest){: external}.

    You need all of the files in the repository to complete a back up and restore. Follow the instructions in GitHub Help to clone or download a compressed file of the repository.
    {: important}

1.  Make each script an executable file by running the following command:

    ```bash
    chmod +x <name-of-script>
    ```
    {: pre}

    Replace `<name-of-script>` with the name of the script.

1.  Restore the data from the backup file on your local system to the new {{site.data.keyword.discoveryshort}} deployment by running the following command:

    ```bash
    ./all-backup-restore.sh restore -f backup_file_name [--pvc] [--mapping]
    ```
    {: pre}

    The `--pvc` parameter is optional. For more information about when to use it, see [Configuring jobs to use PVC](#backup-pvc).

    The `--mapping` parameter is optional. For more information about when to use it, see [Mapping multitenant clusters](#backup-mapping).

    By default, the backup and restore scripts create a `tmp` directory in the current directory that the script uses for extracting or compressing backup files. If you used the `--use-job` parameter when you backed up the data, specify it again when you restore the data. This parameter instructs the backup script to use a Kubernetes job to back up ElasticSearch and MinIO.

    The `gateway`, `ingestion`, `orchestrator`, `hadoop worker`, and `controller` pods automatically restart.

## Using OADP to back up a cluster where {{site.data.keyword.discoveryshort}} is installed
{: #backup-restore-oadp}

If you plan to back up and restore an entire {{site.data.keyword.icp4dfull_notm}} instance by using the {{site.data.keyword.icp4dfull_notm}} Red Hat OpenShift APIs for Data Protection (OADP) backup and restore utility, you must do some additional steps in the right order for the utility to work properly when {{site.data.keyword.discoveryshort}} is present.

1.  Run the {{site.data.keyword.discoveryshort}} backup script.

1.  Use the OADP backup utility to back up the cluster.

1.  Delete the project. This process removes the persistent volume claims and persistent volumes that are associated with {{site.data.keyword.discoveryshort}}.

1.  Use the OADP backup utility to restore the cluster.

1.  Uninstall {{site.data.keyword.discoveryshort}}, and then install {{site.data.keyword.discoveryshort}} again on the restored cluster.

    A repeat of the installation is required because the utility does not always reinstall {{site.data.keyword.discoveryshort}} correctly.
    {: note}

1.  Run the {{site.data.keyword.discoveryshort}} restore script to restore your data.

### Backing up data manually
{: #backup-user-data}

Manually back up data that is not backed up by using the scripts.

To manually back up your data from an instance of {{site.data.keyword.discoveryshort}}, complete the following steps:

1.  Enter the following command to log on to your {{site.data.keyword.discoveryshort}} cluster:

    ```bash
    oc login https://<OpenShift administrative console URL> \
    -u <cluster administrator username> -p <password>
    ```
    {: pre}

1.  Enter the following command to switch to the proper namespace:

    ```bash
    oc project <discovery-install namespace>
    ```
    {: pre}

1.  Enter `oc get pods|grep crawler`.

1.  Enter the following command:

    ```bash
    oc cp <crawler pod>:/mnt <path-to-backup-directory>
    ```
    {: pre}

### Restoring data manually
{: #restore-user-data}

Manually restore data that cannot be restored by using the script.

To manually restore your data from an instance of {{site.data.keyword.discoveryshort}}, complete the following steps:

1.  Enter the following command to log on to your {{site.data.keyword.discoveryshort}} cluster:

    ```bash
    oc login https://<OpenShift administrative console URL> \
    -u <cluster administrator username> -p <password>
    ```
    {: pre}

1.  Enter the following command to switch to the proper namespace:

    ```bash
    oc project <discovery-install namespace>
    ```
    {: pre}

1.  Enter `oc get pods|grep crawler`.

1.  Enter the following command:

    ```bash
    oc cp <path-to-backup-directory> <crawler pod>:/mnt
    ```
    {: pre}
