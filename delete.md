---

copyright:
  years: 2019, 2023
lastupdated: "2022-12-08"

keywords: delete service

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Deleting a service instance
{: #delete}

The procedure that you follow to delete a service instance differs depending on how the instance was deployed.
{: shortdesc}

## Deleting a managed service instance [IBM Cloud]{: tag-ibm-cloud}
{: #delete-cloud}

When you delete a {{site.data.keyword.discoveryshort}} service instance, the data associated with your service is also removed.

Only the owner or someone with Administrator role-level access to the service instance can delete it.

To delete your {{site.data.keyword.discoveryshort}} service instance, complete the following steps:

1.  From the [IBM Cloud Resource list](https://cloud.ibm.com/resources){: external}, expand the **AI/Machine Learning** section.
1.  Find the service instance that you want to delete.
1.  Click the *Actions* menu icon, and then select **Delete**.

The data that is associated with the service instance is retained for 7 days. After the 7-day retention period, it is deleted. If a service instance is deleted by mistake, you can restore it as long as you do so before the 7-day window closes. For more information, see [Using resource reclamations](/docs/account?topic=account-resource-reclamation&interface=cli){: external} in the {{site.data.keyword.cloud_notm}} documentation.

For more information about how data is handled by {{site.data.keyword.cloud_notm}}, see the following information:

-   [Data Processing and Protection Datasheet](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=A1417A507E8211E6BA51E79BE9476040){: external}.
-   [IBM Cloud Data security and privacy terms](https://www.ibm.com/support/customer/csol/terms/){: external}

For more information about how to delete a deployment of the service from Cloud Pak for Data as a Service, see [Deleting a deployment](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/ml-deploy-delete.html?audience=wdp){: external}.

## Deleting an installed service instance [IBM Cloud Pak for Data]{: tag-cp4d}
{: #delete-cp4d}

Only the owner or an Administrator of the provisioned service instance can delete it.

To deprovision a service instance of {{site.data.keyword.discoveryshort}} for {{site.data.keyword.icp4dfull_notm}}, complete the following steps:

1.  From the {{site.data.keyword.icp4dfull_notm}} web client menu, click **Services > Instances**.
1.  Find your service instance, and then click the menu icon and choose **Delete**.

For more information about how to uninstall the service, see [Uninstalling {{site.data.keyword.discoveryshort}}](https://www.ibm.com/docs/SSQNUZ_4.5.x/svc-discovery/discovery-uninstall.html){: external}.
