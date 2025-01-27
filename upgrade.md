---

copyright:
  years: 2015, 2025
lastupdated: "2023-06-30"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Upgrading
{: #upgrade}

Learn how to upgrade your service plan.
{: shortdesc}

[IBM Cloud]{: tag-ibm-cloud} **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments. For more information about upgrading an installed deployment that is hosted by {{site.data.keyword.icp4dfull_notm}}, see [Upgrading the service](/docs/discovery-data?topic=discovery-data-upgrade-data).
{: note}

## Upgrading your plan
{: #upgrade-plan}

You can explore the {{site.data.keyword.discoveryshort}} [service plan options](https://www.ibm.com/cloud/watson-discovery/pricing-2/){: external} to decide which plan is best for you.

The page header shows the plan you are using today.

![Shows that the Plus plan is displayed in the page header](images/plan-in-header.png){: caption="Plus plan is displayed in the page header" caption-side="bottom"}

You cannot upgrade from any v1 plan to any v2 plan. For example, you cannot upgrade a Lite plan to a Plus, Enterprise, or Premium (v2) plan. And you cannot upgrade an Advanced, Partner, Standard, or Premium (v1) plan to an Enterprise or Premium (v2) plan. To start using v2, create a new Plus, Enterprise, or Premium plan.

For information about upgrading from a Lite to an Advanced v1 plan, see [Upgrading your service](/docs/discovery?topic=discovery-upgrading-your-plan#service){: external} in the v1 documentation.

Even though you can use the Plus plan for the first 30 days at no charge, you must have a paid account to create a Plus plan. For more information about creating a paid account, see [Upgrading your account](/docs/account?topic=account-upgrading-account){: external}.

1.  How you upgrade depends on your plan.

    -   If you decide you want to keep the Plus plan after using the 30-day free trial, no action is required.

        After 30 days of using the Plus plan at no cost, you are charged for it.

    -   If you decide you do *not* want to continue using the Plus plan, delete the Plus plan service instance before the 30-day trial period ends. You can delete the service instance from the [IBM Cloud Resource list](https://cloud.ibm.com/resources){: external}.

        The number of days that are left in your trial is displayed in the page header.

    -   To upgrade a Plus plan to an Enterprise plan, complete the following steps:

        -   Open the service page for your Plus plan service instance from the [IBM Cloud Resource list](https://cloud.ibm.com/resources){: external}.
        -   Click *Upgrade*.
        -   Choose the Enterprise plan, and then click *Save*.
        -   Give the upgrade process time to finish.
        
            The time it takes to convert the plan varies depending on the amount of data in your existing Plus plan service instance. It takes at least 20 minutes and, for instances with large amounts of data, can take more than a day to complete. The {{site.data.keyword.cloud_notm}} page does not show progress information and doesn't indicate when the plan upgrade process is finished. To check whether the new plan is in effect, you must refresh the service instance overview page, and then check for the new plan name to be displayed in the *Plan* tile.
            
            During the plan upgrade process, you can continue to submit search queries in your existing projects. However, avoid the following actions:

            -   Adding new projects or collections
            -   Deleting or changing existing collections, including adding documents, editing fields, and changing enrichment settings.

    -   If you are creating an Enterprise plan in the same data center location where you have an existing Premium plan, you must create a new resource group for the new plan. You cannot use the same resource group for Enterprise and Premium plans that are hosted in the same location. For more information, see [Managing resource groups](/docs/account?topic=account-rgs&interface=ui){: external}.
    -   You cannot do an in-place upgrade from a Plus or Enterprise plan to a Premium plan.

        A Premium plan instance must be provisioned for you. To start the process, contact [Sales](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson&disableCookie=Yes){: external}. You will be asked to provide the following details:

        -   Customer name
        -   Customer email
        -   Planned deployment date
        -   Data center location, such as Dallas or Frankfurt
        -   Account ID
        -   Resource group name
        -   Resource group ID

            The resource group is created by the account holder. For more information, see [Managing resource groups](/docs/account?topic=account-rgs&interface=ui){: external}.

You cannot directly downgrade from one plan to another. If you want to move from an Enterprise plan to a Plus plan, for example, you must provision a new Plus plan and then move data to it from your existing Enterprise plan. After the data is moved, you can delete the Enterprise plan. For more information about how to back up data that you want to move between service instances, see [High availability and disaster recovery](/docs/discovery-data?topic=discovery-data-recovery).
{: important}

For more information about plans, see [Discovery pricing plans](/docs/discovery-data?topic=discovery-data-pricing-plans).
