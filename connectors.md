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

# Building and implementing a custom connector
{: #build-connector}

{{site.data.keyword.discovery-data_short}} provides connectors to many popular data sources, as described in [Configuring data sources](/docs/discovery-data?topic=discovery-data-collections#collection-types). If you need to connect to a different data source, you can write and deploy a _custom connector_. 
{: shortdesc}

You can use the following information as guidance for writing and deploying a custom connector. The information also includes example code and configuration files for a basic connector.

## Custom connector requirements
{: #about-ccs}

A custom connector is a component that uses the SDK and crawler framework documented here to connect to and crawl a specific data source. Custom connectors have the same general requirements as provided connectors. For more information, see [Connector and file type requirements](/docs/discovery-data?topic=discovery-data-collections#connectorrequirements).

When preparing to implement a custom connector, you need to have information about the following items:

  - The data source, including:
    - The data source's network location (server name or address including port, or URL including port)
    - The data source's authentication method and security credentials
    - The path or paths on the data source that the connector needs to crawl
    - The connection method or protocol that the data source supports
  - The schedule on which the connector needs to run (**Note:** Not supported in the current release)

## Designing a custom connector
{: #design-connector}

A custom connector needs the following capabilities:

  - Configuring a crawler.
    - Configuring all settings that are required to connect to the data source.
    - Discovering a _crawl space_ on the data source. At least one crawl space is required.
  - Crawling documents.
    - Crawling the documents on each data set.
    - Adding Access Control List (ACL) information to each document.
  - Retrieving ACL information for the username that authenticates to the data source.
  - Filtering documents for each user. **Note**: The example connector code does not implement document filtering.

These capabilities can be implemented by using the interfaces and methods described in [Developing custom connector code](/docs/discovery-data?topic=discovery-data-connector-dev).

## Custom connector notes
{: #connector-notes}

Observe the following notes and warnings when implementing a custom connector.
{:shortdesc}

  - Custom connectors do _not_ support the following documented features in the current release:
    - Crawl schedule settings
    - Synchronization settings
    - The `required` and `hidden` validation settings when the configuration is displayed in the {{site.data.keyword.discovery-data_short}} tooling
    - The **More processing settings** menu to perform actions such as enabling OCR
    - Document-level security
    - The use of `<condition />` tags in the definition file. These tags are currently ignored.
  - When you use the example connector code in the current release, the {{site.data.keyword.discovery-data_short}} tooling does not collapse and group authentication settings for the custom connector's properties. For example, if the `{connector_name}_DATASOURCE_SETTINGS_USE_KEY_LABEL` toggle is set to `Off`, the tooling still displays the fields for `{connector_name}_DATASOURCE_SETTINGS_KEY_LABEL` and `{connector_name}_DATATSOURCE_SETTINGS_PASSPHRASE_LABEL` even though they are not applicable with the toggle setting.
  - The `list` parameter type is not supported in the {{site.data.keyword.discovery-data_short}} tooling.
  - If a custom connector fails to connect to its source for any reason, it issues a generic error message such as `Failed to create connector` or `Timed out`, or a `500` HTTP error. Specific failure information is not currently provided.
  - If a custom connector is deployed and creates hidden files, undeployment takes a considerable length of time (several minutes up to several hours in extreme cases) while the script locates all of the connector's components.

  See the [Release notes](/docs/discovery-data?topic=discovery-data-release-notes) for possible additional issues.
