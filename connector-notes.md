---

copyright:
  years: 2019
lastupdated: "2020-01-06"

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

# Custom connector notes
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

  See the [Release notes](/docs/services/discovery-data?topic=discovery-data-release-notes) for possible additional issues.



