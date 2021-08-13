---

copyright:
  years: 2019, 2021
lastupdated: "2021-08-13"

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

# Building a Cloud Pak for Data custom connector
{: #build-connector}

{{site.data.keyword.discoveryshort}} provides connectors to many popular data sources, as described in [Configuring Cloud Pak for Data data sources](/docs/discovery-data?topic=discovery-data-collection-types). If you need to connect to a different data source, you can write and deploy a *custom connector*. 
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{:note}

Any custom code that is used with {{site.data.keyword.discoveryfull}} is the responsibility of the developer and is not covered by IBM support.
{: note}

Example code and configuration files for a basic custom connector are included.

Related topics:

- [Developing custom Cloud Pak for Data connector code](/docs/discovery-data?topic=discovery-data-connector-dev)
- [Assembling, compiling, and packaging a custom Cloud Pak for Data connector](/docs/discovery-data?topic=discovery-data-assemble)
- [Installing and uninstalling a custom Cloud Pak for Data connector](/docs/discovery-data?topic=discovery-data-install-connector)
- [Using a custom Cloud Pak for Data connector from the Discovery user interface](/docs/discovery-data?topic=discovery-data-ccs-tooling)

## Custom connector requirements
{: #about-ccs}

A custom connector is a component that uses the SDK and crawler framework that is documented here to connect to and crawl a specific data source. Custom connectors have the same general requirements as provided connectors. For more information, see [Data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements).

Before you implement a custom connector, you need to know the following information about the data source:

- The data source's network location (server name or address, including port, or URL, including port)
- The data source's authentication method and security credentials
- The path or paths on the data source that the connector needs to crawl
- The connection method or protocol that the data source supports

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

These capabilities can be implemented by using the interfaces and methods that are described in [Developing custom connector code](/docs/discovery-data?topic=discovery-data-connector-dev).

## Custom connector limitations
{: #connector-notes}

Observe the following notes and warnings when you implement a custom connector.
{:shortdesc}

- Custom connectors do *not* support the following features:

  - Synchronization settings
  - Filtering documents based on user access at query time. (At crawl and index time, only documents that the current user has the right to access are returned.)
  - The `required` and `hidden` validation settings. They are ignored when the connector is displayed in {{site.data.keyword.discoveryshort}}
  - The use of `<condition />` tags in the definition file. These tags are currently ignored.
- When you use the example connector code in the current release, {{site.data.keyword.discoveryshort}} does not collapse and group authentication settings for the custom connector's properties. For example, if the `{connector_name}_DATASOURCE_SETTINGS_USE_KEY_LABEL` toggle is set to `Off`, the user interface shows the fields for `{connector_name}_DATASOURCE_SETTINGS_KEY_LABEL` and `{connector_name}_DATATSOURCE_SETTINGS_PASSPHRASE_LABEL` anyhow.
- The `list` parameter type is not supported.
- If a custom connector fails to connect to its source for any reason, it issues a generic error message such as `Failed to create connector` or `Timed out`, or a `500` HTTP error. Specific failure information is not currently provided.

  See the [Release notes](/docs/discovery-data?topic=discovery-data-release-notes) for more possible issues.
