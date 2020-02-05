---

copyright:
  years: 2019, 2020
lastupdated: "2020-01-17"

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

# Managing the cluster
{: #manage}

After you install and configure {{site.data.keyword.discovery-data_long}}, you can manage the instance and the cluster.

## Preparing your local machine
{: #manage-prep-local-machine}

Ensure that you have the following prerequisites installed and working correctly on your local machine before performing any cluster-management tasks.

1. Install the `cloudctl`, `helm`, and `kubectl` command-line tools as described at [Software requirements](/docs/discovery-data?topic=discovery-data-install#prereqs).

1.  Start `helm`:
  
    ```bash
    helm init --client-only
    ```
    {: pre}

1.  Verify that the tools are installed correctly by running the following test commands.

    - Test the OpenShift CLI (`oc`):

      ```bash
      oc login https://{hostname}:8443
      ```
      {: pre}
    
      If you are using a load balancer, specify the hostname of the load balancer instead of the hostname of the master node.
      {: note}

    - Test Kubernetes (`kubectl`):

      ```bash
      kubectl get namespaces
      ```
      {: pre}

      If you cannot run the `kubectl` command, see [Enabling access to the Kubernetes command-line interface](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}.
      {: note}

    - Test Helm (`helm`):

      ```bash
      helm version --tls
      ```
      {: pre}

## Performing management tasks
{: perform-mgmt-tasks}

The following are some of the tasks you can perform to monitor and maintain your {{site.data.keyword.discovery-data_short}} instance.

  - Identify the cluster nodes to which the product is deployed:
    ```bash
    kubectl get pods -o wide | grep -v Completed
    ```
    {: pre}

  - List the number of replicas of each microservice in a given `{namespace}`:
    ```bash
    kubectl get deploy -n {namespace}
    ```
    {: pre}
    or
    ```bash
    kubectl get statefulset -n {namespace}
    ```
    {: pre}

  - Change (increase or decrease) the number of replicas:
    ```bash
    kubectl scale deploy {pod_name} --replicas={number}
    ```
    {: pre}
    or
    ```bash
    kubectl scale statefulsets {set_name} --replicas={number}
    ```
    {: pre}

  - View logs

    By default, {{site.data.keyword.icp4dfull_notm}} automatically logs information from each service. For more information, see [Viewing logs](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external}.

## Managing user access
{: #manage-user-access}

After you provision an instance, you can share the URL for the service with other users. However, those users can log in to the service only if you give them access.

If you plan to use SAML for single sign-on (SSO), complete [Configuring single sign-on](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso) before you add users. If you add users before you configure SSO, you need to re-add the users with their SAML IDs to enable them to use SSO.

1.  From the web client menu, click **Administer > Manage user**.

1.  Click **Add user**, then specify the user's full name, user name, and email address. Set the user's permissions, and then click **Add**.

1.  From the web client menu, select **My Instances**.

1.  Find your {{site.data.keyword.discovery-data_short}} instance, click the more (**...**) menu, and then choose **Manage Access**.

1.  Click **Add user**.

1.  Click the user name field to see a list of the people you can add.

    The users you added in the previous steps are listed. Select a name, choose **User** or **Admin** as their access role, and then click **Add**. 

    If you are not connected to an existing user registry and have not enabled single sign-on, then temporary passwords are created for the users you add. The temporary passwords are sent to users by way of the email addresses you specified.

## Scaling
{: #scaling}

You can improve ingestion and indexing throughput as well as queries per second by increasing the number of replicas of certain system resources.

Scaling should be used in conjunction with a data architecture that leverages multiple collections in order to fully realize its benefits.

The following table describes the stateful set details.

| Component | Resource | Type | Effect of scaling |
| ----------- | --------- | ------ | ---------------- |
| Ingestion  | {release-name}-watson-discovery-ingestion | StatefulSet  | Increase number of collections that can be ingested to concurrently|
| Indexing | {release-name}-watson-discovery-elastic | StatefulSet | Increase indexing throughput, queries per second supported, and maximum number of indexable documents |
| Enrichment and SDU | {release-name}-watson-discovery-hdp-worker | StatefulSet | Increase enrichment and SDU page processing throughput  |
| SDU | {release-name}-watson-discovery-sdu-api | Deployment | Increase SDU OCR and document reconstruction throughput |

You can scale Resources of type `StatefulSet` by executing the following command:

```bash
kubectl scale statefulset <resource> --replicas=<number>
```
{: pre}

You can scale Resources of type `Deployment` by executing the following command:

```bash
kubectl scale deployment.v1.apps/<resource> --replicas=<number>
```
{: pre}

Increasing the capacity of Elastic can increase the overall performance. Others will increase the number of collections concurrently updated.

### Scaling Etcd clusters
{: #scalingetcd}

`Etcd` clusters are scaled up or down manually using backup and restoration scripts. 

Multi-node `Etcd` clusters must be configured during deployment. Scaling the `Etcd` cluster up or down after deployment is not recommended.
{: important}

1.  Backup the `Etcd` cluster.
    
    ```bash
    etcd-backup-restore.sh backup <release_name>
    ```
    {: pre}
    
1.  Scale the `Etcd` pod to 0.
    
    ```bash
    kubectl scale statefulset <release_name>-watson-discovery-etcd --replicas=0
    ```
    {: pre}

1.  Delete the PVC and PV of `Etcd`. List the {{site.data.keyword.discovery-data_short}} PVC:
    
    ```bash
    kubectl get pvc -l release=<release-name>
    ```
    {: pre}

    Delete the PVC for `Etcd`.

    ```bash
    kubectl delete pvc <pvc_name>
    ```
    {: pre}

    List the PV:
    
    ```bash
    kubectl get pv | grep <release_name>
    ```
    {: pre}

    Delete the PV for `Etcd`.
    
    ```bash
    kubectl delete pv <pv_name>
    ```
    {: pre}

1. Edit the StatefulSet. Please find and edit the following lines by running 
  
    ```bash
    kubectl edit sts <release_name>-watson-discovery-etcd`
    ```
    {: pre}

    This example scales the cluster to 3 nodes.

    - Edit the replica number.
    
      ```
      spec:
      podManagementPolicy: Parallel
      replicas: 3 [Set the replica number here. The replica count should always be an odd number, and never exceed 7 (ideally 5)]
      revisionHistoryLimit: 10
      ```
      {: pre}

    - Edit the endpoints for the `etcdctl` command and the peer endpoints.
    
      ```bash
      [Create the data dir if not exists]
      if [ ! -d '${DATA_DIR}' ]; then
      echo "==> Creating data dir..."
      mkdir -p ${DATA_DIR}
      fi
      export ETCDCTL_ENDPOINTS="https://<release-name>-watson-discovery-etcd-0.<release-name>-watson-discovery-etcd-svc-headless:2379,https://<release-name>-watson-discovery-etcd-1.<release-name>-watson-discovery-etcd-svc-headless:2379,https://<release-name>-watson-discovery-etcd-2.<release-name>-watson-discovery-etcd-svc-headless:2379," 
      [Add the URL of endpoints here. Replace <release_name> with your environment. The last character should be ','.]
      export ETCD_PEER_ENDPOINTS="http://<release-name>-watson-discovery-etcd-0.<release-name>-watson-discovery-etcd-svc-headless:2380,http://<release-name>-watson-discovery-etcd-1.<release-name>-watson-discovery-etcd-svc-headless:2380,http://<release-name>-watson-discovery-etcd-2.<release-name>-watson-discovery-etcd-svc-headless:2380," 
      [Edit this line the same as above. Set the port number carefully.]
      ETCDCTL_ENDPOINTS=${ETCDCTL_ENDPOINTS%","}
      ETCD_PEER_ENDPOINTS=${ETCD_PEER_ENDPOINTS%","}
      ```
      {: pre}

    - Edit the replica number in the `if` statement.
    
      ```bash
      [Adding a new member to the cluster]
      elif [ "${ID}" -ge 3 ]; then [Put the number of replica after '-ge']
      echo "==> Adding member to existing cluster."
      ```
      {: pre}

    - Edit the environment variables ETCD_INITIAL_CLUSTER and ETCD_INITIAL_CLUSTER_TOKEN.
    
      ```bash
      name: ETCD_INITIAL_CLUSTER_TOKEN
      value: ibm-wd-etcd-cluster-zen-wd
        
      name: ETCD_INITIAL_CLUSTER
      value: zen-wd-watson-discovery-etcd-0=http://zen-wd-watson-discovery-etcd-0.zen-wd-watson-discovery-etcd-svc-headless:2380,zen-wd-watson-discovery-etcd-1=http://zen-wd-watson-discovery-etcd-1.zen-wd-watson-discovery-etcd-svc-headless:2380,zen-wd-watson-discovery-etcd-2=http://zen-wd-watson-discovery-etcd-2.zen-wd-watson-discovery-etcd-svc-headless:2380, 
      [Edit this line the same as step ⅱ.]
      image: mycluster.icp:8500/zen/ibm-wex-ee:12.0.3.1055
      ```
      {: pre}

    - Restore the data to the `Etcd` cluster. After all `Etcd` nodes have started, run:
    
      ```bash
      etcd-backup-restore.sh restore <release_name> -f <backup_file>
      ```
      {: pre}

    - Restart the `Gateway`, `Ingestion`, `Orchestrator`, and `Ranker` Master pods. List them by running:
    
      ```bash
      kubectl get pod -l release=zen-wd | grep -e gateway -e ingestion -e orchestrator -e ranker-master
      ```
      {: pre}

    - Then delete these pods.
    
      ```bash
      kubectl delete pod <pod_name>...
      ```
      {: pre}

      The pods will restart automatically.

