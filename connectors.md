---

copyright:
  years: 2019
lastupdated: "2019-12-02"

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
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Building and implementing a custom connector
{: #build-connector}

{{site.data.keyword.discovery-data_short}} provides connectors to many popular data sources, as described in [Configuring data sources](/docs/services/discovery-data?topic=discovery-data-collection-types#collection-types). If you need to connect to a different data source, you can write and deploy a _custom connector_. 
{: shortdesc}

This document provides information about writing and deploying a custom connector, including example code and configuration files for a basic connector.

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
