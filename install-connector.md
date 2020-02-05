---

copyright:
  years: 2019
lastupdated: "2019-12-18"

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

# Installing and uninstalling a custom connector
{: #install-connector}

After you have compiled and packaged your custom connector, you need to install it to your {{site.data.keyword.discovery-data_short}} instance.
{: shortdesc}

{{site.data.keyword.discovery-data_short}} provides a script named `manage_custom_crawler.sh` for installing and uninstalling custom connectors. The script is located in the `scripts` directory of the expanded `custom-crawler-docs.zip` file as described in [Understanding the `custom-crawler-docs.zip` file](/docs/discovery-data?topic=discovery-data-example-connector#ccs-grok-crawler-zip-file).

## Installing a connector
{: #install-connector}

You can install your custom connector to your {{site.data.keyword.discovery-data_short}} instance by performing the following steps.

  1. Ensure that you have completed all steps to create a custom connector up to and including the steps listed in [Compiling and packaging the example connector](/docs/discovery-data?topic=discovery-data-compile-package-connector).
    
  1. Run the following command from the directory on your local machine where you created and compiled your custom connector:
     ```sh
     bash scripts/manage_custom_crawler.sh deploy -z {built_connector_zip_file}
     ```
     {: pre}
    where `{built_connector_zip_file}` is the name of the file you packaged in [Compiling and packaging the example connector](/docs/discovery-data?topic=discovery-data-compile-package-connector).

    **Important**: If your {{site.data.keyword.discovery-data_short}} instance is running on Red Hat OpenShift, specify the `-o` or `--openshift` parameter with the script:
      ```sh
      bash scripts/manage_custom_crawler.sh deploy -z {built_connector_zip_file} -o true
      ```
      {: pre}

## Verifying an installed connector
{: #verify-connector-install}

Verify that the connector has been deployed to the {{site.data.keyword.discovery-data_short}} instance by logging into the {{site.data.keyword.discovery-data_short}} tooling and ensuring that an icon for the connector is displayed on the **Configure collection** page.

## Using an installed connector on {{site.data.keyword.discovery-data_short}}
{: #use-installed-connector}

To use the installed custom connector, follow the steps listed in [Creating a collection](/docs/discovery-data?topic=discovery-data-collections#createcollection). The custom connector appears in the list of connectors provided at [Configuring data sources](/docs/discovery-data?topic=discovery-data-collections#collection-types). For further information, see [Using a custom connector with the {{site.data.keyword.discovery-data_short}} tooling](/docs/discovery-data?topic=discovery-data-ccs-tooling).

## Uninstalling a connector
{: #uninstall-connector}

To uninstall a custom connector from a {{site.data.keyword.discovery-data_short}} instance, run the following command at the root of the unzipped `custom-crawler-docs.zip` directory:

```sh
bash scripts/manage_custom_crawler.sh undeploy -n {built_connector_name}
```
{: pre}
where `{build_connector_name}` is the name, not the zip file, of the installed connector.

**Important**: If your {{site.data.keyword.discovery-data_long}} instance is running on Red Hat OpenShift, specify the `-o` or `--openshift` parameter with the script:
```sh
bash scripts/manage_custom_crawler.sh undeploy -n {built_connector_name} -o true
```
{: pre}

## Understanding the `manage_custom_crawler.sh` script
{: #ccs-deploy-script}

The `manage_custom_crawler.sh` script has the following internal documentation:

```
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



