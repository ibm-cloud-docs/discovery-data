---

copyright:
  years: 2019, 2022
lastupdated: "2022-03-09"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Installing a custom Cloud Pak for Data connector
{: #install-connector}

After you have compiled and packaged your custom connector, you need to install it to your {{site.data.keyword.discoveryshort}} instance.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

{{site.data.keyword.discoveryshort}} provides a script named `manage_custom_crawler.sh` for installing and uninstalling custom connectors. The script is located in the `scripts` directory of the expanded `custom-crawler-docs.zip` file as described in [Understanding the `custom-crawler-docs.zip` file](/docs/discovery-data?topic=discovery-data-connector-dev#ccs-grok-crawler-zip-file).

## Installing a connector
{: #installing-connector}

You can install your custom connector to your {{site.data.keyword.discoveryshort}} instance by performing the following steps.

1.  Ensure that you have completed all steps to create a custom connector up to and including the steps listed in [Compiling and packaging the example connector](/docs/discovery-data?topic=discovery-data-assemble#compile-package-connector).

1.  Run the following command from the directory on your local machine where you created and compiled your custom connector:

    ```sh
    bash scripts/manage_custom_crawler.sh --endpoint {endpoint} --token {access token} deploy -n {crawler name} -f {built_connector_zip_file}
    ```
    {: pre}

    where you specify values for the following variables:
    
    -   endpoint: URL for your service instance. You can get this value from the *Access information* section of the service instance overview page in the {{site.data.keyword.icp4dfull_notm}} administrative console.
    -   access token: Bearer token that is required to access the endpoint. You can get this value from the same page as the endpoint.
    -   crawler name: (Optional) Name that you specified for the crawler.
    -  `{built_connector_zip_file}` is the name of the file you created in [Compiling and packaging the example connector](/docs/discovery-data?topic=discovery-data-assemble#compile-package-connector).

    For example:

    ```sh
    bash scripts/manage_custom_crawler.sh --endpoint https://mycpd.wd40.example.com/discovery/zen40-wd/instances/1638165624521059/api --token eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6ImVKcV9HY29NcHF5WUFJcVByZ0x0cERRZDNQcmRiTWo5TGg0X09WOEU4MlkifP.eyJ1aXQiOiIxMDAwMzMwOTk5IiwidXNlcm5hbWUiOiJhZG1pbiIsInJvbGUiOiJBZG1pbiIsInBlcm1pc3Npb25zIjpbImFkbWluaXN0cmF0b3IiLCJjYW5fcHJvdmlzaW9uIl0sImdyb3VwcyI6WzEwMDAwXSwic3ViIjoiYWRtaW4iLCJpc3MiOiJLTk9YU1NPIiwiYXVkIjoiRFNYIiwiaWF0IjoxNjQyNzAyMDA3fQ.5oymGw7pi6tAbTMW9rcdb62G95teR2-tKyznA_wjk_G698fbx1Zl73KZKyEWcTKtyX7IJ1Px5DPdophcqS9i3bPJowHy-ioVp6DML02mscZImhvZPra-e6gwUdhSB64KArmMClo1-kZG20EclNh6-oxR447Bjdsgp7IYpkmynmw0K6vPIqmzwEhr9gAK1vWLOoVd4EoiYNuxZaSFL5byJ0mnQxXzM14w3lKQHZ91WYVKc4JnuJiSVsdpGqVz1JNFmT8D9FBqJQ4uxtshnii0f1Yh-USKCbJmMPXicU8cDtJIfheBejwenfvejUTz5rgZgymYWrGvw3G2oOx_L1Yg-Q deploy -n awesome_crawler -f awesome_crawler.zip
    ```
    {: pre}

    Instead of specifying an access token for authentication, you can specify username and password parameters. For more information, see [Understanding the `manage_custom_crawler.sh` script](#ccs-deploy-script).

When the custom crawler is deployed, a resource ID is assigned to the connector.

## Verifying an installed connector
{: #verify-connector-install}

Verify that the connector has been deployed to the {{site.data.keyword.discoveryshort}} instance by logging into the {{site.data.keyword.discoveryshort}} tooling and ensuring that your connector is displayed as an option on the **Configure collection** page.

## Using an installed connector on {{site.data.keyword.discoveryshort}}
{: #use-installed-connector}

To use the installed custom connector, follow the steps listed in [Creating a collection](/docs/discovery-data?topic=discovery-data-collections#createcollection). The custom connector appears in the list of connectors provided at [Configuring Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types). For more information, see [Using a custom connector with the {{site.data.keyword.discoveryshort}} tooling](/docs/discovery-data?topic=discovery-data-ccs-tooling).

## Uninstalling a connector
{: #uninstall-connector}

To uninstall a custom connector from a {{site.data.keyword.discoveryshort}} instance, complete the following steps:

1.  Optional: If you don't know the resource ID, run the following command to list the custom connectors. The resource IDs of the connectors are returned.

    ```sh
    scripts/manage_custom_crawler.sh --endpoint {endpoint} --token {token} list
    ```
    {: pre}

1.  Run the following command from the directory where you extracted your custom connector ZIP file to uninstall the connector:

    ```sh
    scripts/manage_custom_crawler.sh --endpoint {endpoint} --token {token} undeploy --id {crawler_resource_id}
    ```
    {: pre}

    where `{crawler-resource-id}` is the ID that is generated for the crawler when it is deployed.

    ```sh
    scripts/manage_custom_crawler.sh --endpoint {endpoint} --token {token} undeploy --id {crawler_resource_id}
    ```
    {: pre}

Instead of specifying an access token for authentication, you can specify username and password parameters. For more information, see [Understanding the `manage_custom_crawler.sh` script](#ccs-deploy-script).

## Understanding the `manage_custom_crawler.sh` script
{: #ccs-deploy-script}

The `manage_custom_crawler.sh` script has the following internal documentation:

```text
Watson Discovery Custom Crawler Manager

This script will help you deploy, manage, and undeploy your custom crawler for
Watson Discovery.

Subcommands:
  deploy        Add a new Custom Crawler to your Watson Discovery instance.
  undeploy      Undeploy your Custom Crawler by name.
  list          List all Custom Crawlers for your Watson Discovery instance.

Options:
  -e --endpoint         The endpoint URL for your cluster and add-on service instance
                        (`https://{cpd_cluster_host}{:port}/discovery/{release}/instances/{instance_id}/api`)
  -t --token            The authorization token of your Cloud Pak instance
  -u --user             The user name of your Cloud Pak instance
  -p --password         The user password of your Cloud Pak instance
                        If the password is not specified, the command line prompts to input
  -n --name             The name of the custom crawler to upload (deploy only)
  -f --file             The path of the custom crawler package to upload (deploy only)
  -i --id               The crawler_resource_id value to delete the custom crawler (undeploy only)
  --help                Show this message.
```
{: screen}

## 4.0.5 and earlier releases only
{: #ccs-405-and-earlier}

### Installing a connector in 4.0.5 and earlier releases
{: #405-installing-connector}

You can install your custom connector to your {{site.data.keyword.discoveryshort}} instance by performing the following steps.

1.  Ensure that you have completed all steps to create a custom connector up to and including the steps listed in [Compiling and packaging the example connector](/docs/discovery-data?topic=discovery-data-assemble#compile-package-connector).

1.  Run the following command from the directory on your local machine where you created and compiled your custom connector:

    ```sh
    bash scripts/manage_custom_crawler.sh deploy -z {built_connector_zip_file}
    ```
    {: pre}

    where `{built_connector_zip_file}` is the name of the file you packaged in [Compiling and packaging the example connector](/docs/discovery-data?topic=discovery-data-assemble#compile-package-connector).

    If your {{site.data.keyword.discoveryshort}} instance is running on Red Hat OpenShift, specify the `-o` or `--openshift` parameter with the script.
    {: important}

    For example:

    ```sh
    bash scripts/manage_custom_crawler.sh deploy -z myCrawler.zip -o true
    ```
    {: pre}

### Uninstalling a connector in 4.0.5 and earlier releases
{: #405-uninstall-connector}

To uninstall a custom connector from a {{site.data.keyword.discoveryshort}} instance, run the following command at the root of the unzipped `custom-crawler-docs.zip` directory:

```sh
bash scripts/manage_custom_crawler.sh undeploy -n {built_connector_name}
```
{: pre}

where `{build_connector_name}` is the name, not the zip file, of the installed connector.

If your {{site.data.keyword.discoveryfull}} instance is running on Red Hat OpenShift, specify the `-o` or `--openshift` parameter with the script.
{: important}

```sh
bash scripts/manage_custom_crawler.sh undeploy -n {built_connector_name} -o true
```
{: pre}

### Understanding the `manage_custom_crawler.sh` script in 4.0.5 and earlier releases
{: #405-ccs-deploy-script}

The `manage_custom_crawler.sh` script has the following internal documentation:

```text
Usage: ${BASH_SOURCE[0]} [--pathToZip PATH] [--properties PROPERTIES] [--xml XML]

Watson Discovery Custom Crawler Manager

This script will help you deploy, manage, and undeploy your custom crawler for
Watson Discovery.

Subcommands:
  deploy        Add a new Custom Crawler to your Watson Discovery instance.
  properties    Generate the properties file for your crawler.
  undeploy      Undeploy your Custom Crawler by name.
  list          List all Custom Crawlers for your Watson Discovery instance.

Options:
  -d --discovery        The name of the Watson Discovery instance
  -z --zipfile          The path to the zip file to be uploaded.
                        For deploy only.
  -x --xml              The path to the XML file to be uploaded.
                        For deploy only.
  -n --name             The name of the Custom Crawler to undeploy.
  -m --messages         The path to the properties file, used when doing a two part deploy.
                        For properties only.
  -o --openshift        Set flag to true if this is an OpenShift Cluster
  --help                Show this message.
```
{: screen}
