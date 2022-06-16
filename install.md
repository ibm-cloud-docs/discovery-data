---

copyright:
  years: 2019, 2022
lastupdated: "2022-06-16"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Installing 4.0.9
{: #install}

Find information about how to install and manage IBM Watson Discovery Cartridge for IBM Cloud Pak for Data 4.0.9.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

You install {{site.data.keyword.icp4dfull}}, and then install the {{site.data.keyword.discoveryshort}} service.

## Full installation instructions
{: #full-installation-instructions}

[Installing {{site.data.keyword.discoveryfull}} on {{site.data.keyword.icp4dfull}}](https://www.ibm.com/docs/cloud-paks/cp-data/4.0?topic=discovery-installing-watson){: external}

Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.discovery-data_short}} offerings purchased on or after August 30, 2019. {{site.data.keyword.discoveryfull}} is FISMA High Ready.

## Administering an installed deployment
{: #admin-data}

In a multitenant environment, you install the {{site.data.keyword.discoveryshort}} service one time, and up to 10 service instances can be deployed. The computing resources, such as CPU and memory, that are provisioned for the installation are shared by all of the deployed instances. 

For planning purposes, consider the total size of artifacts, such as collections and enrichments, from across all of the instances, not the size per instance.

## Scaling the service
{: #scale-task}

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

    In this example, the number of replicas of the API gateway pod is increased from `1` to `2`:

    ```yaml
    spec:
      api:
        replicas: 2
    ```
    {: codeblock}

    For more information about the YAML files that you can edit, see [YAML files](#scale-yaml-files).

1.  After you edit the YAML file for the PVC, save and close it. Give the cluster a few minutes to pick up and apply the changes. 

    You can verify that the changes were applied by running the following command:

    ```bash
    oc get pvc {PVC NAME}
    ```
    {: codeblock}
    
1.  To ensure that any new nodes that start will use the latest settings, edit the custom resource for the service. Change the default settings to reflect the new values.
    
    For example, to change the default size for Elastic search storage pods, make the following change in the custom resource definition:

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
{: #scale-yaml-files}

Definitions that are specified in YAML files provide instructions to the cluster about how to manage the pods that are used by the service. 

#### UI pods
{: #scale-ui}

```yaml
spec:
  tooling:
    minerapp:
      replicas: {number of replicas}
    tooling:
      replicas: {number of replicas}
```
{: codeblock}

#### API gateway pod
{: #scale-api-gateway}

```yaml
spec:
  api:
    replicas: {number of replicas}
```
{: codeblock}

#### Elastic search pods
{: #scale-elastic}

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

#### Hadoop worker pod
{: #scale-hadoop}

```yaml
spec:
  hdp:
    worker:
      replicas: {number of replicas}
```
{: codeblock}

#### Crawler pod
{: #scale-crawler}

```yaml
spec:
  ingestion:
    crawler:
      replicas: {number of replicas}
```
{: codeblock}

#### Analyze API pod
{: #scale-analyze-api}

```yaml
spec:
  statelessapi:
    runtime:
      replicas: {number of replicas}
```
{: codeblock}

#### Watson Knowledge Studio model enrichment pod
{: #scale-wks}

```yaml
spec:
  wksml:
    replicas: {number of replicas}
```
{: codeblock}
