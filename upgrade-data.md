---

copyright:
  years: 2015, 2022
lastupdated: "2022-04-01"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Upgrading the service
{: #upgrade-data}

Learn how to upgrade the version of your installed service deployment.
{: shortdesc}

![{{site.data.keyword.icp4dfull_notm}} only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

## Upgrade your deployment
{: #upgrade-data-overview}

In-place upgrade support was added with the 4.0.2 release. For information about how to upgrade from one 4.x release to a later one, see [Upgrading Watson Discovery to a newer 4.0 refresh](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=discovery-upgrading-watson-version-40){: external}.

For information about how to back up and restore data from a 2.x deployment so that you can use it with {{site.data.keyword.discoveryfull}} 4, read the following information:

-   [Backing up and restoring data in {{site.data.keyword.icp4dfull_notm}}](/docs/discovery-data?topic=discovery-data-backup-restore)
-   [Backing up and restoring data to 2.2.1 or earlier releases](/docs/discovery-data?topic=discovery-data-backup-restore-prior)

## Supported upgrade paths
{: #upgrade-data-paths}

The following table lists the supported upgrade paths for the {{site.data.keyword.discoveryshort}} service.

| 4.0 refresh in use | 4.0 refresh you can upgrade to |
|------------------------------|----------------------|
| 4.0.0 | 4.0.2 and 4.0.3 |
| 4.0.2 | 4.0.3 |
| 4.0.3 | 4.0.4 |
| 4.0.4 | 4.0.5 |
| 4.0.5 | 4.0.6 |
| 4.0.6 | 4.0.7 |
{: caption="Supported upgrade paths" caption-side="top"}

For more information about the supported upgrade paths for {{site.data.keyword.icp4dfull_notm}}, see [Upgrading {{site.data.keyword.icp4dfull_notm}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=upgrading){: external}.

## Dependencies
{: #upgrade-data-dependencies}

{{site.data.keyword.discoveryshort}} 4.0.5 has dependencies on the following packages. If you are using a manual subscription approval process, then you might be asked to approve updates to one or more of these resources.

-   `ibm-etcd-operator`
-   `ibm-minio-operator`
-   `ibm-elasticsearch-operator`
-   `ibm-model-train-classic-operator`
-   `ibm-rabbitmq-operator`
-   `ibm-watson-gateway-operator`
-   `ibm-watson-discovery-operator`

It also has dependencies on the following packages:

-   IBM Cloud Pak foundational services

    -   `ibm-common-service-operator`
    -   `ibm-namespace-scope-operator`
    -   `operand-deployment-lifecycle-manager`
    -   `cloud-native-postgresql`
    -   `ibm-cert-manager-operator`
    -   `ibm-licensing-operator`
    -   `ibm-zen-operator`

-   {{site.data.keyword.icp4dfull_notm}}

    `cpd-platform-operator`

### Changing the subscription approval policy

If you want to change the subscription approval policy after the initial installation of the service, you can patch the Subscription resource. 

1.  Check the current configuration by using the following command:

    ```bash
    oc get sub -n cpd-operators ibm-watson-discovery-operator-subscription -o jsonpath='{.spec.installPlanApproval}{"\n"}'
    ```
    {: codeblock}

    Either `Manual` or `Automatic` is returned. 
    
1.  To change the value of the `installPlanApproval` field, use a patch command. 

    For example, to change from `Automatic` to `Manual`, enter the following command:

    ```bash
    oc patch sub ibm-watson-discovery-operator-subscription --type=merge --patch '{"spec": {"installPlanApproval": "Manual"}}'
    ```
    {: codeblock}

For more information, see [Installing a specific version of an Operator](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.8/html/operators/user-tasks#olm-installing-specific-version-cli_olm-installing-operators-in-namespace){: external} in the Red Hat OpenShift documentation.
