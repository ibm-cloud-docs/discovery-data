---

copyright:
  years: 2019
lastupdated: "2019-07-01"

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

# Managing the cluster
{: #manage}

After you install and configure {{site.data.keyword.discovery-data_long}}, you can manage the instance and the cluster.

## Preparing your local machine
{: #manage-prep-local-machine}

Ensure that you have the following prerequisites installed and working correctly on your local machine before performing any cluster-management tasks.

1. Install the `cloudctl`, `helm`, and `kubectl` command-line tools as described at [Software requirements](/docs/services/compare-comply-data?topic=compare-comply-data-install#prereqs).

1.  Start `helm`:
  
    ```bash
    helm init --client-only
    ```
    {: pre}

1.  Verify that the tools are installed correctly by running the following test commands.

    - Test the IBM Cloud Private CLI (`cloudctl`):

      ```bash
      cloudctl login -a https://{hostname}:8443 -u {admin_user_id} -p {admin_password}
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

After you provision an instance, you can share the URL for the service with other users. However, those users can  log in to the service only if you give them access.

If you plan to use SAML for single sign-on (SSO), complete [Configuring single sign-on](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso) before you add users. If you add users before you configure SSO, you need to re-add the users with their SAML IDs to enable them to use SSO.

1.  From the web client menu, click **Administer > Manage user**.

1.  Click **Add user**, then specify the user's full name, user name, and email address. Set the user's permissions, and then click **Add**.

1.  From the web client menu, select **My Instances**.

1.  Find your Compare and Comply instance, click the more (**...**) menu, and then choose **Manage Access**.

1.  Click **Add user**.

1.  Click the user name field to see a list of the people you can add.

    The users you added in the previous steps are listed. Select a name, choose **User** or **Admin** as their access role, and then click **Add**. 

    If you are not connected to an existing user registry and have not enabled single sign-on, then temporary passwords are created for the users you add. The temporary passwords are sent to users by way of the email addresses you specified.