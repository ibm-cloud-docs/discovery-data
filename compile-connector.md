---

copyright:
  years: 2019, 2020
lastupdated: "2020-05-13"

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
{:xml: .ph data-hd-programlang='xml'}
{:properties: .ph data-hd-programlang='properties'}

# Compiling and packaging the example connector
{: #compile-package-connector}

After you write the source code and configuration files for your custom connector, you need to compile and package it.
{: shortdesc}

## Prerequisites
{: #ccs-compilation-prereqs}

To compile a custom connector, you need to have the following items on your local machine. For more information, see [Custom connector example](/docs/discovery-data?topic=discovery-data-example-connector#example-connection-requirements).

  - JDK 1.8 or higher
  - [Gradle](https://gradle.org/install/){: external}
  - The `custom-crawler-docs.zip` file from an installed {{site.data.keyword.discovery-data_short}} instance
  - The JSch package
  - The following files for the example custom connector:
    - Java source code (`SftpCrawler.java`)
    - XML definition file (`template.xml`)
    - Properties file (`messages.properties`)

  Do not change the names or paths of the `SftpCrawler.java`, `template.xml`, and `messages.properties` files. Doing so can result in problems including build failures.
  {: important}

## Compiling and packaging the source code
{: #compile-connector}

  1. Ensure you are in the custom connector development directory on your local machine:
     ```sh
     cd {local_directory}
     ```
     {: pre}

  1. Use Gradle to compile your Java source code and to create a ZIP file that includes all of the required components for the custom connector:
    ```sh
    gradle build packageCustomCrawler
    ```
    {: pre}

  Gradle creates a file in `{local_directory}/build/distributions/{built_connector_zip_file}`, where the name of the `{built_connector_zip_file}` is based on the value of `initial-value` in line 7 of the `template.xml` definitions file. For example, if the line reads as follows, Gradle outputs a file named `{local_directory}/build/distributions/my-sftp-connector.zip`.

  ```xml
 <declare type="string" name="crawler_name" initial-value="my-sftp-connector"/>
  ```

## Next step
{: #compile-next-step}

Proceed to [Installing and uninstalling a custom connector](/docs/discovery-data?topic=discovery-data-install-connector) to install the custom connector to your {{site.data.keyword.discovery-data_short}} instance.