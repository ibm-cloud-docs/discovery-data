---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-31"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Backing up and restoring data in Cloud Pak for Data
{: #backup-restore}

Use the following procedures to back up and restore data in your {{site.data.keyword.discovery-data_long}} instance.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

These procedures are for advanced users who have experience with administering {{site.data.keyword.discovery-data_short}} clusters. You do not need to back up and restore data as part of standard use or maintenance.
{: important}

You can back up your data from and restore it to the following versions:

- 4.0.x to 4.0.y
- 2.2.1 to 4.0.x
- 2.2.0 to 4.0.x

You can do an in-place upgrade from one 4.0.x version to a later 4.0.y version as an alternative to following the procedures in this topic. For more information, see [Upgrading Watson Discovery to a newer 4.0 refresh](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=discovery-upgrading-watson-version-40){: external}.
{: note}

If you plan to backup and restore an entire Cloud Pak for Data instance by using the Cloud Pak for Data OpenShift® APIs for Data Protection (OADP) backup and restore utility, you must apply a patch before you start the backup. The patch stops Discovery from preventing the utility from completing successfully.

1.  Download the `wd-aux-br-patch.zip` file from the [Watson Developer Cloud Github](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/discovery-data/2.2.0/wd-aux-br-patch.zip) repository.
1.  Extract the `wd-aux-br-patch.yaml` file from the ZIP file.
1.  Run the following command in a terminal that is logged in to the cluster:

    ```bash
    oc create -f wd-aux-br-patch.yaml
    ```
    {: pre}

For more information about backing up and restoring data in previous versions, see [Backing up and restoring data to 2.2.1 or earlier releases](/docs/discovery-data?topic=discovery-data-backup-restore-prior).

## Process overview
{: #overview}

At a high level, the process includes the following steps:

1.  Back up your {{site.data.keyword.discoveryshort}} data by using the backup script or manually or both.
1.  Install the latest version of the {{site.data.keyword.icp4dfull_notm}}.
1.  Install the latest version of the {{site.data.keyword.discoveryshort}} service on the cluster.
1.  Restore the backed-up {{site.data.keyword.discoveryshort}} data by using the restore scripts or manually or both.

## Back up and restore limitations
{: #bnr-restrictions}

You cannot migrate the following data:

- Dictionary suggestions models. These models are created when you build a dictionary. The dictionary is included in the backup, but the term suggestions model is not. Reprocess the migrated collections to enable dictionary term suggestions.
- You cannot back up and restore curations or migrate them because curations are a beta feature.

You can back up and restore some data by using the backup and restore scripts, but you must back up and restore other data manually. The following data must be backed up manually:

- Local file system folders and documents that you can crawl by using the Local File System data source.

The following updates are made when your collections are restored:

- Any collection that contains documents that were created by uploading data are automatically recrawled and reindexed when restored. These documents are assigned new document ID numbers in the restored collections.
- Collections that were used in *Content Mining* projects are automatically recrawled and reindexed when restored. Only documents that are added by uploading data are assigned new document ID numbers in the restored collections.
- If you enabled the **Content intelligence** feature for *Document Retrieval* projects with a 2.2.1 or a later 2.2.x deployment and want to continue to use the projects in 4.0.0, you must take an extra step after you restore the data. For more information, see [Resetting the project type](#contracts).

## Back up and restore methods
{: #backup-restore-methods}

You can back up and restore your instance of {{site.data.keyword.discoveryshort}} manually or by using scripts. The scripts for 2.2.0 can be used for 2.2.1 and 4.0 also.

- [Using the backup scripts](#wddata-backup)
- [Using the restore scripts](#wddata-restore)
- [Backing up data manually](#backup-user-data)
- [Restoring data manually](#restore-user-data)

You must have Administrative access to the {{site.data.keyword.discoveryshort}} instance on your {{site.data.keyword.discoveryshort}} cluster (where the data must be backed up) and administrative access to the new instance (where the data must be restored to).

## Using the backup scripts
{: #wddata-backup}

Because changes to the data stored in {{site.data.keyword.discoveryfull}} during a backup can cause the backup to become corrupted and unusable, no in-flight requests are allowed during the backup period.

An in-flight request is any {{site.data.keyword.discoveryfull}} action that processes data, including the following actions:

- Source crawl (scheduled or unscheduled)
- Ingesting documents
- Training a trained query model

Complete the following steps to back up {{site.data.keyword.discoveryfull}} data by using the backup scripts:

1.  Enter the following command to set the current namespace where your {{site.data.keyword.discoveryshort}} instance is deployed:

    ```bash
    oc project <namespace>
    ```
    {: pre}

1.  Get the backup script from the [GitHub repository](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/2.2.0){: external}.

    You need all of the files in the repository to complete a backup and restore. Follow the instructions in GitHub Help to clone or download a compressed file of the repository.
    {: important}

1.  Make each script executable by running the following command:

    ```bash
    chmod +x <name-of-script>
    ```
    {: pre}

    where `<name-of-script>` is the name of the script.

1.  Run the `all-backup-restore.sh` script.

    ```bash
    ./all-backup-restore.sh backup [ -f backup_file_name ] [--pvc]
    ```
    {: pre}    

    The `-f backup_file_name` parameter is optional. The name `watson_discovery_<timestamp>.backup` is used if you don't specify a name.

    The `--pvc` parameter is optional. For more information about when to use it, see [Configuring jobs to use PVC](#pvc).

    If you are backing up version 2.1.4, enter the following command:

    ```bash
    ./all-backup-restore.sh backup <release_name> [ -f backup_file_name ] [--pvc]
    ```
    {: pre}

    By default, the backup and restore scripts create a `tmp` directory in the current directory that the script uses for extracting or compressing backup files.

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

In most cases, you don't need to use a persistent volume. If you choose to use a persistent volume, the volume must be three times as large as the largest backup file in the data store. The size of data store's backup file depends on usage. After you create a backup, you can [extract files from the archive file](#backup-unpack) to check the file sizes.

### Mapping multitenant clusters
{: #backup-mapping}

With version 4.0.6 or later, if you are restoring a multitenant cluster, you must perform an extra step. You must create a JSON file that maps the service instance IDs between the backed-up cluster and the cluster where the data is being restored.

This mapping step is not required if the instance IDs did not change between the back up and restore steps. For example, you can skip this step if you are restoring data to the same cluster where it was backed up from or if you are restoring data to a brand new cluster that has no Discovery instances.

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

    Add the instance IDs for the destination service instances that you listed in the previous step. The following snippet is an example mapping file.

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

With version 4.0.6 or later, if you are restoring a multitenant cluster to a multitenant cluster where {{site.data.keyword.discoveryfull}} is running, see [Mapping multitenant clusters](#backup-mapping) before you begin.

Complete the following steps to restore data in {{site.data.keyword.discoveryfull}} by using the restore scripts:

1.  Enter the following command to set the current namespace where your {{site.data.keyword.discoveryshort}} instance is deployed:

    ```bash
    oc project <namespace>
    ```
    {: pre}

1.  If you haven't already, get the restore script from the [GitHub repository](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/2.2.0){: external}.

    You need all of the files in the repository to complete a back up and restore. Follow the instructions in GitHub Help to clone or download a compressed file of the repository.
    {: important}

1.  Make each script executable by running the following command:

    ```bash
    chmod +x <name-of-script>
    ```
    {: pre}

    where `<name-of-script>` is the name of the script.

1.  Restore the data from the backup file on your local machine to the new {{site.data.keyword.discoveryshort}} deployment by running the following command:

    ```bash
    ./all-backup-restore.sh restore -f backup_file_name [--pvc] [--mapping]
    ```
    {: pre}

    The `--pvc` parameter is optional. For more information about when to use it, see [Configuring jobs to use PVC](#backup-pvc).

    The `--mapping` parameter is optional. For more information about when to use it, see [Mapping multitenant clusters](#backup-mapping).

    By default, the backup and restore scripts create a `tmp` directory in the current directory that the script uses for extracting or compressing backup files.

    The gateway, ingestion, orchestrator, hadoop worker, and controller pods automatically restart.

## Backing up data manually
{: #backup-user-data}

Manually back up data that is not backed up by using the scripts.
{: shortdesc}

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

## Restoring data manually
{: #restore-user-data}

Manually restore data that cannot be restored by using the script.
{: shortdesc}

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

    If you are manually restoring data to an instance of {{site.data.keyword.discoveryshort}} version 2.1.2 or earlier, enter `oc get pods|grep ingestion` to find the ingestion pod.
    {: tip}

1.  Enter the following command:

    ```bash
    oc cp <path-to-backup-directory> <crawler pod>:/mnt
    ```
    {: pre}

### Resetting the project type
{: #contracts}

To use the Content intelligence feature in the 2.2.1 release, you enabled the feature in the overrides YAML file and then installed the service. Afterward, every Document Retrieval project that was created was able to understand contract content by default.

With the 4.0.0 release, the way to enable contract understanding changed. Now, you do not need to make any customizations before installing the service. Instead, you can create a Document Retrieval project, and then apply the Contracts enrichment to the project. In addition to simplifying the enablement steps, this change means that you can now create a Document Retrieval project without the Contracts enrichment feature if you don't need it.

As a result of this usability improvement, when you migrate a project with the content intelligence feature to the latest version of the product, you must take an extra step to reset the project type for the project. The old project is recognized as a `document_retrieval` project type. In 4.0.0, a project must have a `content_intelligence` project type to support the Contracts enrichment.

To change the project type that is assigned to a project that requires the Contracts enrichment, complete the following steps.

Changing a project type with the API is only supported in this specific upgrade scenario. Do not change a project type under any other circumstances or your project might become unusable.
{: important}

1.  Get the appropriate URL and project ID information for the project that you want to reset.

    For more information, see [Using the API](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-api-use#api-use-cpd).
1.  Use the [Update a project](https://cloud.ibm.com/apidocs/discovery-data#updateproject){: external} API method to change the type that is associated with your project.

    For example, the following POST request changes the project type of the project with ID `ef5b7eb5-15d4-4a97-b325-a4cb2436966e`:

    ```bash
    curl -X POST -H "Authorization: Bearer {token}" \
    -H "Content-Type: application/json" \
    -d "{ \
	    "type": "content_intelligence" \
    }" \
    "https://mycluster/discovery/wd/instances/1621739945813501/api/v2/projects/ef5b7eb5-15d4-4a97-b325-a4cb2436966e?version=2020-08-30" \
    ```
    {: pre}
