---

copyright:
  years: 2019
lastupdated: "2019-07-29"

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

# Backing up and restoring data
{: #backup-restore}

Use the following procedures to back up and restore user data in your {{site.data.keyword.discovery-data_long}} instance.
{: shortdesc}

The procedures on this page are for advanced users who have experience administering {{site.data.keyword.discovery-data_short}} clusters. You do not need to back up and restore data, as part of standard use or maintenance.
{: important}

## General prerequisites
{: #gen-prereqs}

### Required tools
{: #tools}

Before backing up or restoring data, ensure that you have the following tools installed on your machine:

  - `kubectl`, which is available as described at [Installing the Kubernetes CLI (kubectl) ![External link icon](../../icons/launch-glyph.svg"External link icon")](<https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_kubectl.html>){: new_window}.

### Required permissions
{: #perms}

You must also have the following permissions:

  - Administrative access to the {{site.data.keyword.discovery-data_short}} instance on your {{site.data.keyword.discovery-data_short}} cluster (these data must be backed up) and administrative access to the new instance that the data are being restored to.
  - Permissions to use cluster-wide CLI tools, such as `kubectl`.

### Example syntax
{: #example-syntax}

In the following procedures, angle brackets (`< >`) are used to indicate variables that need to be substituted with values for your local installation, and curly brackets (`{ }`) are used literally in `bash` scripts and commands. This use of curly brackets differs from the standard Watson documentation convention of using curly brackets to indicate substitutions. 
{: important}

## Process overview
{: #overview}

The backup and restore process can be summarized as follows:

### Backing up

  1. Back up IBM Cloud Pak for Data, if required. See [Backup and restore](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/backup_restore.html) for more information.
  1. Ensure that the {{site.data.keyword.discovery-data_short}} instance being backed up does not have any incoming requests and that there are no outstanding in-flight requests.
     **Note:** For the purposes of the procedures described in this topic, a request is a current action being perfomed by Watson Discovery. Actions perfomed by Watson Discovery include:
     -  Performing a source crawl (scheduled or unscheduled)
     -  Ingesting documents
     -  Training a trained query model
  1. Copy the data from the data service to the matching service on the new pod.
  1. Clean or groom the data, as necessary.

### Restoring

  1. Use the generated backup to restore a {{site.data.keyword.discovery-data_short}} application to an existing and/or new {{site.data.keyword.discovery-data_short}} installation.
  1. Copy the data from the new pod to the data service.
  1. Enable requests on the new {{site.data.keyword.discovery-data_short}} instance.

## Backup prerequisites
{: #backup-prereqs}

Changes to the data stored in Watson Discovery during a backup can cause the backup to become corrupt and unusable (for example, adding documents to a collection). Before initiating a backup, observe the following requirements:

  - Ensure there are no incoming requests to the instance.
  - Ensure that any in-flight requests to the instance have been handled.
  - Ensure the ingestion queues are empty.
    {: important}

There is no precise order in which you need to back up or restore the data services, provided no in-flight requests are permitted during the backup period. However, as read-only operations, queries are permitted during the backup period.
{: note}

Download and make executable the following backup and restore scripts:

- <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery-data/elastic-backup-restore.sh" download>elastic-backup-restore.sh <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
- <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery-data/hdp-backup-restore.sh" download>hdp-backup-restore.sh <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
- <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery-data/wddata-backup-restore.sh" download>wddata-backup-restore.sh <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
- <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery-data/etcd-backup-restore.sh" download>etcd-backup-restore.sh <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
- <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery-data/postgresql-backup-restore.sh" download>postgresql-backup-restore.sh <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>
- <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery-data/all-backup-restore.sh" download>all-backup-restore.sh <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>

Here is a direct link to the directory containing these scripts: (https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data)

To make a script executable, run the following command (for each script downloaded):

```bash
  chmod +x <script-name>
```

Where `<script-name>` is the name of the script.

## Backing up Watson Discovery
{: wddata-backup}

Perform the following steps to completely back up Watson Discovery:

  1. Ensure that the following services are running on your {{site.data.keyword.discovery-data_short}} instance.
    -  `Postgresql`
    -  `Etcd`
    -  `ElasticSearch`
    -  `Hadoop`
    -  `<release_name>-watson-discovery-gateway-0`
  1. Run the `all-backup-restore.sh` script, and specify the release name you are backing up. You can also specify the file name of backup and the namespace in which the gateway pods are deployed, if necessary:

      ```bash
      ./all-backup-restore.sh backup <release_name> [-f backupFileName] [-n namespace]
      ```

      The scripts generate an archive file, including the backup files of above services. The file is named `watson_discovery_<timestamp>.backup` or the file specified by `-f` option in the current directory. These scripts create a`tmp` directory in the current directory, while backing up and restoring. You can unpack the archive file by running following command:

      ```bash
      tar xvf <backup_file_name>
      ```

  You can also back up individual services using the following procedures. These services are backed up when using the `all-backup-restore.sh` script and do not need to be individually backed up if it is used.
  {: note}

### Backing up the Postgresql service
{: #postgres-backup}

  1. Ensure that `Postgresql` is running on your {{site.data.keyword.discovery-data_short}} instance.
  1. Run the `postgresql-backup-restore.sh` script, and specify the release name you are backing up. You can also specify the file name of backup and the namespace in which Postgresql is deployed, if necessary:
      ```bash
      ./postgresql-backup-restore.sh backup <release_name> [-f backupFileName] [-n namespace]
      ```

  The script generates a `pg_<timestamp>.dump` file or the file specified `-f` option in the current directory. The backup file contains the abbreviated output from the Postgresql `pg_dump` command.

### Backing up the ElasticSearch service
{: #es-backup}

  1. Ensure that `ElasticSearch` is running on your {{site.data.keyword.discovery-data_short}} instance.
  1. Run the `elastic-backup-restore.sh` script, and specify the release name you are backing up. You can also specify the file name of backup and the namespace in which ElasticSearch is deployed, if necessary:
      ```bash
      ./elastic-backup-restore.sh backup <release_name> [-f backupFileName] [-n namespace]
      ```
  The script generates a `elastic_<timestamp>.snapshot` file or the file specified `-f` option in the current directory. The backup file contains the snapshot files from the ElasticSearch `snapshot` function.

### Backing up the Etcd service
{: #etcd-backup}

  1. Ensure that `Etcd` is running on your {{site.data.keyword.discovery-data_short}} instance.
  1. Run the `etcd-backup-restore.sh` script, and specify the release name you are backing up. You can also specify the file name of backup and the namespace in which Etcd is deployed, if necessary:
      ```bash
      ./etcd-backup-restore.sh backup <release_name> [-f backupFileName] [-n namespace]
      ```

  The script prints all of the keys and values contained in `etcd` to a text file named `etcd_<timestamp>.db` or the file specified by `-f` option in the current directory. 

### Backing up the Hadoop service
{: hdp-backup}

  1. Ensure that `Hadoop` is running on your {{site.data.keyword.discovery-data_short}} instance.
  1. Run the `hdp-backup-restore.sh` script, and specify the release name you are backing up. You can also specify the file name of backup and the namespace in which Hadoop is deployed, if necessary:
      ```bash
      ./hdp-backup-restore.sh backup <release_name> [-f backupFileName] [-n namespace]
      ```

     The script backs up all files in `HDFS` to a file named `hdp_<timestamp>.backup` or the file specified by `-f` option in the current directory. 


### Backing up the Backend service
{: wddata-backup}

  1. Ensure that `<release_name>-watson-discovery-gateway-0` is running on your {{site.data.keyword.discovery-data_short}} instance.
  1. Run the `wddata-backup-restore.sh` script, and specify the release name you are backing up. You can also specify the file name of backup and the namespace in which the gateway pods are deployed, if necessary:
      ```bash
      ./wddata-backup-restore.sh backup <release_name> [-f backupFileName] [-n namespace]
      ```

     The script generates a `wddata_<timestamp>.backup` file or the file specified by `-f` option in the current directory, including the files for the configuration of crawler and logging, the credential files; and `jar` files, such as JDBC connecter for the crawler.

## Restoring Watson Discovery
{: wddata-restore}

Perform the following steps to completely restore Watson Discovery:

  1. Ensure that the following services are running on your {{site.data.keyword.discovery-data_short}} instance.
    -  `Postgresql`
    -  `Etcd`
    -  `ElasticSearch`
    -  `Hadoop`
    -  `<release_name>-watson-discovery-gateway-0`
  1. To ensure that no services/clients connect to the Postgresql service while restoring, change the target port of the Postgresql service by running following command:
      ```bash
      kubectl edit svc <release_name>-watson-discovery-postgresql
      ```
    
      After running the command, change the `targetPort` from `5432` to `5433`, as shown in the following, and save your change:
      ```
      apiVersion: v1
      kind: Service
      metadata:
      ......
      spec:
        clusterIP: xx.xx.xx.xx
        ports:
        - name: pgport
          port: 5432
          protocol: TCP
          targetPort: 5433
        selector:
          app: watson-discovery
      ......
      ```

  1. Restore the data from the backup file on your local machine to the new {{site.data.keyword.discovery-data_short}} deployment by running the following command. Then, specify the release name you are restoring to and the file name of backup. You can also specify the namespace in which the {{site.data.keyword.discovery-data_short}} service is deployed, if necessary:
      ```
      ./all-backup-restore.sh restore <release_name> -f <backup_file> [-n namespace]
      ```

  The gateway, ingestion, orchestrator, master pods automatically restart.
  1. Restore the `targetPort` of the Postgresql service from `5433` to `5432`.

You can also restore individual services using the following procedures. These services are restored when using the `all-backup-restore.sh` script and, if you use it, do not need to be individually restored.
{: note}

### Restoring the Postgresql service
{: #restore-postgres}

  1. Ensure that `Postgresql` is running on your {{site.data.keyword.discovery-data_short}} instance.
  1. To ensure that no services/clients connect to the Postgresql service while restoring, change the target port of the Postgresql service by running following command:
      ```bash
      kubectl edit svc <release_name>-watson-discovery-postgresql
      ```
    
      After running the command, change the `targetPort` from `5432` to `5433`, as shown in the following, and save the change:
      ```
      apiVersion: v1
      kind: Service
      metadata:
      ......
      spec:
        clusterIP: xx.xx.xx.xx
        ports:
        - name: pgport
          port: 5432
          protocol: TCP
          targetPort: 5433
        selector:
          app: watson-discovery
      ......
      ```

  1. Run the following command to restore the data to the new Postgresql deployment. Then, specify the release name you are restoring to and the file name of backup. You can also specify the namespace in which Postgresql is deployed, if necessary:
      ```bash
      ./postgresql-backup-restore.sh restore <release_name> -f <backup_file> [-n namespace]
      ```

  1. Restore the `targetPort` of the Postgresql service from `5433` to `5432`.


### Restoring the ElasticSearch service
{: #es-restore}

  1. Ensure that `ElasticSearch` is running on your {{site.data.keyword.discovery-data_short}} instance.
  1. Restore the data from the snapshot file on your local machine to the new ElasticSearch deployment by running the following command. Then, specify the release name you are restoring to and the file name of backup. You can also specify the namespace in which ElasticSearch is deployed, if necessary:
     ```
     ./elastic-backup-restore.sh restore -f backup_file_name [-n namespace]
     ```


### Restoring the Etcd service
{: etcd-restore}

  1. Ensure that `Etcd` is running on your {{site.data.keyword.discovery-data_short}} instance.
  1. Restore the data from the text file on your local machine to the new Etcd deployment by running the following command. Then, specify the release name you are restoring to and the file name of backup. You can also specify the namespace in which Etcd is deployed, if necessary:
      ```
      ./etcd-backup-restore.sh restore <release_name> -f <backup_file> [-n namespace]
      ```


### Restoring the Hadoop service
{: etcd-restore}

  1. Ensure that `Hadoop` is running on your {{site.data.keyword.discovery-data_short}} instance.
  1. Restore the data from the backup file on your local machine to the new Hadoop deployment by running the following command. Then, specify the release name you are restoring to and the file name of backup. You can also specify the namespace in which Hadoop is deployed, if necessary:
      ```
      ./hdp-backup-restore.sh restore <release_name> -f <backup_file> [-n namespace]
      ```


### Restoring the Backend service
{: wddata-restore}

  1. Ensure that `<release_name>-watson-discovery-gateway-0` is running on your {{site.data.keyword.discovery-data_short}} instance.
  1. Restore the data from the backup file on your local machine to the new {{site.data.keyword.discovery-data_short}} deployment by running the following command. Then, specify the release name you are restoring to and the file name of backup. You can also specify the namespace in which the `<release_name>-watson-discovery-gateway-0` is deployed, if necessary:
      ```
      ./wddata-backup-restore.sh restore <release_name> -f <backup_file> [-n namespace]
      ```
