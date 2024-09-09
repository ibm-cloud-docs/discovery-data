---

copyright:
  years: 2020, 2024
lastupdated: "2021-10-06"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Managing custom crawler plug-ins on your Watson Discovery cluster
{: #manage-plugin}

You can use the `scripts/manage_crawler_plugin.sh` script to perform common plug-in management actions. The `scripts/manage_crawler_plugin.sh` script is located in the [crawler plug-in SDK package](/docs/discovery-data?topic=discovery-data-crawler-plugin-build#obtain-sdk). When you use the script in a command, you must have the endpoint URL of your {{site.data.keyword.discoveryshort}} cluster and the username and password of your {{site.data.keyword.cpd_full}} instance.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

## Commands and options for managing your crawler plug-ins
{: #mng-plugin-cmd-opt}

You can enter `scripts/manage_crawler_plugin.sh --help` to view the following help messages in the script:

```sh
Usage: scripts/manage_crawler_plugin.sh --endpoint endpoint --user username [--password password] command

Watson Discovery Crawler Plug-in Manager

This script will help you deploy, undeploy, and list your crawler plug-ins for Watson Discovery.

Commands:
deploy        Add a new crawler plug-in to your Watson Discovery instance
undeploy      Undeploy your crawler plug-in by ID
list          List all crawler plug-ins for your Watson Discovery instance (default)

Options:
-e --endpoint         The endpoint URL for your cluster and add-on service instance
                      (https://{cpd_cluster_host}{: port}/discovery/{release}/instances/{instance_id}/api)
-u --user             The user name of your Cloud Pak instance
-p --password         The user password of your Cloud Pak instance
                      If the password is not specified, the command line prompts to input
-n --name             The name of the crawler plug-in to upload (deploy only)
-f --file             The path of the crawler plug-in package to upload (deploy only)
--id                  The crawler_resource_id value to delete the crawler plug-in (undeploy only)
--help                Show this message
```
{: codeblock}

You can use the following commands to deploy, undeploy, and list your crawler plug-ins. Replace the variable references `{variable}` with the required information:

- Deploy crawler plug-in: `scripts/manage_crawler_plugin.sh --endpoint {endpoint_URL} --user {username} deploy --name {plugin_name}`
- Undeploy crawler plug-in: `scripts/manage_crawler_plugin.sh --endpoint {endpoint_URL} --user {username} undeploy --id {crawler_resource_id}`
- List deployed crawler plug-in: `scripts/manage_crawler_plugin.sh --endpoint {endpoint_URL} --user {username} list`

After you use the `scripts/manage_crawler_plugin.sh` script to deploy a crawler plug-in, you can select the plug-in in the {{site.data.keyword.discoveryshort}} tooling when you create a collection. For more information about the crawler plug-in settings in {{site.data.keyword.discoveryshort}}, see [Crawler plug-in settings](/docs/discovery-data?topic=discovery-data-collection-types#plugin-settings).
