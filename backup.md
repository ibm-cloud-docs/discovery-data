---

copyright:
  years: 2020
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

# Backing up and restoring data
{: #backup-restore}

Use the following procedures to back up and restore user data in your {{site.data.keyword.discovery-data_long}} instance.
{: shortdesc}

These procedures are for advanced users who have experience administering {{site.data.keyword.discovery-data_short}} clusters. You do not need to back up and restore data as part of standard use or maintenance.
{: important}

The following data is not part of a backup and is therefore not present when restoring data:

  - Training data (see the [Known issue](/docs/services/discovery-data?topic=discovery-data-known-issues#24jan2020ki) about the backup and restore of training data.)
  - Curations (beta feature available only in the API)
  - Dictionary suggestions models. These are created when you build a dictionary using the tooling. The dictionary will be included in the backup, but the suggestions model will not.
  - Content Miner Document flags 

The following updates are made when your collections are restored:

  - Any collection that contains documents that were added by upload (the`Upload data` option in the tooling) are automatically recrawled and reindexed when restored. These documents will have new document id numbers in the restored collections.
  - All collections used in a **Content Miner** project are automatically recrawled and reindexed when restored. Only the documents added by upload (the`Upload data` option in the tooling) will have new document id numbers in the restored collections.

## Required tools and permissions
{: #toolsperms}

Before backing up or restoring data, ensure that you have the following tool installed on your machine:

  - `kubectl`, which is available at [Installing the Kubernetes CLI (kubectl)](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_kubectl.html){: external}.

You must also have the following permissions:

  - Administrative access to the {{site.data.keyword.discovery-data_short}} instance on your {{site.data.keyword.discovery-data_short}} cluster (the data must be backed up) and administrative access to the new instance that the data are being restored to.
  - Permissions to use cluster-wide CLI tools, such as `kubectl`.

## Process overview
{: #overview}

Summary of the backup process:

  1. Back up IBM Cloud Pak for Data, if required. For more information, see [Backup and restore](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/backup_restore.html){: external}.
  1. Ensure that the {{site.data.keyword.discovery-data_short}} instance being backed up meets the prerequisites listed in [Backing up {{site.data.keyword.discovery-data_long}}](/docs/services/discovery-data?topic=discovery-data-backup-restore#wddata-backup).
  1. Copy the data from the data service to the matching service on the new pod.
  1. Clean or groom the data, as necessary.

Summary of the restore process:

  1. Use the generated backup to restore a {{site.data.keyword.discovery-data_short}} application to an existing and/or new {{site.data.keyword.discovery-data_short}} installation.
  1. Copy the data from the new pod to the data service.
  1. Enable requests on the new {{site.data.keyword.discovery-data_short}} instance.

## Example syntax
{: #example-syntax}

In the following procedures, angle brackets (`< >`) are used to indicate variables that need to be substituted with values for your local installation, and curly brackets (`{ }`) are used literally in `bash` scripts and commands. This use of curly brackets differs from the standard Watson documentation convention of using curly brackets to indicate substitutions. 
{: important}

## Backup scripts
{: #backup-scripts}

There are two versions of the `all-backup-restore.sh` backup and restore scripts. One set is for {{site.data.keyword.discovery-data_short}} versions 2.0.0 and 2.0.1; the other is for versions 2.1.0 and later. **If you are backing up a 2.0 version of {{site.data.keyword.discovery-data_short}}, and then restoring to version 2.1.0 or later -- backup with the 2.0 scripts and restore with the 2.1 scripts.** 
{: important}

 -  Backup/restore scripts for versions 2.1.0 and later. [GitHub repository](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/2.1){: external}.
 -  Backup/restore scripts for 2.0.0 and 2.0.1: [GitHub repository](https://github.com/watson-developer-cloud/doc-tutorial-downloads/tree/master/discovery-data/2.0){: external}.

You will need all files stored in the applicable GitHub repository to perform a backup and restore. Follow the instructions in GitHub Help to clone or download a zip file of the repository.
{: important}

To make a script executable, run the following command:

```bash
  chmod +x <script-name>
```

Where `<script-name>` is the name of the script.

## Backing up Watson Discovery
{: #wddata-backup}

Back up prerequisites:

Since changes to the data stored in {{site.data.keyword.discovery-data_long}} during a backup can cause the backup to become corrupt and unusable, no in-flight requests are permitted during the back up period. 

A request is a current action being performed by {{site.data.keyword.discovery-data_long}}. Actions performed by {{site.data.keyword.discovery-data_short}} include:
  -  Performing a source crawl (scheduled or unscheduled)
  -  Ingesting documents
  -  Training a trained query model 

Queries are read-only operations, so they are permitted during the back up period.
{: tip} 

Perform the following steps to back up {{site.data.keyword.discovery-data_long}}:

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

If you want to install multiple {{site.data.keyword.discovery-data_short}} add-ons to different clusters, see [Copying {{site.data.keyword.discovery-data_short}} data across {{site.data.keyword.discovery-data_short}} clusters](/docs/discovery-data?topic=discovery-data-backup-restore#copy-data-new-clusters).
{: note}

## Restoring Watson Discovery
{: #wddata-restore}

Perform the following steps to restore data in {{site.data.keyword.discovery-data_long}}:

  1. Ensure that the following services are running on your {{site.data.keyword.discovery-data_short}} instance.
    -  `Postgresql`
    -  `Etcd`
    -  `ElasticSearch`
    -  `Hadoop`
    -  `<release_name>-watson-discovery-gateway-0`
  
  1. Restore the data from the backup file on your local machine to the new {{site.data.keyword.discovery-data_short}} deployment by running the following command. Then, specify the `<release_name>` (you can use `core` as the `<release_name>` when restoring to version 2.1.2) you are restoring to and the file name of backup. You can also specify the namespace in which the {{site.data.keyword.discovery-data_short}} service is deployed, if necessary:
      ```
      ./all-backup-restore.sh restore <release_name> -f <backup_file> [-n namespace]
      ```

  The gateway, ingestion, orchestrator, hadoop worker, and master pods automatically restart.
  
If you want to install multiple {{site.data.keyword.discovery-data_short}} add-ons to different clusters, see [Copying {{site.data.keyword.discovery-data_short}} data across {{site.data.keyword.discovery-data_short}} clusters](/docs/discovery-data?topic=discovery-data-backup-restore#copy-data-new-clusters).
{: tip}

## Copying Discovery for Cloud Pak for Data data across Discovery for Cloud Pak for Data clusters
{: #copy-data-new-clusters}

It is recommended that you only copy data to newly created instances, as copying data to a cluster already in use might result in data loss.
{: important}

If you are installing multiple {{site.data.keyword.discovery-data_short}} add-ons to different clusters, you can copy the data from a {{site.data.keyword.discovery-data_short}} instance to a new cluster. To copy data across {{site.data.keyword.discovery-data_short}} add-on instances deployed on different clusters, first backup the instance you want to copy the data from, and then restore to your new {{site.data.keyword.discovery-data_short}} instance.
