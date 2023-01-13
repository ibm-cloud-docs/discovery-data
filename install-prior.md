---

copyright:
  years: 2019, 2023
lastupdated: "2022-12-29"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Installing earlier releases
{: #install-prior}

Find information related to scaling and upgrading earlier releases of {{site.data.keyword.discovery-data_short}}.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

For full installation instructions, see the following topics:

-   [Installing 4.0.x](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=discovery-installing-watson){: external}
-   [Installing 2.2.0, 2.2.1](https://www.ibm.com/docs/cloud-paks/cp-data/3.5.0?topic=services-watson-discovery){: external}
-   [Installing 2.1.3, 2.1.4](https://www.ibm.com/docs/cloud-paks/cp-data/3.0.1?topic=services-watson-discovery){: external}

## Custom scaling in {{site.data.keyword.discovery-data_short}} 4.0.x
{: #scaling-discovery-40x}

In a multitenant environment, you install the {{site.data.keyword.discoveryshort}} service one time, and up to 10 service instances can be deployed. The computing resources, such as CPU and memory, that are provisioned for the installation are shared by all of the deployed instances. For planning purposes, consider the total size of artifacts, such as collections and enrichments, from across all of the instances, not the size per instance.

To scale a deployment, you must have administrative privileges for the project where the deployment is hosted.

To scale the size of your deployment, complete the following steps:

1.  Edit the YAML file for the persistent volume claim (PVC) where the resource that you want to change is running.

1.  Use the following command to get the PVC name. The name is typically something like `data-wd-ibm-elasticsearch-es-server-client-0`.

    ```bash
    oc get pvc | grep 'elasticsearch-es-server-client'
    ```
    {: codeblock}
    
1.  Use the following command to edit the file:

    ```bash
    oc edit pvc {PVC NAME FROM PREVIOUS STEP}
    ```
    {: codeblock}

1.  Edit the YAML file for the PVC pod. You can change settings such as the number of replicas for the target pods or the replica size.

    In the following example, the storage size for the Elastic search client node is changed from `1 Gi` to `2 Gi`.

    ```yaml
    spec:
      ...
      resources:
        requests:
          storage: 2Gi
    ```
    {: codeblock}

    In this example, the number of replicas of the `API gateway` pod is increased from `1` to `2`:

    ```yaml
    spec:
      api:
        replicas: 2
    ```
    {: codeblock}

    For more information about the YAML files that you can edit, see [YAML files](#scaling-yaml-files).

1.  After you edit the YAML file for the PVC, save and close it. Give the cluster a few minutes to pick up and apply the changes. 

    You can verify that the changes were applied by running the following command:

    ```bash
    oc get pvc {PVC NAME}
    ```
    {: codeblock}
    
1.  To ensure that any new nodes that start will use the latest settings, edit the custom resource for the service. Change the default settings to reflect the new values.
    
    For example, to change the default size for `Elastic search storage` pods, make the following change in the custom resource definition:

    ```yaml
    elasticsearch:
      clientNode:
        persistence:
          size: 2Gi
    ```
    {: codeblock}

    For more information, see [Additional installation options](https://www.ibm.com/docs/en/SSQNUZ_4.0/svc-discovery/discovery-install-overview.html#operator-install__options){: external}. Not all of the resources that are used by the service are listed in the default custom resource. You can add other resources to the CR if adjustments to their defaults are needed.

1.  Run the following command to apply the CR changes:

    ```bash
    oc patch wd wd --patch "$(cat $file_name)" --type='merge'
    ```
    {: codeblock} 

### YAML files
{: #scaling-yaml-files}

Definitions that are specified in YAML files provide instructions to the cluster about how to manage the pods that are used by the service. 

#### `UI` pods
{: #scaling-ui}

```yaml
spec:
  tooling:
    minerapp:
      replicas: {number of replicas}
    tooling:
      replicas: {number of replicas}
```
{: codeblock}

#### `API gateway` pod
{: #scaling-api-gateway}

```yaml
spec:
  api:
    replicas: {number of replicas}
```
{: codeblock}

#### `Elastic search` pods
{: #scaling-elastic}

```yaml
spec:
  elasticsearch:
    clientNode:
      replicas: {number of replicas}
    dataNode:
      replicas: {number of replicas}
    masterNode:
      replicas: {number of replicas}
```
{: codeblock}

#### `Hadoop worker` pod
{: #scaling-hadoop}

```yaml
spec:
  hdp:
    worker:
      replicas: {number of replicas}
```
{: codeblock}

#### `Crawler` pod
{: #scaling-crawler}

```yaml
spec:
  ingestion:
    crawler:
      replicas: {number of replicas}
```
{: codeblock}

#### `Analyze API` pod
{: #scaling-analyze-api}

```yaml
spec:
  statelessapi:
    runtime:
      replicas: {number of replicas}
```
{: codeblock}

#### `Watson Knowledge Studio model enrichment` pod
{: #scaling-wks}

```yaml
spec:
  wksml:
    replicas: {number of replicas}
```
{: codeblock}

## Custom scaling in {{site.data.keyword.discovery-data_short}} 2.2.0
{: #scaling-discovery}

You can perform custom scaling on pods in {{site.data.keyword.discoveryshort}} 2.2.0.

1.  To update the replicas, create a yaml file that specifies the number of replicas for the target pods. For example, to increase the number of replicas of the `API gateway` pod, create the following yaml file:

    ```yaml
    spec:
      api:
        replicas: 2
    ```
    {: codeblock}

1.  Apply the file by using the `oc patch` command:

    ```bash
    oc patch wd wd --patch "$(cat $file_name)" --type='merge'
    ```
    {: codeblock}

For more information about the YAML files that you can edit, see [YAML files](#scaling-yaml-files).

## Upgrading Discovery for Cloud Pak for Data from 2.2.0 to 2.2.1
{: #upgrade-discovery}

To upgrade versions of {{site.data.keyword.discoveryfull}} that are earlier than 2.2.0, you must uninstall the current version and then install the newer version.

{{site.data.keyword.discovery-data_short}} supports an in-place upgrade from version 2.2.0 to 2.2.1 only, so you do not need to uninstall version 2.2.0 and install version 2.2.1. For more information, see the following sections:

- [Preparing to upgrade your Watson Discovery clusters](#prepare-clusters)
- [Upgrading your Watson Discovery instance](#upgrade-instance)
- [Verifying that your upgrade completed successfully](#verify-upgrade).

For the procedures to back up and restore user data in {{site.data.keyword.discovery-data_short}}, see [Backing up and restoring data](/docs/discovery-data?topic=discovery-data-backup-restore).

### Preparing to upgrade your Watson Discovery clusters
{: #prepare-clusters}

Before you upgrade your {{site.data.keyword.discovery-data_short}} 2.2.0 instance, you must prepare your {{site.data.keyword.discovery-data_short}} clusters for the upgrade so that you know if you need to create or update any resources on the clusters. If you do not prepare your clusters, your upgrade will fail.
{: shortdesc}

As you prepare your clusters for the upgrade, you do not need to pause or stop any in-flight operations, such as crawling, ingesting documents, or training a query model. This upgrade performs a rolling update of each component in your instance without any downtime.
{: note}

Complete the following steps to prepare your {{site.data.keyword.discovery-data_short}} clusters that are connected to the internet for the upgrade from version 2.2.0 to 2.2.1:

1.  From your installation node, navigate to the directory where you placed the {{site.data.keyword.icp4dfull}} CLI and the `repo.yaml` file.
1.  Enter the following command to log in to your Red Hat OpenShift cluster as an administrator:

    ```sh
    oc login <OpenShift_URL:port>
    ```
    {: pre}

    where `<OpenShift_URL:port>` is the URL that you use when you log in to your OpenShift cluster.
1. Enter the following command to verify that {{site.data.keyword.discovery-data_short}} 2.2.0 is already installed and is in a `Ready` state:

    ```sh
    ./cpd-cli status -a watson-discovery -n <Project>
    ```
    {: pre}

    in which `<Project>` is the namespace where your {{site.data.keyword.discovery-data_short}} 2.2.0 instance is installed.
1.  Enter the following command to view the list of resources that you must create or update on the cluster:

    ```sh
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

1.  Re-enter the command in step 4, and include the `--apply` flag to create or update the necessary resources on your cluster:

    ```sh
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

1.  From your installation node, navigate to the directory where you placed the {{site.data.keyword.icp4dfull}} CLI and the `repo.yaml` file.
1.  Enter the following command to log in to your Red Hat OpenShift cluster as an administrator:

    ```sh
    oc login <OpenShift_URL:port>
    ```
    {: pre}

    where `<OpenShift_URL:port>` is the URL that you use when you log in to your OpenShift cluster.
1.  Enter the following command to view a summary of changes that take effect after you upgrade the service:

    ```sh
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

1.  Re-enter the command from step 3 without the `--dry-run` flag to upgrade your {{site.data.keyword.discovery-data_short}} instance.

### Verifying that your upgrade completed successfully
{: #verify-upgrade}

1.  From your installation node, enter the following command to obtain the {{site.data.keyword.discovery-data_short}} assembly status:

    ```sh
    ./cpd-cli status \
    --assembly watson-discovery \
    --namespace <Project>
    ```
    {: pre}

    in which `<Project>` is the namespace where your {{site.data.keyword.discovery-data_short}} 2.2.1 instance is installed. If the status is `Not Ready`, it might take several minutes before the assembly status indicates `Ready`. If the status is `Failed`, you can get help by creating a case from [IBM Cloud Support](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.
1.  Enter the following command to verify the `WatsonDiscovery` custom resource status:

    ```sh
    oc get WatsonDiscovery wd
    ```
    {: pre}

    If the value of `Ready` equals `True` and the value of `Updating` equals `False`, the upgrade is complete.
