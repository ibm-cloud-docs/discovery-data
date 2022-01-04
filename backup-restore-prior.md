---

copyright:
  years: 2020, 2022
lastupdated: "2021-10-02"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Backing up and restoring data to 2.2.1 or earlier releases
{: #backup-restore-prior}

Use the following procedures to back up and restore data in your {{site.data.keyword.discovery-data_long}} 2.2.0 or earlier instances.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

These procedures are for advanced users who have experience with administering {{site.data.keyword.discovery-data_short}} clusters.  You do not need to back up and restore data as part of standard use or maintenance.
{: important}

For more information about how to migrate your data from earlier versions to the latest version, see [Backing up and restoring data in Cloud Pak for Data](/docs/discovery-data?topic=discovery-data-backup-restore).

Use the information in this topic to migrate your data from and restore it to the following versions:

- 2.2.0 to 2.2.1
- 2.1.4 to 2.2.1
- 2.1.4 to 2.2.0
- 2.1.3 to 2.2.1
- 2.1.3 to 2.1.4
- 2.1.2 to 2.1.4
- 2.1.2 to 2.1.3
- 2.1.1 to 2.1.2
- 2.1.0 to 2.1.2

Backup and restore are supported on all versions of {{site.data.keyword.discoveryshort}}.

## Process overview
{: #overview-prior}

The high-level steps in the process are the following:

1.  Back up your {{site.data.keyword.discoveryshort}} data by using the backup script or manually or both.
1.  Install the latest version of the {{site.data.keyword.icp4dfull_notm}}.
1.  Install the latest version of the {{site.data.keyword.discoveryshort}} service on the cluster.
1.  Restore the backed-up {{site.data.keyword.discoveryshort}} data by using the restore scripts or manually or both.

## Back up and restore limitations
{: #bnr-restrictions-prior}

You can back up and restore some data by using the backup and restore scripts, but you must back up and restore other data manually.

You cannot automatically migrate the following data from version 2.1.2 to later versions, nor can you automatically back up and restore the following data on version 2.1.2 and earlier:

-   User data

    -   [Box files](#migrate-box) that contain your credentials for configuring your Box crawler
    -   Local file system folders and documents that you can crawl by using the Local File System data source. Unlike the other listed data, you cannot back up and restore local file system folders and documents on version 2.1.3 and later, and you cannot migrate them from version 2.1.3 to later versions.
    -   Driver files of JDBC or Salesforce crawlers
-   Dictionary suggestions models. These models are created when you build a dictionary. The dictionary is included in the backup, but the suggestions model is not.
-   Content Miner Document flags
-   You cannot back up and restore curations or migrate them from version 2.1.2 to later versions because curations are a beta feature.

However, other than local file system folders and documents, you can back up and restore the previous data on version 2.1.3 and later, and you can migrate the previous data from 2.1.3 to later versions. You can migrate other data and training data from version 2.1.2 to later versions by using the version 2.1 backup scripts.

To configure your Box, Salesforce, or JDBC crawlers in version 2.1.3 or later, log in to version 2.1.3 or later and update the configuration of your Box, Salesforce, or JDBC crawlers. Alternatively, you can use the backup and restore scripts.

For more information about configuring specific crawlers or for information about migrating your Box, Salesforce, or JDBC crawlers, see the following topics:

- [Configuring {{site.data.keyword.discovery-data_short}} data sources](/docs/discovery-data?topic=discovery-data-collection-types)
- [Migrating Box crawlers](#migrate-box)
- [Migrating Salesforce or JDBC crawlers](#migrate-salesforce-jdbc)

The following updates are made when your collections are restored:

- Any collection that contains documents that were added by uploading data are automatically recrawled and reindexed when restored. These documents are assigned new document ID numbers in the restored collections.
- All collections that are used in a **Content Miner** project are automatically recrawled and reindexed when restored. Only the documents that are added by uploading data are assigned new document ID numbers in the restored collections.

## Back up and restore methods
{: #backup-restore-methods-prior}

You can back up and restore your instance of {{site.data.keyword.discoveryshort}} by using manual or automated methods. The methods of backing up and restoring your instance and migrating your crawlers are as follows:

- [Backing up Watson Discovery by using the backup scripts](/docs/discovery-data?topic=discovery-data-backup-restore#wddata-backup)
- [Restoring Watson Discovery by using the restore scripts](/docs/discovery-data?topic=discovery-data-backup-restore#wddata-restore)
- [Backing up data manually](/docs/discovery-data?topic=discovery-data-backup-restore#backup-user-data)
- [Restoring data manually](/docs/discovery-data?topic=discovery-data-backup-restore#restore-user-data)
- [Migrating Box crawlers](/docs/discovery-data?topic=discovery-data-backup-restore#migrate-box)
- [Migrating Salesforce and JDBC crawlers](/docs/discovery-data?topic=discovery-data-backup-restore#migrate-salesforce-jdbc)

### Backing up Watson Discovery by using the backup scripts
{: #wddata-backup-prior}

Backup prerequisites:

Because changes to the data stored in {{site.data.keyword.discoveryfull}} during a backup can cause the backup to become corrupted and unusable, no in-flight requests are allowed during the backup period.

A request is a current action that is being performed by {{site.data.keyword.discoveryfull}}. Actions that are performed by {{site.data.keyword.discoveryshort}} include:

-   Source crawl (scheduled or unscheduled)
-   Ingesting documents
-   Training a trained query model

Perform the following steps to back up {{site.data.keyword.discoveryfull}} by using the backup scripts:

1.  Ensure that the following services are running on your {{site.data.keyword.discoveryshort}} instance.

    -   `Postgresql`
    -   `Etcd`
    -   `ElasticSearch`
    -   `Hadoop`
    -   `Minio`
    -   `<release_name>-watson-discovery-gateway-0`

1.  Enter the following command to set the current namespace where your {{site.data.keyword.discoveryshort}} instance is deployed:

    ```sh
    kubectl config set-context $(kubectl config current-context) \
    --namespace=<namespace>
    ```
    {: pre}

    You can also set the current namespace by using this `oc` command:

    ```sh
    oc project <namespace>
    ```
    {: pre}

1.  Run the `all-backup-restore.sh` script. The `<-f backupFileName>` part of the following command is optional. You can also specify the namespace in which the gateway pods are deployed:

    ```sh
    ./all-backup-restore.sh backup <-f backupFileName>
    ```
    {: pre}

    If you are backing up version 2.1.4 and earlier, enter `./all-backup-restore.sh backup <release_name> <-f backupFileName>` to specify the release name that you are backing up. Like the command for version 2.2.0, the `<-f backupFileName>` part of the command is optional, and you can specify the namespace in which the gateway pods are deployed.
    {: tip}

The scripts generate an archive file, including the backup files of the services that are listed in Step 1. The file is named `watson_discovery_<timestamp>.backup` or the file that is specified by the `-f` option in the current directory. These scripts create a `tmp` directory in the current directory when they back up and restore documents. You can unpack the archive file by running following command:

```sh
tar xvf <backup_file_name>
```
{: pre}

If you want to install multiple {{site.data.keyword.discoveryshort}} add-ons to different clusters, see [Copying {{site.data.keyword.discoveryshort}} data across {{site.data.keyword.discoveryshort}} clusters](/docs/discovery-data?topic=discovery-data-backup-restore#copy-data-new-clusters).
{: note}

For more information about the backup and restore methods, see [Back up and restore methods](/docs/discovery-data?topic=discovery-data-backup-restore#backup-restore-methods).

### Restoring Watson Discovery by using the restore scripts
{: #wddata-restore-prior}

Perform the following steps to restore data in {{site.data.keyword.discoveryfull}} by using the restore scripts:

1.  Ensure that the following services are running on your {{site.data.keyword.discoveryshort}} instance.

    -   `Postgresql`
    -   `Etcd`
    -   `ElasticSearch`
    -   `Hadoop`
    -   `Minio`
    -   `<release_name>-watson-discovery-gateway-0`

1.  Enter the following command to set the current namespace where your {{site.data.keyword.discoveryshort}} instance is deployed:

    ```sh
    kubectl config set-context $(kubectl config current-context) \
    --namespace=<namespace>
    ```
    {: pre}

    You can also set the current namespace by using this `oc` command:

    ```sh
    oc project <namespace>
    ```
    {: pre}

1.  Restore the data from the backup file on your local machine to the new {{site.data.keyword.discoveryshort}} deployment by running the following command:

    ```sh
    ./all-backup-restore.sh restore -f <backupFileName>
    ```
    {: pre}

    If you are restoring version 2.1.4 and earlier, enter `./all-backup-restore.sh restore <release_name> -f <backupFileName>` to specify the `<release_name>` that you are restoring to and the file name that you want to back up. You can use `core` as the `<release_name>` if you restore to version 2.1.2.
    {: tip}

The `gateway`, `ingestion`, `orchestrator`, `hadoop worker`, and `controller` pods automatically restart.

If you want to install multiple {{site.data.keyword.discoveryshort}} add-ons to different clusters, see [Copying {{site.data.keyword.discoveryshort}} data across {{site.data.keyword.discoveryshort}} clusters](/docs/discovery-data?topic=discovery-data-backup-restore#copy-data-new-clusters).
{: tip}

For more information about the backup and restore methods, see [Backup and restore methods](/docs/discovery-data?topic=discovery-data-backup-restore#backup-restore-methods).

#### Installing the `requests` package manually
{: #requests-manual-prior}

During the restore process, the restore script attempts to install a .pip package, called `requests`, in the container. If your environment has a firewall, the script fails, and the package cannot download. In that case, you can copy the package to your gateway pod and install the package there. This task is only applicable to {{site.data.keyword.discovery-data_short}} version 2.1.2.
{: shortdesc}

To install the `requests` package manually, complete the following steps:

1.  Enter the following command to download the `requests` package on another environment that can install the package by using pip3:

    ```sh
    pip3 download -d <src_directory> --no-binary :all: requests
    ```
    {: pre}

1.  You must copy and install the `requests` package to the first gateway pod that is listed. To list the available gateway pods, enter the following command:

    ```sh
    kubectl get pod -l "release=core,run=gateway"
    ```
    {: pre}

    In a list of multiple gateway pods, note the first one listed. If only one gateway pod is listed, copy the `requests` package to that pod.

1.  Enter the following command to copy the `requests` package to the first listed gateway pod:

    ```sh
    kubectl cp -c nginx <src_directory> <first-listed-gateway-pod>:/tmp/requests_src
    ```
    {: pre}

1.  Enter the following command to install the `requests` package on the gateway pod:

    ```sh
    kubectl exec -c nginx <first-listed-gateway-pod> -- pip3 install --user \
    -q --no-cache-dir /tmp/requests_src/requests-<version>.tar.gz
    ```
    {: pre}

1.  Enter the following command to run the post-restore scripts.

    Entering `-n` is optional. If you do not enter `-n`, the scripts run in the current namespace.
    {: note}

    ```sh
    ./post-restore.sh core [-n <namespace>]
    ```
    {: pre}

    The `requests` package is removed upon restarting the gateway pod, and the `all-backup-restore.sh` script restarts the gateway pod before it runs the `post-restore.sh` script.
    {: note}

### Backing up data manually
{: #backup-user-data-prior}

Because [some data](/docs/discovery-data?topic=discovery-data-backup-restore#bnr-restrictions) is not automatically backed up when you back up an instance of {{site.data.keyword.discoveryshort}}, such as Box files that contain your configuration credentials and Local File System folders and documents, you must manually back up this data.
{: shortdesc}

To manually back up your data from an instance of {{site.data.keyword.discoveryshort}}, complete the following steps:

1.  Enter the following command to log on to your {{site.data.keyword.discoveryshort}} cluster:

    ```sh
    oc login https://<OpenShift administrative console URL> \
    -u <cluster administrator username> -p <password>
    ```
    {: pre}

1.  Enter the following command to switch to the proper namespace:

    ```sh
    oc project <discovery-install namespace>
    ```
    {: pre}

1.  Enter `oc get pods|grep crawler`.

    If you are manually backing up data from an instance of {{site.data.keyword.discoveryshort}} version 2.1.2 or earlier, enter `oc get pods|grep ingestion` to find the ingestion pod.
    {: tip}

1.  Enter the following command:

    ```sh
    kubectl cp <crawler pod>:/mnt <path-to-backup-directory>
    ```
    {: pre}

    Or you can back up your data by using the following `oc` command:

    ```sh
    oc rsync <crawler pod>:/mnt <path-to-backup-directory>
    ```
    {: pre}

    If you are manually backing up data from an instance of {{site.data.keyword.discoveryshort}} version 2.1.2 or earlier, enter `kubectl cp <ingestion-pod>:/mnt <path-to-backup-directory>`.
    {: tip}

For more information about the backup and restore methods, see [Back up and restore methods](/docs/discovery-data?topic=discovery-data-backup-restore#backup-restore-methods).

### Restoring data manually
{: #restore-user-data-prior}

Because [some data](/docs/discovery-data?topic=discovery-data-backup-restore#bnr-restrictions) is not automatically restored after you back up an instance of {{site.data.keyword.discoveryshort}}, such as Box files that contain your configuration credentials and Local File System folders and documents, you must manually restore this data.
{: shortdesc}

To manually restore your data from an instance of {{site.data.keyword.discoveryshort}}, complete the following steps:

1.  Enter the following command to log on to your {{site.data.keyword.discoveryshort}} cluster:

    ```sh
    oc login https://<OpenShift administrative console URL> \
    -u <cluster administrator username> -p <password>
    ```
    {: pre}

1.  Enter the following command to switch to the proper namespace:

    ```sh
    oc project <discovery-install namespace>
    ```
    {: pre}

1.  Enter `oc get pods|grep crawler`.

    If you are manually restoring data to an instance of {{site.data.keyword.discoveryshort}} version 2.1.2 or earlier, enter `oc get pods|grep ingestion` to find the ingestion pod.
    {: tip}

1.  Enter the following command:

    ```sh
    kubectl cp <crawler pod>:/mnt <path-to-backup-directory>
    ```
    {: pre}

    Or you can restore your data by using the following `oc` command:

    ```sh
    oc rsync <path-to-backup-directory> <crawler pod>:/mnt
    ```
    {: pre}

    If you are manually restoring data to an instance of {{site.data.keyword.discoveryshort}} version 2.1.2 or earlier, enter `kubectl cp <path-to-backup-directory> <ingestion pod>:/mnt`.
    {: tip}

For information about the backup and restore methods, see [Back up and restore methods](/docs/discovery-data?topic=discovery-data-backup-restore#backup-restore-methods).

### Migrating Box crawlers
{: #migrate-box}

Complete this task if you are migrating a Box crawler from {{site.data.keyword.discoveryshort}} version 2.1.2 to 2.1.3 or from 2.1.2 to 2.1.4. In the Box data source in {{site.data.keyword.discoveryshort}} version 2.1.3 and 2.1.4, you can upload a JSON file that contains your Box credentials. This JSON file replaces the .pem file from previous versions. If you are upgrading from a version of the Box data source that is earlier than 2.1.3, you can convert your .pem file to a JSON file and upload it to migrate your Box crawler to version 2.1.3.
{: shortdesc}

If you manually back up your data from version 2.1.3 and restore it on 2.1.4, your Box crawler from version 2.1.3 is automatically migrated to 2.1.4. Therefore, you do not need to complete the following task if you want to migrate your Box crawler from version 2.1.3 to 2.1.4.
{: note}

To migrate your Box crawler, complete the following steps:

1.  Back up the user data of an older version of {{site.data.keyword.discoveryshort}} that you are migrating data from. For more information about manually backing up data, see [Backing up data manually](/docs/discovery-data?topic=discovery-data-backup-restore#backup-user-data).
1.  Enter the following command to log on to your {{site.data.keyword.discoveryshort}} cluster, replacing the `<>` and the content within with your OpenShift administrative console URL and login credentials:

    ```sh
    oc login https://<OpenShift administrative console URL> \
    -u <cluster administrator username> -p <password>
    ```
    {: pre}

1.  Enter the following command:

    ```sh
    oc project <namespace>
    ```
    {: pre}

1.  Enter the following command:

    ```sh
    ./migrate-box-credential.sh make-json <json_file_name>
    ```
    {: pre}

    A JSON file is generated that has output that looks like the following example:

    ```json
    {
      "clientId_to_clientSecret": {
        "clientId_1": "",
        "clientId_2": "",
      },
      "keyId_to_passphrase": {
        "keyId_1": "",
        "keyId_2": "",
      }
    }
    ```
    {: codeblock}

1.  Open the file in a text editor, and complete the fields next to `clientId` and `keyId`. In `clientId_to_clientSecret`, enter the value of your `clientSecret` that corresponds to each `clientId`. In `keyId_to_passphrase`, enter the passphrase of the private key that corresponds to each `keyId`. If a passphrase is not set for a specific key, leave the field blank.
1.  Enter the following command to upload the JSON file that contains both the Box configuration data and the .pem files:

    ```sh
    ./migrate-box-credential.sh migrate <json_file_name> \
    <user_data_directory> <backup_file_name>
    ```
    {: pre}

To see the backup, restore, and migration restrictions for all versions of {{site.data.keyword.discoveryshort}}, see [Backing up and restoring data in Cloud Pak for Data](/docs/discovery-data?topic=discovery-data-backup-restore). For more information about the backup and restore methods, see [Back up and restore methods](/docs/discovery-data?topic=discovery-data-backup-restore#backup-restore-methods).

### Migrating Salesforce or JDBC crawlers
{: #migrate-salesforce-jdbc}

Complete this task if you are migrating a Salesforce or JDBC crawler from {{site.data.keyword.discoveryshort}} version 2.1.2 to 2.1.3 or from 2.1.2 to 2.1.4. You can configure your version 2.1.3 Salesforce or JDBC crawlers as they are in older versions by using the backup and restore scripts.
{: shortdesc}

If you back up your user data from version 2.1.3 and restore it on 2.1.4, your Salesforce or JDBC crawlers from version 2.1.3 are automatically migrated to 2.1.4. Therefore, you do not need to complete the following task if you want to migrate your Salesforce or JDBC crawlers from version 2.1.3 to 2.1.4.
{: note}

To migrate your Salesforce or JDBC crawlers, complete the following steps:

1.  Back up the user data of the older version of {{site.data.keyword.discoveryshort}} that you are migrating the data from. For more information about manually backing up data, see [Backing up data manually](/docs/discovery-data?topic=discovery-data-backup-restore#backup-user-data).
1.  Enter the following command to log on to your {{site.data.keyword.discoveryshort}} cluster, replacing the `<>` and the content within with your OpenShift administrative console URL and login credentials:

    ```sh
    oc login https://<OpenShift administrative console URL> \
    -u <cluster administrator username> -p <password>
    ```
    {: pre}

1.  Enter the following command:

    ```sh
    oc project <namespace>
    ```
    {: pre}

1.  Enter the following command:

    ```sh
    ./migrate-crawler-jar.sh <user_data_directory> <backup_file_name>
    ```
    {: pre}

To see the backup, restore, and migration restrictions for all versions of {{site.data.keyword.discoveryshort}}, see [Backing up and restoring data in Cloud Pak for Data](/docs/discovery-data?topic=discovery-data-backup-restore). For information about the backup and restore methods, see [Backup and restore methods](/docs/discovery-data?topic=discovery-data-backup-restore#backup-restore-methods).

## Prerequisites, overview, and scripts for backup and restore by using the scripts
{: #bnr-prereq-prior}

Review the following requirements, process overview, and the list of scripts for guidance on how to successfully back up and restore your instance of {{site.data.keyword.discoveryshort}}.
{: shortdesc}

### Required tools, permissions, and system requirements
{: #toolsperms-prior}

Before backing up or restoring data, ensure that you have the following tool that is installed on your machine:

-   `kubectl` 1.11 or later, which is available at [Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/){: external}.

You must have the following permissions:

-   Administrative access to the {{site.data.keyword.discoveryshort}} instance on your {{site.data.keyword.discoveryshort}} cluster (the data must be backed up) and administrative access to the new instance that the data is being restored to.
-   Permissions to use cluster-wide CLI tools, such as `kubectl`.

You must also have the following system requirement: Red Hat Enterprise Linux 7.5 or later.

### Example syntax
{: #example-syntax-prior}

In the following procedures, angle brackets (`< >`) are used to indicate variables that need to be substituted with values for your local installation, and curly brackets (`{ }`) are used literally in `bash` scripts and commands. This use of curly brackets differs from the standard Watson documentation convention of using curly brackets to indicate substitutions.
{: important}

### Backup scripts
{: #backup-scripts-prior}

Use the `all-backup-restore.sh` backup and restore script to back up and restore to {{site.data.keyword.discoveryshort}} version 2.1.0 or later.

-   Back up and restore scripts for versions 2.2.0 and later. [GitHub repository](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/2.2.0){: external}.
-   Backup and restore scripts for version 2.1.3 and 2.1.4. [GitHub repository](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/2.1.3){: external}.
-   Back up and restore scripts for versions 2.1.0 through 2.1.2. [GitHub repository](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/2.1){: external}.

You need all files that are stored in the applicable GitHub repository to perform a backup and restore. Follow the instructions in GitHub Help to clone or download a compressed file of the repository.
{: important}

To make a script executable, run the following command:

```sh
chmod +x <name-of-script>
```

Where `<name-of-script>` is the name of the script.

## Copying data from Discovery for Cloud Pak for Data across clusters
{: #copy-data-new-clusters-prior}

Copy data only to newly created instances.  Copying data to a cluster already in use might result in data loss.
{: important}

If you are installing multiple {{site.data.keyword.discoveryshort}} add-ons to different clusters, you can copy the data from a {{site.data.keyword.discoveryshort}} instance to a new cluster. To copy data across {{site.data.keyword.discoveryshort}} add-on instances deployed on different clusters, first back up the instance you want to copy the data from, and then restore to your new {{site.data.keyword.discoveryshort}} instance.
