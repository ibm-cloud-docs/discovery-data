---

copyright:
  years: 2020, 2025
lastupdated: "2025-02-13"

keywords: known issues

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Known issues
{: #known-issues}

Known issues are listed by the release in which they were identified.
{: shortdesc}



[IBM Cloud Pak for Data]{: tag-cp4d} [IBM Software Hub]{: tag-teal}

The known issues that are described in this topic apply to installed deployments only.
{: note}

## 5.1.x releases
{: #5dot1}

See [Limitations and known issues in Watson Discovery](https://www.ibm.com/docs/en/SSNFH6_5.1.x/svc-discovery/discovery-known-issues.html)

## 5.0.x releases
{: #5dot0}

See [Limitations and known issues in Watson Discovery](https://www.ibm.com/docs/SSQNUZ_5.0.x/svc-discovery/discovery-known-issues.html)

## 4.8.x releases
{: #4dot8}

See [Limitations and known issues in Watson Discovery](https://www.ibm.com/docs/SSQNUZ_4.8.x/svc-discovery/discovery-known-issues.html)

## 4.7.x releases
{: #4dot7}

See [Limitations and known issues in Watson Discovery](https://www.ibm.com/docs/SSQNUZ_4.7.x/svc-discovery/discovery-known-issues.html)

## 4.6.x releases
{: #4dot6}

See [Limitations and known issues in Watson Discovery](https://www.ibm.com/docs/SSQNUZ_4.6.x/svc-discovery/discovery-known-issues.html)

## 4.5.x releases
{: #4dot5}

See [Limitations and known issues in Watson Discovery](https://www.ibm.com/docs/SSQNUZ_4.5.x/svc-discovery/discovery-known-issues.html){: external}.

## 4.0.x releases
{: #4dot0}

For more information about known issues, see the [{{site.data.keyword.icp4dfull_notm}} documentation](https://www.ibm.com/docs/SSQNUZ_4.0/svc-discovery/discovery-known-issues.html){: external}.

## 4.0.9, 25 May 2022
{: #25may2022ki}

-   {{site.data.keyword.discoveryshort}} generates a partial failure status message for the {{site.data.keyword.icp4dfull_notm}} Red Hat OpenShift APIs for Data Protection (OADP) backup and restore utility.

    -  **Error**: When you check the status of the OADP backup utility after using it to backup a cluster where {{site.data.keyword.discoveryshort}} is installed, a `Phase: PartiallyFailed` message is displayed. One or more {{site.data.keyword.discoveryshort}} components are included in the `Failed` list.
    -  **Cause**: {{site.data.keyword.discoveryshort}} cannot be backed up and restored by using the OADP backup and restore utility. When the {{site.data.keyword.discoveryshort}} service is present, and an administrator backs up an entire {{site.data.keyword.icp4dfull_notm}} instance, a status message is displayed that indicates a partial failure. This status is displayed because the persistent volume claims (PVCs) for {{site.data.keyword.discoveryshort}} are not backed up. However, the message does not impact the back up of the rest of the services.
    -  **Solution**: No action is required to resolve the status message. You can remove the persistent volume claims that are associated with the Discovery service separately. After using the scripts to back up your Discovery service data, you can follow the step that is documented in the uninstall instructions for the Discovery service to delete the PVCs. For more information about how to remove the PVC associated with Discovery, see [Uninstalling the Discovery service](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=discovery-uninstalling-service){: external}.

## 4.0.8, 27 April 2022
{: #27april2022ki}

-   The wd-discovery-multi-tenant-migration job fails if anyone besides a system administrator performs the upgrade.

    -   **Error**: When you upgrade with a user ID other than admin, the migration job fails.
    -   **Cause**: The migration script assumes that the script is run by a user with the admin user ID.
    -   **Solution**: Apply a patch that allows the migration to be successful. Complete the following steps:

        1.  From the Cloud Pak for Data web client, get the user ID of the owner of the instance that you want to upgrade.
        1.  Download the `wd-migration-uid-patch.zip` patch file from the [Watson Developer Cloud GitHub](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/discovery-data/latest/wd-migration-uid-patch.zip){: external} repository.
        1.  Extract the **wd-migration-uid-patch.yaml** file from the archive file, and then open it in a text editor.
        1.  Replace the `<user_id>` variable with the user ID of the owner of the instance that you want to upgrade.
        1.  Run the following command in a terminal that is logged in to the cluster:

            ```bash
            oc create -f wd-migration-uid-patch.yaml
            ```
            {: codeblock}

        1.  Delete the previous migration job by using the following command:

            ```bash
            oc delete job wd-discovery-multi-tenant-migration
            ```
            {: codeblock}

    After the job is deleted, the migration job restarts and the migration resumes.

    The issue is fixed with the 4.0.9 release.

-   {{site.data.keyword.discoveryshort}} generates a partial failure status message for the {{site.data.keyword.icp4dfull_notm}} OpenShift® APIs for Data Protection (OADP) backup and restore utility.

    -  **Error**: When you check the status of the OADP backup utility after using it to backup a cluster where {{site.data.keyword.discoveryshort}} is installed, a `Phase: PartiallyFailed` message is displayed. One or more {{site.data.keyword.discoveryshort}} components are included in the `Failed` list.
    -  **Cause**: {{site.data.keyword.discoveryshort}} cannot be backed up and restored by using the OADP backup and restore utility. When the {{site.data.keyword.discoveryshort}} service is present, and an administrator backs up an entire {{site.data.keyword.icp4dfull_notm}} instance, a status message is displayed that indicates a partial failure. This status is displayed because the persistent volume claims (PVCs) for {{site.data.keyword.discoveryshort}} are not backed up. However, the message does not impact the back up of the rest of the services.
    -  **Solution**: No action is required to resolve the status message. You can remove the persistent volume claims that are associated with the Discovery service separately. After using the scripts to back up your Discovery service data, you can follow the step that is documented in the uninstall instructions for the Discovery service to delete the PVCs. For more information about how to remove the PVC associated with Discovery, see [Uninstalling the Discovery service](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=discovery-uninstalling-service){: external}.

## 4.0.7, 30 March 2022
{: #30March2022ki}

-   {{site.data.keyword.discoveryshort}} generates an error in the {{site.data.keyword.icp4dfull_notm}} OpenShift® APIs for Data Protection (OADP) backup and restore utility.

    -  **Error**: The utility does not complete successfully and the following message is written to the log: `preBackupViaConfigHookRule on backupconfig/watson-discovery in namespace cpd (status=error)`
    -  **Cause**: {{site.data.keyword.discoveryshort}} cannot be backed up and restored by using the OADP backup and restore utility. When the {{site.data.keyword.discoveryshort}} service is present, and an administrator attempts to backup an entire {{site.data.keyword.icp4dfull_notm}} instance, {{site.data.keyword.discoveryshort}} prevents the utility from completing successfully.
    -  **Solution**: Apply a patch that stops {{site.data.keyword.discoveryshort}} from preventing the utility from completing successfully.

       1.  Download the `wd-aux-br-patch.zip` file from the [Watson Developer Cloud Github](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/discovery-data/latest/wd-aux-br-patch.zip) repository.
       1.  Extract the `wd-aux-br-patch.yaml` file from the ZIP file.
       1.  Run the following command in a terminal that is logged in to the cluster:

           ```bash
           oc create -f wd-aux-br-patch.yaml
           ```
           {: pre}

    The issue is fixed with the 4.0.8 release. (You still cannot back up the Discovery service by using the OADP utility, but the OADP utility can back up other services when Discovery is installed.)

-   `Deployed` status of resources fluctuates after the 4.0.7 upgrade is completed.

    -   **Error**: When you check the status by submitting the `oc get WatsonDiscovery` command, the ready status of the resources toggles between showing `23/23` and `20/23` components as being ready for use.
    -   **Cause**: The readiness state of the resources is not reported consistently after a migration.
    -   **Solution**: Typically, the instance is ready for use despite the ready state instability. To manually refresh the status information, run the following commands in a terminal that is logged in to the cluster:

        ```sh
        oc proxy &
        curl -ksS -X PATCH -H "Accept: application/json, */*" -H "Content-Type: application/merge-patch+json" http://127.0.0.1:8001/apis/discovery.watson.ibm.com/v1/namespaces/<namespace>/watsondiscoveries/wd/status --data '{"status": null}'
        ```
        {: pre}

    This issue is fixed with the 4.0.8 release.

-   The wd-discovery-multi-tenant-migration job fails if anyone besides a system administrator performs the upgrade.

    -   **Error**: When you upgrade with a user ID other than admin, the migration job fails.
    -   **Cause**: The migration script assumes that the script is run by a user with the admin user ID.
    -   **Solution**: Apply a patch that allows the migration to be successful. Complete the following steps:

        1.  From the Cloud Pak for Data web client, get the user ID of the owner of the instance that you want to upgrade.
        1.  Download the `wd-migration-uid-patch.zip` patch file from the [Watson Developer Cloud GitHub](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/discovery-data/latest/wd-migration-uid-patch.zip){: external} repository.
        1.  Extract the **wd-migration-uid-patch.yaml** file from the archive file, and then open it in a text editor.
        1.  Replace the `<user_id>` variable with the user ID of the owner of the instance that you want to upgrade.
        1.  Run the following command in a terminal that is logged in to the cluster:

            ```bash
            oc create -f wd-migration-uid-patch.yaml
            ```
            {: codeblock}

        1.  Delete the previous migration job by using the following command:

            ```bash
            oc delete job wd-discovery-multi-tenant-migration
            ```
            {: codeblock}

    After the job is deleted, the migration job restarts and the migration resumes.

    The issue is fixed with the 4.0.9 release.

## 4.0.6, 1 March 2022
{: #01March2022ki}

-   Upgrade to 4.0.6 fails if no {{site.data.keyword.discoveryshort}} instance is provisioned in the existing cluster before you begin the upgrade process.

    -   **Error**: The 4.0.6 upgrade process assumes that a {{site.data.keyword.discoveryshort}} instance is provisioned in the existing cluster. For example, if you are upgrading from 4.0.5 to 4.0.6, you must have an instance provisioned in the 4.0.5 cluster before you begin the migration.
    -   **Cause**: The current code returns an error when no instance exists because it cannot find a document index to migrate.
    -   **Solution**: Verify that an instance of {{site.data.keyword.discoveryshort}} has been provisioned in the existing {{site.data.keyword.icp4dfull_notm}} cluster before you start the upgrade to 4.0.6. If you tried to upgrade to 4.0.6, but no instances were provisioned and the migration failed, remove the existing installation and install 4.0.6 from scratch.

-   `Deployed` status of resources fluctuates after the 4.0.6 upgrade is completed.

    -   **Error**: When you check the status by submitting the `oc get WatsonDiscovery` command, the ready status of the resources toggles between showing `23/23` and `20/23` components as being ready for use.
    -   **Cause**: The readiness state of the resources is not reported consistently after a migration.
    -   **Solution**: Typically, the instance is ready for use despite the ready state instability. The ready state settles after approximately 5 hours. You can wait for the readiness state to consistently show `23/23` or you can manually refresh the status information by running the following commands in a terminal that is logged into the cluster:

        ```sh
        oc proxy &
        curl -ksS -X PATCH -H "Accept: application/json, */*" -H "Content-Type: application/merge-patch+json" http://127.0.0.1:8001/apis/discovery.watson.ibm.com/v1/namespaces/<namespace>/watsondiscoveries/wd/status --data '{"status": null}'
        ```
        {: pre}

    This issue is fixed with the 4.0.8 release.

-   {{site.data.keyword.discoveryshort}} generates an error in the {{site.data.keyword.icp4dfull_notm}} OpenShift® APIs for Data Protection (OADP) backup and restore utility.

    -  **Error**: The utility does not complete successfully and the following message is written to the log: `preBackupViaConfigHookRule on backupconfig/watson-discovery in namespace cpd (status=error)`
    -  **Cause**: {{site.data.keyword.discoveryshort}} cannot be backed up and restored by using the OADP backup and restore utility. When the {{site.data.keyword.discoveryshort}} service is present, and an administrator attempts to backup an entire {{site.data.keyword.icp4dfull_notm}} instance, {{site.data.keyword.discoveryshort}} prevents the utility from completing successfully.
    -  **Solution**: Apply a patch that stops {{site.data.keyword.discoveryshort}} from preventing the utility from completing successfully.

       1.  Download the `wd-aux-br-patch.zip` file from the [Watson Developer Cloud Github](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/discovery-data/latest/wd-aux-br-patch.zip) repository.
       1.  Extract the `wd-aux-br-patch.yaml` file from the ZIP file.
       1.  Run the following command in a terminal that is logged in to the cluster:

           ```bash
           oc create -f wd-aux-br-patch.yaml
           ```
           {: pre}

    This issue was fixed with the 4.0.8 release. (You still cannot back up the Discovery service by using the OADP utility, but the OADP utility can back up other services when Discovery is installed.)

-   The wd-discovery-multi-tenant-migration job fails if anyone besides a system administrator performs the upgrade.

    -   **Error**: When you upgrade with a user ID other than admin, the migration job fails.
    -   **Cause**: The migration script assumes that the script is run by a user with the admin user ID.
    -   **Solution**: Apply a patch that allows the migration to be successful. Complete the following steps:

        1.  From the Cloud Pak for Data web client, get the user ID of the owner of the instance that you want to upgrade.
        1.  Download the `wd-migration-uid-patch.zip` patch file from the [Watson Developer Cloud GitHub](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/discovery-data/latest/wd-migration-uid-patch.zip){: external} repository.
        1.  Extract the **wd-migration-uid-patch.yaml** file from the archive file, and then open it in a text editor.
        1.  Replace the `<user_id>` variable with the user ID of the owner of the instance that you want to upgrade.
        1.  Run the following command in a terminal that is logged in to the cluster:

            ```bash
            oc create -f wd-migration-uid-patch.yaml
            ```
            {: codeblock}

        1.  Delete the previous migration job by using the following command:

            ```bash
            oc delete job wd-discovery-multi-tenant-migration
            ```
            {: codeblock}

    After the job is deleted, the migration job restarts and the migration resumes.

    The issue is fixed with the 4.0.9 release.

## 4.0.5, 26 January 2022
{: #26january2022ki}

-   {{site.data.keyword.discoveryshort}} generates an error in the {{site.data.keyword.icp4dfull_notm}} OpenShift® APIs for Data Protection (OADP) backup and restore utility.

    -  **Error**: The utility does not complete successfully and the following message is written to the log: `preBackupViaConfigHookRule on backupconfig/watson-discovery in namespace cpd (status=error)`
    -  **Cause**: {{site.data.keyword.discoveryshort}} cannot be backed up and restored by using the OADP backup and restore utility. When the {{site.data.keyword.discoveryshort}} service is present, and an administrator attempts to backup an entire {{site.data.keyword.icp4dfull_notm}} instance, {{site.data.keyword.discoveryshort}} prevents the utility from completing successfully.
    -  **Solution**: Apply a patch that stops {{site.data.keyword.discoveryshort}} from preventing the utility from completing successfully.

       1.  Download the `wd-aux-br-patch.zip` file from the [Watson Developer Cloud Github](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/discovery-data/latest/wd-aux-br-patch.zip) repository.
       1.  Extract the `wd-aux-br-patch.yaml` file from the ZIP file.
       1.  Run the following command in a terminal that is logged in to the cluster:

           ```bash
           oc create -f wd-aux-br-patch.yaml
           ```
           {: pre}

    This issue was fixed with the 4.0.8 release. (You still cannot back up the Discovery service by using the OADP utility, but the OADP utility can back up other services when Discovery is installed.)

## 4.0.4, 20 December 2021
{: #20december2021ki}

-   {{site.data.keyword.discoveryshort}} generates an error in the {{site.data.keyword.icp4dfull_notm}} OpenShift® APIs for Data Protection (OADP) backup and restore utility.

    -  **Error**: The utility does not complete successfully and the following message is written to the log: `preBackupViaConfigHookRule on backupconfig/watson-discovery in namespace cpd (status=error)`
    -  **Cause**: {{site.data.keyword.discoveryshort}} cannot be backed up and restored by using the OADP backup and restore utility. When the {{site.data.keyword.discoveryshort}} service is present, and an administrator attempts to backup an entire {{site.data.keyword.icp4dfull_notm}} instance, {{site.data.keyword.discoveryshort}} prevents the utility from completing successfully.
    -  **Solution**: Apply a patch that stops {{site.data.keyword.discoveryshort}} from preventing the utility from completing successfully.

       1.  Download the `wd-aux-br-patch.zip` file from the [Watson Developer Cloud Github](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/discovery-data/latest/wd-aux-br-patch.zip) repository.
       1.  Extract the `wd-aux-br-patch.yaml` file from the ZIP file.
       1.  Run the following command in a terminal that is logged in to the cluster:

           ```bash
           oc create -f wd-aux-br-patch.yaml
           ```
           {: pre}

    This issue was fixed with the 4.0.8 release. (You still cannot back up the Discovery service by using the OADP utility, but the OADP utility can back up other services when Discovery is installed.)

## 4.0.3, 18 November 2021
{: #18november2021ki}

-   The guided tours are not available in this release.

-   {{site.data.keyword.discoveryshort}} generates an error in the {{site.data.keyword.icp4dfull_notm}} OpenShift® APIs for Data Protection (OADP) backup and restore utility.

    -  **Error**: The utility does not complete successfully and the following message is written to the log: `preBackupViaConfigHookRule on backupconfig/watson-discovery in namespace cpd (status=error)`
    -  **Cause**: {{site.data.keyword.discoveryshort}} cannot be backed up and restored by using the OADP backup and restore utility. When the {{site.data.keyword.discoveryshort}} service is present, and an administrator attempts to backup an entire {{site.data.keyword.icp4dfull_notm}} instance, {{site.data.keyword.discoveryshort}} prevents the utility from completing successfully.
    -  **Solution**: Apply a patch that stops {{site.data.keyword.discoveryshort}} from preventing the utility from completing successfully.

       1.  Download the `wd-aux-br-patch.zip` file from the [Watson Developer Cloud Github](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/discovery-data/latest/wd-aux-br-patch.zip) repository.
       1.  Extract the `wd-aux-br-patch.yaml` file from the ZIP file.
       1.  Run the following command in a terminal that is logged in to the cluster:

           ```bash
           oc create -f wd-aux-br-patch.yaml
           ```
           {: pre}

    This issue was fixed with the 4.0.8 release. (You still cannot back up the Discovery service by using the OADP utility, but the OADP utility can back up other services when Discovery is installed.)

## 4.0.0, 13 July 2021
{: #13july2021ki}

-   Machine learning model enrichments that you apply by using the Analyze API can fail.

    -   **Error**: `[WKSML_MODEL_NAME]: Enrichment of a document failed`
    -   **Cause**: There is a known issue in Watson Knowledge Studio that can cause a timeout in enrichment processing.
    -   **Solution**: When you use the Analyze API to apply a Watson Knowledge Studio model enrichment to a collection, keep the size of the input document under 50 KB.

### 2.2.1 issues that were fixed in subsequent releases
{: #26feb2021ki-fixed}

-   [Fixed in version 4] If you add an {{site.data.keyword.knowledgestudiofull}} machine learning enrichment to a collection, the ingestion process might run very slowly but will eventually complete. If ingestion processes slowly, you might see the following error message in **Warnings and errors**:

    ```text
    [WKSML_MODEL_NAME]: Document analysis timed out
    ```

    For additional timeout details, you can check your {{site.data.keyword.knowledgestudioshort}} machine learning logs, which might look similar to the following:

    ```json
    {
      "message": "Analysis failed due to:
        org.apache.uima.analysis_engine.AnalysisEngineProcessException
        at c.i.n.b.SIREAnnotator.process(_:454)
      ... ",
      "level": "SEVERE",
    }
    ```
    {: codeblock}

    Documents that time out during processing are indexed without {{site.data.keyword.knowledgestudioshort}} enrichment results.

## 2.2.1, 26 February 2021
{: #26feb2021ki}

-   Deployment timing issue:

    -   **Error**: After installing patch 7, when you try to provision a service instance, a `404 Not Found` error is displayed. The following message might be logged for the `nginx` pods: `open() "/usr/local/openresty/nginx/html/watson/common/discovery/auth" failed (2: No such file or directory)`
    -   **Solution**: Restart the `zen-watcher` pod.

-   If you perform an air-gapped installation that pulls container images from an external container registry, you might experience the following issue:

    -   **Error**: Some {{site.data.keyword.discoveryshort}} pods might report an `ImagePullBackoff` error.
    -   **Cause**: The wrong image pull secret is being used.
    -   **Solution**: Complete the following steps during the installation:

        -   Start installing Watson {{site.data.keyword.discoveryshort}}.
        -   After watson-discovery-operator module completes, check if a WatsonDiscovery custom resource is created by running the following command:

            ```sh
            oc get WatsonDiscovery wd
            ```
            {: pre}

        -   After the custom resource is created, run the following commands to point the correct image pull secret to pull images from the external registry:

            ```sh
            pull_secret=$(oc get secrets | grep 'docker-pull-.*-watson-discovery-registry-registry' | cut -d ' ' -f 1)
            cat << EOS > discovery-patch.yaml
            spec:
              shared:
                imagePullSecret: $pull_secret
            EOS
            oc patch wd wd --type=merge --patch "$(cat discovery-patch.yaml)"
            ```
            {: codeblock}

        -   If the `RabbitMQ` pods are still in ImagePullBackoff state, remove the RabbitMQ CR to enable the rabbitmq-operator to re-create the RabbitMQ clusters. You can use the following command:

            ```sh
            oc delete IbmRabbitmq wd-rabbitmq
            ```
            {: pre}

-   In {{site.data.keyword.discoveryfull}}, the `Content Mining` project only supports one collection per project. If you create more than one `Content Mining` collection, you might experience errors. If you experience errors, delete additional `Content Mining` collections so that each `Content Mining` project has only one associated collection.
-   If you are preparing your {{site.data.keyword.discovery-data_short}} clusters for an in-place upgrade of your instance from 2.2.0 to 2.2.1, occasionally, the `cpd-cli adm` command fails, showing the following error message: `Error from server (UnsupportedMediaType): error when applying patch`. If you receive this error message, enter `oc delete scc cpd-zensys-scc cpd-user-scc cpd-noperm-scc edb-operator-scc admin-discovery-scc` to delete the related resources, and re-enter the `cpd-cli adm` command.
-   If you are upgrading your {{site.data.keyword.discovery-data_short}} instance from 2.2.0 to 2.2.1, occasionally, the `cpd-cli upgrade` command completes before rolling updates complete. For information about verifying that your upgrade completed successfully, see [Verifying that your upgrade completed successfully](/docs/discovery-data?topic=discovery-data-install#verify-upgrade).
-   Model-train images are not updated after upgrading from {{site.data.keyword.discoveryshort}} 2.2.0 to 2.2.1. To work around this issue, delete the deployments that the model-train operator creates, and wait for the operator to recreate the deployments. Enter the following command to delete the deployments:

    ```sh
    oc delete deploy -l 'app.kubernetes.io/managed-by=ibm-modeltrain'
    ```
    {: pre}

    After you run this command, the model-train operator creates new deployments.

-   If you upgrade {{site.data.keyword.discovery-data_short}} from 2.2.0 to 2.2.1, you might receive the following error message:

    ```text
    [ERROR] [2021-03-04 05:12:44-0657] Exiting due to error (Storage class is immutable. Module ibm-watson-gateway-operator x86_64 from Assembly portworx-shared-gp3 was installed with ibm-watson-gateway-operator x86_64, but new install/upgrade command is requesting portworx-db-gp3-sc. If you installed the assembly with a different storage class, please upgrade it individually.). Please check /ibm/cpd-cli-workspace/logs/CPD-2021-03-04T05-12-04.log for details
    [ERROR] 2021-03-04T05:12:44.659615Z Execution error:  exit status 1
    ```

    This error message is generated because the storage class that was used for installation is different than the one that was used during the upgrade. This discrepancy results from a different add-on installing the dependency operators because the storage class dependency operators of the different add-on were recorded as the ones that were used for installation. To work around this issue, you must upgrade the following subassemblies individually:

    -   Upgrade the Watson gateway operator:

        ```sh
        ./cpd-cli upgrade \
        --repo ./repo.yaml \
        --assembly ibm-watson-gateway-operator \
        --arch Cluster_architecture \
        --namespace <Project> \
        --transfer-image-to <Registry_location> \
        --cluster-pull-prefix <Registry_from_cluster> \
        --ask-pull-registry-credentials \
        --ask-push-registry-credentials
        ```
        {: pre}

    -   Upgrade Minio operator:

        ```sh
        ./cpd-cli upgrade \
        --repo ./repo.yaml \
        --assembly ibm-minio-operator \
        --namespace <Project> \
        --transfer-image-to <Registry_location> \
        --cluster-pull-prefix <Registry_from_cluster> \
        --ask-pull-registry-credentials \
        --ask-push-registry-credentials
        ```
        {: pre}

    -   Upgrade RabbitMQ operator:

        ```sh
        ./cpd-cli upgrade \
        --repo ./repo.yaml \
        --assembly ibm-rabbitmq-operator \
        --namespace <Project> \
        --transfer-image-to <Registry_location> \
        --cluster-pull-prefix <Registry_from_cluster> \
        --ask-pull-registry-credentials \
        --ask-push-registry-credentials
        ```
        {: pre}

    -   Upgrade etcd operator:

        ```sh
        ./cpd-cli upgrade \
        --repo ./repo.yaml \
        --assembly ibm-etcd-operator \
        --namespace <Project> \
        --transfer-image-to <Registry_location> \
        --cluster-pull-prefix <Registry_from_cluster> \
        --ask-pull-registry-credentials \
        --ask-push-registry-credentials
        ```
        {: pre}

    -   Upgrade model train classic operator:

        ```sh
        ./cpd-cli upgrade \
        --repo ./repo.yaml \
        --assembly modeltrain-classic \
        --arch Cluster_architecture \
        --namespace <Project> \
        --transfer-image-to <Registry_location> \
        --cluster-pull-prefix <Registry_from_cluster> \
        --ask-pull-registry-credentials \
        --ask-push-registry-credentials
        ```
        {: pre}

    -   Upgrade Elasticsearch operator:

        ```sh
        ./cpd-cli upgrade \
        --repo ./repo.yaml \
        --assembly ibm-cloudpakopen-elasticsearch-operator \
        --namespace <Project> \
        --transfer-image-to <Registry_location> \
        --cluster-pull-prefix <Registry_from_cluster> \
        --ask-pull-registry-credentials \
        --ask-push-registry-credentials
        ```
        {: pre}

        where `<Project>` is the namespace where your {{site.data.keyword.discovery-data_short}} 2.2.0 instance is installed, where `<Registry_location>` is the location of the images that you pushed to the registry server, and where `<Registry_from_cluster>` is the location from which pods on the cluster can pull images.

-   When you install on {{site.data.keyword.icp4dfull_notm}} 3.5, you might encounter the following issue:

    -   **Error**: If you try to provision the {{site.data.keyword.discoveryshort}} service on a cluster where Planning Analytics is running, some of the {{site.data.keyword.discoveryshort}} pods don't start and installation fails. The logs for the pod show messages such as, `java.lang.NumberFormatException: For input string`.
    -   **Cause**: An environment variable named `COUCHDB_PORT` is added to the Kubernetes cluster by the couchdb service that is installed with Planning Analytics. {{site.data.keyword.discoveryshort}} does not use couchdb, and therefore does not specify a value for this environment variable. However, some pods attempt to parse the variable, which results in the error.
    -   **Solution**: [Install patch cpd-watson-discovery-2.2.1-patch-1](https://www.ibm.com/docs/en/cloud-paks/cp-data/3.5.0?topic=iwd-installing-watson-discovery#svc-install__patches-section){: external}, which fixes this issue.

Also, see the issues in all previous releases.

## 2.2, 8 December 2020
{: #8dec2020ki}

-   When a small CSV file (generally a CSV with 99 lines or fewer) is uploaded, the header and/or first row may not be ingested correctly. If this happens, in the tooling, navigate to the CSV Settings tab and update the settings. After reprocessing, navigate to the **Manage fields** tab and update the field types if needed.
-   If you have set up your collections using a custom crawler built with the [{{site.data.keyword.icp4dfull_notm}} custom connector](/docs/discovery-data?topic=discovery-data-build-connector), and then remove the custom crawler deployment, the Processing Settings page will not display the crawler configuration. This is because the underlying crawler is not available. To work around this issue, confirm that the custom crawler is deployed when there are collections using it.
-   When using a [{{site.data.keyword.icp4dfull_notm}} custom connector](/docs/discovery-data?topic=discovery-data-build-connector) with {{site.data.keyword.discoveryshort}} for {{site.data.keyword.icp4dfull_notm}} 2.2, the script `scripts/manage_custom_crawler.sh` used to deploy and remove the deployment of the custom crawler fails. To work around this issue, replace  line 37 `podname="gateway"` with `podname="wd-discovery-gateway"` in `scripts/manage_custom_crawler.sh`, and then rerun the deploy command.
-   When you create a custom enrichment in the tooling, you must choose a field the enrichment should be applied to and click **Apply**. If no field is selected, then the **Apply and reprocess** button will be disabled for enrichments changes until the new enrichment has a field.
-   If you apply the [Contracts](/docs/discovery-data?topic=discovery-data-contracts-schema) enrichment or the [Understanding tables](/docs/discovery-data?topic=discovery-data-understanding_tables) enrichment to a collection, you might receive the following error message when that collection is ingesting documents: `The number of nested documents has exceeded the allowed limit of [X].` Contact the [IBM Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external} to adjust the limit.
-   When text is enriched with a custom dictionary, the output of `entities.type` should be the full facet path for the Dictionary enrichment. However, in this release, the full facet path will not be displayed. To work around this, reprocess the collection. For example, if the facet path is `sample1.sample2`, it will look like this before reprocessing:

    ```json
    {
      "result" : {
        "enriched_text" : [
          {
            "entities" : [
              {
                "text" : "capital",
                "type" : "sample2",
                ...
                "model_name" : "Dictionary:.sample1.sample2"}
                ...
    ```
    {: codeblock}

    And this after:

    ```json
    {
      "result" : {
        "enriched_text" : [
          {
            "entities" : [
              {
                "text" : "capital",
                "type" : "sample1.sample2",
                ...
                "model_name" : "Dictionary:.sample1.sample2"}
                ...
    ```
    {: codeblock}

-   When a CSV file is uploaded with the converter settings set to `auto_detection=true`, the **CSV settings** tab in the tooling will display the incorrect settings. If you update the settings on the **CSV settings** tab, `auto_detection` will no longer be set to `true`.
-   In Office documents ('.doc', '.docx', '.odf', '.xls', '.xlsx', '.ods', '.ppt', '.pptx', '.odp') converted using a Smart Document Understanding (SDU) custom model, the `publicationdate` may not display in `extracted_metadata` field in the JSON response. It will instead appear in the `html` field of the JSON response. The `publicationdate` in the `html` field will be the date the document was ingested and not the document's original publication date.
-   The Analyze API uses an in-memory cache to hold the enrichment models associated with the collection used to run the documents. If the collection contains many large enrichments or multiple of these collections are used at the same time, the cache may run out of memory. When this happens, the Analyze API returns null results (see example) and the stateless api rest proxy will display this message in its log: `RESOURCE_EXHAUSTED: stateless.Analysis/analyze: RESOURCE_EXHAUSTED`.

    ```json
    {
      "result": null,
      "notices": null
    }
    ```
    {: codeblock}

    To work around this issue:

    1.  Review the enrichments used in the collection and remove those that are not necessary for your application. In particular, remove the *Part of Speech* enrichment.
    1.  Reduce the number of collections used concurrently with the Analyze API.
    1.  Increase the cache memory:

        -   Increase the memory limit of `container model-runtime` in `deployment core-discovery-stateless-api-model-runtime` to `10` GB or more
        -   Edit the environment variable `CAPACITY_MB` in `deployment core-discovery-stateless-api-model-runtime`, set it to 1`0240` or more

-   If the model runtime container is restarted but the model mesh runtime container is not, the Analyze API can run into problems.

    -   **Error**: The Analzye API call returns 500 error on a specific collection and the log contains the following entry:

        ```json
        "message": "error occurred in analyzer
          java.lang.NullPointerException
          at c.i.e.a.a.s.r.ModelManager$2.analyze(ModelManager.java:112)
        ```
        {: codeblock}

    -   **Cause**: The model runtime container and model mesh runtime container are out of sync.
    -   **Solution**: Delete the `wd-stateless-api-model-runtime` pods to restart both the model mesh and model runtime containers.

Also see the issues identified in all previous releases.

## 2.1.4, 2 September 2020:
{: #2sept2020ki}

- When configuring a Web crawl using FORM authentication, if you specify a URL without a trailing slash, for example: `https://webcrawlurl.com`, the web crawl will only crawl the login page. To work around this issue, add a trailing slash to the URL, for example: `https://webcrawlurl.com/`.
- The [Guided Tours](/docs/discovery-data?topic=discovery-data-tours) do not run on Firefox. For the list of other supported browsers, see [Browser support](/docs/discovery-data?topic=discovery-data-about#about-browser).
- Ingesting documents into a collection that uses a custom [Advanced Rules model](/docs/discovery-data?topic=discovery-data-domain-pattern#advanced-rules) built in Watson Knowledge Studio may fail if multiple extractors in the model internally use the same names for one or more output views.
- If you delete a large number of documents, then immediately ingest a large number of documents, it may take longer for all the documents to become available.
- The [Classifier](/docs/discovery-data?topic=discovery-data-domain-classifier) enrichment doesn't work when FIPS (Federal Information Processing Standards) is enabled.

Also see the issues identified in all previous releases.

### 2.1.4 issues that were fixed in subsequent releases
{: #2sept2020ki-fixed}

-   [Fixed in version 2.2] In the deployed Content Mining application, if you include the tilde (~) symbol in a search query to enable fuzzy matching or include an asterisk (*) symbol to represent a wildcard, the search customizations function properly, but the matching string is not highlighted in the query result.
-   [Fixed in version 2.2] A conversion error may occur when the **Include in index** field on the **Manage fields** tab in the tooling is changed. The document will not be indexed if this error occurs. To work around the issue:
    1.  `oc edit sts core-discovery-converter`
    1.  Edit between `containers` and `- name: INGESTION_POD_NAME` as follows:

        ```yaml
        containers:
          - command:
            - bash
            - -c
            - |
              FILE=/opt/ibm/wex/zing/bin/converter.sh &&
              sed -i "/choreo_2.11-9.1.1.jar/d" $FILE &&
              sed -i "/disco-doc-conversion-commons_2.11-1.0.4.jar/d" $FILE &&
              sed -i "/jackson-module-scala_2.11-2.10.4.jar/d" $FILE &&
              sed -i "/macro-compat_2.11-1.1.1.jar/d" $FILE &&
              sed -i "/pureconfig-core_2.11-0.12.2.jar/d" $FILE &&
              sed -i "/pureconfig-generic-base_2.11-0.12.2.jar/d" $FILE &&
              sed -i "/pureconfig-generic_2.11-0.12.2.jar/d" $FILE &&
              sed -i "/pureconfig-macros_2.11-0.12.2.jar/d" $FILE &&
              sed -i "/pureconfig_2.11-0.12.2.jar/d" $FILE &&
              sed -i "/scala-guice_2.11-4.1.1.jar/d" $FILE &&
              sed -i "/scala-logging_2.11-3.7.2.jar/d" $FILE &&
              sed -i "/scalactic_2.11-3.0.5.jar/d" $FILE &&
              sed -i "/scalaj-http_2.11-2.3.0.jar/d" $FILE &&
              sed -i "/service-commons_2.11-22.1.0.jar/d" $FILE &&
              sed -i "/shapeless_2.11-2.3.3.jar/d" $FILE &&
              /opt/ibm/wex/zing/bin/entrypoint.sh /opt/ibm/wex/zing/bin/controller.sh
            env:
            - name: INGESTION_POD_NAME
        ```
        {: codeblock}

        Added lines from `- command:` to `/opt/ibm/wex/zing/bin/entrypoint.sh` `/opt/ibm/wex/zing/bin/controller.sh` and removed `-` before `env:`

    1.  Save the changes. It will restart the `converter` pod.

## 2.1.3, 19 June 2020:
{: #19jun2020ki}

- `Entity Subtypes` in {{site.data.keyword.knowledgestudiofull}} Machine Learning models are not supported in {{site.data.keyword.discovery-data_short}} 2.1.3 or later. For instructions on converting existing models, contact the [Support center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.
- You cannot upload CSV files that include a space in the file name (for example: `file 1.csv`) to a Content Mining project. Rename the file to work around the issue.
- When performing Project level relevancy training, if you have multiple collections, and two or more of those collections contains a duplicate `document_id`, then project level relevancy training will fail. Example of duplicate `document_ids`: `Collection A` contains a document with the id of `1234`, and `Collection B` also contains a document with the id of `1234`.
- Only the first facet using a field with the prefix `extracted_metadata` is saved correctly after creation. Others with that prefix will appear but after a screen refresh will be gone. This only happens once per project, so the workaround is to refresh and add the facet again.
- [IBM Cloud Pak for Data]{: tag-cp4d} During installation on {{site.data.keyword.icp4dfull}} 2.5.0.0, some Kubernetes Jobs may incorrectly report their status as `OOMKilled`, causing the install to timeout. To resolve this, once a Job returns `OOMKilled` verify the logs of the Pod associated with that Job. There should be no obvious error messages in the logs and the resources are reported in the logs as created. Manually verify these resources exist in the namespace and then delete the Job. This will cause the install to continue.
- Some documents may show two `html` fields when applying an enrichment. Both `html` fields shown are the same and operate as such.
- When creating a data source in Firefox, you may not see the entire list of options, including the **More processing settings** settings. To work around the issue, zoom out, increase the browser height, or use another supported browser.
- When customizing the display of search results, the changes made sometimes do not save after clicking the `Apply` button. To work around this issue, refresh the browser and try to make the changes again.
- When setting up a data source or web crawler for your collection, if you enter an incorrect configuration, then try to update it on the **Processing settings** page, the data source update or crawl may not start when you click the `Apply changes and reprocess` button. You can confirm this issue by opening the **Activity** page for your collection to see if processing has started. If you see that processing has not started for your data source, click the `Recrawl` button, then the `Apply changes and reprocess` button. If you see that processing has not started for your web crawl, click the `Stop` button, then the `Recrawl` button.
- [IBM Cloud Pak for Data]{: tag-cp4d} When running Helm tests on the `core` deployment using `helm test core`, the `core-discovery-api-post-install-test` will return a `FAILED` status. This is due to a bug within the `test` pod's image. The test result can be ignored as the failure is not related to anything within the deployment.
- By default, Optical Character Recognition (OCR) is set to `off` when you create any **Project type** with the tooling. However, if you create a Project using the API, OCR is set to `on`. To work around this issue, open the Tooling and change the **Project setting** to `off`.
- When Optical Character Recognition (OCR) is set to `on` for a Collection AND no trained Smart Document Understanding (SDU) model is applied, PNG, TIFF, and JPG files will not be processed for text recognition. Images embedded in PDF, Word, PowerPoint, and Excel documents will not be processed - only the non-image portion of these documents will be processed for text recognition. To work around this issue, import or train an SDU model and reprocess the collection. This will allow text to be extracted from the images.
- After you create a Search Skill in Watson Assistant and are directed to the Watson {{site.data.keyword.discoveryshort}} tooling, the screen is blank. This happens because the URL is missing the {{site.data.keyword.discoveryshort}} instance ID. To work around this issue:

    1.  From the {{site.data.keyword.icp4dfull_notm}} web client menu, choose **My Instances**. For example: `https://mycluster.com/zen/#/myInstances`.
    1.  Select the {{site.data.keyword.discoveryshort}} instance you are using and click **Launch Tool**.
    1.  Once the tooling is loaded, the URL should have the following structure: `https://mycluster.com/discovery/core/instances/00000000-0000-0000-0001-597165341876/projects`
    1.  Copy the entire path, excluding `/projects`. For example: `https://mycluster.com/discovery/core/instances/00000000-0000-0000-0001-597165341876`
    1.  Go back to the browser tab that is displaying the blank {{site.data.keyword.discoveryshort}} screen. That URL structure will look like this: `https://mycluster.com/discovery/core/collections/new?redirect_uri=...`
    1.  Replace `https://mycluster.com/discovery/core` with the URL you copied previously, so the new URL should look like this: `https://mycluster.com/discovery/core/instances/00000000-0000-0000-0001-597165341876/collections/new?redirect_uri=...`
    1.  Press enter to open updated URL. You should now be on the Watson {{site.data.keyword.discoveryshort}} **Manage collections** page.

Also see the issues identified in all previous releases.

## 2.1.2, 31 March 2020
{: #31mar2020ki}

-   When using passage retrieval with Korean, Polish, Japanese, Slovak or Chinese you may encounter much slower response times in this version. To resolve this, either disable passage retrieval, or upload a custom stopword list with words that are common in your documents (for example, prepositions and pronouns).  See [Defining stopwords](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-search-settings#stopwords) for example stopword lists in several languages. Also see [Stopwords ISO](https://github.com/stopwords-iso/){: external}) on GitHub.
-   [Update: fixed in version 2.1.3] In versions 2.1.2, 2.1.1, and 2.1.0, PNG, TIFF, and JPG individual image files are not scanned, and no text is extracted from those files. PNG, TIFF, and JPEG images embedded in PDF, Word, PowerPoint, and Excel files are also not scanned, and no text is extracted from those image files.
-   Smart Document Understanding does not support `.doc`, `.docx`, `.odf`, `.xls`, `.xlsx`, `.ods`, `.ppt`, `.pptx`, and `.odp` conversion when FIPS (Federal Information Processing Standards) is enabled.
-   In a Content Mining application, any document flags set will disappear if the index is rebuilt for that collection.
-   Beginning with the 2.1.2 release, uploading and managing relevancy training data using the v1 APIs will not train a relevancy training model. The v1 APIs have been superseded by the [Projects relevancy training v2 APIs](https://{DomainName}/apidocs/discovery/discovery-data#createtrainingquery){: external}. If your training data needs to be preserved, it can be listed using the v1 API, then added to a project with the v2 API.
-   Multiple [Regular expressions](/docs/discovery-data?topic=discovery-data-domain-regex) cannot be applied to a collection at the same time.
-   [IBM Cloud Pak for Data]{: tag-cp4d} There were two small changes to the installation instructions README included with the download of {{site.data.keyword.discovery-data_long}}. For the updated version of the README, see the [{{site.data.keyword.discoveryshort}} Helm chart README.md](https://github.com/ibm-cloud-docs/data-readmes/blob/master/discovery-README.md){: external}.

    -   A change to the description of the `--cluster-pull-prefix PREFIX` argument.
    -   The language extension pack name has been updated from `ibm-watson-discovery-pack1-2.1.2.tar.xz.` to `ibm-wat-dis-pack1-prod-2.1.2.tar.xz`.

Also see the issues identified in all previous releases.

## 2.1.1, 24 January 2020
{: #24jan2020ki}

- When creating a [dictionary](/docs/discovery-data?topic=discovery-data-facets#facetdict), suggested dictionary terms are normalized to lowercase by default (for example, Watson Assistant will be normalized to watson assistant). To ensure matching on uppercase terms, they should be explicitly included as part of the `Other terms` list or as the `Base term`.
- When backing up and restoring data, training data does not restore successfully. If the documents in your collection were added by crawl using a connector or web crawl, your training data can be separately retrieved for backup from an existing project and uploaded to a new restored project. For more information, see [List training queries](https://{DomainName}/apidocs/discovery/discovery-data#isttrainingqueries){: external} and [Create training queries](https://{DomainName}/apidocs/discovery/discovery-data#createtrainingquery){: external}) in the API reference.
- When crawling SharePoint Online or SharePoint OnPrem documents, JSON documents may not be indexed correctly and the `title` returned may be `errored`. This is because SharePoint web services use the `ows_FileRef` property to retrieve JSON files, which will return an error page. To fix this issue, contact your SharePoint Administrator and Microsoft Support.
- If you migrate a collection created in version 2.0.1 to either version 2.1.0 or 2.1.1, that collection will not have a **Project type** assigned and the collection will not be available to be queried. To assign a **Project type**, open the **Projects** page by selecting **My Projects**. Name your project and choose one of the Project types: `Document Retrieval`, `Conversational Search`, `Content Mining`, or `Custom`.

Also see the issues identified in all previous releases.

### 2.1.1 issues that were fixed in subsequent releases
{: ##24jan2020ki-fixed}

-   [Fixed in version 2.1.2] When installing {{site.data.keyword.discovery-data_short}} on OpenShift, the `ranker-rest` service might intermittently fail to startup, due to an incompatible jar in the `classpath`. To fix the issue:

    1.  Open the `ranker-rest` editor with this command: `kubectl edit deployment {release-name}-{watson-discovery}-ranker-rest`
    2.  In the editor, search for the `ranker-rest image` (for example: `{docker-registry}/{namespace}/discovery-ranker-rest-service:20200113-150050-2-d1527c2`)
    3.  Add the following command below `{docker-registry}/{namespace}/discovery-ranker-rest-service:20200113-150050-2-d1527c2`:

        ```sh
        command: ["/tini"]
        args: ["-s", "-v", "--", "java", "-Dkaryon.ssl=true", "-Dkaryon.port=9081", "-Dkaryon.ssl.port=9090", "-Dkaryon.ssl.certificate=/opt/bluegoat/karyon/ssl/karyon-cert.pem", "-Dkaryon.ssl.privatekey=/opt/bluegoat/karyon/ssl/karyon-private-key.pem", "-Djavax.net.ssl.trustStore=/opt/bluegoat/karyon/ssl/keystore.jks", "-Djavax.net.ssl.keyStore=/opt/bluegoat/karyon/ssl/keystore.jks", "-Dlog4j.debug=false", "-Dlitelinks.threadcontexts=log4j_mdc", "-Dwatson.ssl.truststore.path=/opt/bluegoat/karyon/ssl/litelinks-truststore.jks", "-Dwatson.ssl.truststore.password=watson15qa", "-Dlitelinks.delay_client_close=false", "-Drxnetty.http.maxcontentlength=314572800", "-cp", "lib/logback-classic-1.2.3.jar:*:lib/*", "com.ibm.watson.raas.rest.Runner"]
        ```
        {: pre}

## 2.1.0, 27 November 2019
{: #29nov2019ki}

- When you apply an enrichment to a collection, the enrichment language must match the collection language, or it will fail. The tooling displays all the collections, regardless of language.
- On the Manage Fields tab, you can edit system-generated fields. The following fields should not be edited by changing the field type or turning off indexing: `document_id`, `extracted_metadata`, `metadata`.
- When you delete a Collection and select the option `Don't delete underlying data`, any incomplete document ingestion crawls will continue running in the background, which will impact the new crawl start times, until the existing crawls are completed.
- [IBM Cloud Pak for Data]{: tag-cp4d} {{site.data.keyword.discoveryshort}} can fail to start up correctly due to components getting into a lock state. Manual database intervention may be needed to clear the lock. For more information on identifying and resolving this issue, see [Clearing a lock state](/docs/discovery-data?topic=discovery-data-troubleshoot#troubleshoot-ls).
- If you upload a document with the Upload Data function, delete that document, and then try to upload either the same document or another document with the same document ID,the upload will fail and the message `Error during creating a document` will be displayed.
- Documents that produce an `html` field when processed can not be used with relevancy training. html is produced for documents processed with Smart Document Understanding or Content Intelligence. The `html` field must be removed before relevancy training can complete successfully.
- If the *Part of Speech* enrichment is not turned on: Dynamic facets will not be created, Dictionary suggestions cannot be used, Content Miner "extracted facets" will not generate.
- [Update: fixed in version 2.1.1] {{site.data.keyword.discoveryshort}} for Content Intelligence and Table Understanding enrichments are configured out of the box to be applied on a field named `html`. When a user uploads a JSON document without a root-level field named `html`, these enrichments will not yield results in the index. To run the enrichments on this kind of JSON documents, users must re-configure the enrichments to run on an existing field (or fields) in the JSON document.
- When viewing the Content Miner deploy page, sometimes the full application URL is not displayed for copying. To fix, refresh the page.
- [Update: fixed in version 2.1.2] Deprovisioning a {{site.data.keyword.discovery-data_long}} Instance will not delete the underlying data. Delete the collections and documents manually.
- [Update: fixed in version 2.1.3] On the Improvement tools panel, the enrichment `Sentiment of phrases` is listed, but is not currently available.
- In Content Mining projects, the `dates` fields may not be parsed properly for display in facets.
- The Dynamic facets toggle should not appear in Content Mining projects.
- A minimum of 50-100 documents should be ingested to see valid dynamic facets generated.
- If you click **Stop** to stop a crawler and the converter processes slowly or has errors, you might see a status of the crawler running.
- The total size limit of all non-HTML fields in uploaded and crawled documents is 1MB, which is equivalent to 1,048,576 bytes, and the total size limit of all HTML fields in these documents is 5MB. If you exceed either limit, you receive an error message stating `The document has fields/HTML fields that exceed the 1 MB/5 MB limit.`, and the document is not ingested. For assistance on increasing either size limit, contact the [IBM Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.

Also see the issues identified in all previous releases.

## 2.0.1, 30 August 2019
{: #30aug2019ki}

- After you create a Machine Learning enrichment using a {{site.data.keyword.knowledgestudiofull}} model, two identically named enrichments may display on the **Enrich fields** page. This will not affect the enrichments, but it is best to use only one of them to select and apply the enrichment to one or more fields.
- If a web crawl appears to be stuck processing at a fixed number of documents, and the message displayed on the **Logs** page is `The ingestion job <jobid> is terminated incorrectly`, contact IBM support for assistance restarting the crawl.
- If one or more of your collections is trained, the training data from one of those collection may display on the **Train** page of an untrained collection. Refresh the page to clear that training data.
- The following types of documents will not be processed if they do not have the proper file extension: .docx, .pptx, .xlsx.

Also see the issues identified in the previous release.

### 2.0.1 issues that were fixed in subsequent releases
{: #30aug2019ki-fixed}

- [Fixed in version 2.1.2] When you upload documents to a collection with existing documents, a `Documents uploaded!` message displays on the **Activity** page, but no further processing status displays until the number of documents increases.

## General Availability (GA) release, 28 June 2019
{: #known-issues-ga}

- If you are working in the {{site.data.keyword.discovery-data_short}} tooling, and your {{site.data.keyword.icp4dfull}} session expires, you will receive a blank page. To return to the tooling, refresh the browser and log back in.
- All JSON files ingested into {{site.data.keyword.discoveryshort}} should include the .json file extension.
- When querying  on the `collection_id` of a trained collection, the `training_status.notices` value may occasionally display as `0` instead of the correct value.
- Not all query limitations are enforced in this release. See [query limitations](/docs/discovery-data?topic=discovery-data-query-reference#query-limitations) for the complete list of banned fields.
- In JSON source documents, you should not duplicate the following system-generated fields: `document_id`, `parent_document_id`, `filename`, and `title`. This will cause the duplicate fields to nest within arrays and break certain features, such as ranker training.
- Do not include a root-level `metadata` property in your JSON documents. If you upload a JSON document that already contains a root-level `metadata` property, then the `metadata` property of the indexed document will be converted to an array in the index.
- Do not use metadata for column names in your CSV files. If you upload a CSV file that uses metadata for the column names in the header, then the `metadata` property of the indexed document will be converted to an array in the index.
- CSV files must use commas (`,`) or semicolons (`;`) as delimiters; other delimiters are not supported. If your CSV file includes values containing either commas or semicolons, you should surround those values in double quotation marks so they are not separated. If header rows are present, the values within them are processed in the same manner as values in all other rows. The last row of CSV files will not be processed if not followed by a CRLF (carriage return).
- Currently, unique collection names are not enforced. Using duplicate collection names is not recommended and should be avoided
