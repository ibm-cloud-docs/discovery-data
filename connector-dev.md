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

# Developing custom connector code
{: #connector-dev}

The custom connector example includes a Java package named `com.ibm.es.ama.custom.crawler`. The package includes the following Java interfaces that you can use when writing your own custom connector.
{: shortdesc}

## Interfaces and JavaDoc
{: #ccs-interfaces-jdoc}

The interfaces listed in this document are available in the JAR packge file that ships with the custom connector ZIP file. After you download and expand the `custom-crawler-docs.zip` file as described in [Downloading the `custom-crawler-docs.zip` file](/docs/discovery-data?topic=discovery-data-example-connector#download-ccs-zip), the interface JAR file is available as `wexlib/onewex-custom-crawler-{version_numbers}.jar` from the top level of the expanded ZIP file. JavaDoc for the JAR file is available as `wexlib/onewex-custom-crawler-{version_numbers}-javadoc.jar` at the same level.

## Initialization interface
{: #ccs-init-interface}

### `CustomCrawler`
{: #customcrawler}

Use the `com.ibm.es.ama.custom.crawler.CustomCrawler` interface to initialize or terminate a custom crawler or to crawl documents from a path. The interface has the following methods.

|Method               |Description
|---------------------|-----------------------|
|`init`               |Initialize a custom crawler |
|`term`               |Terminate a custom crawler |
|`crawl`              |Crawl documents from a given path|

## Configuration interfaces
{: #ccs-config-interfaces}

### `CustomCrawlerConfiguration`
{: #customcrawlerconfiguration}

Use the `com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration` interface to validate the configuration and to discover available crawl spaces on the data source. The interface has the following methods.

|Method               |Description
|---------------------|-----------------------|
|`validate`           |Validate configuration |
|`getFieldsFor`       |List known fields and their types|
|`discoverySubspaces` |Discover crawl spaces on the data source|

### `ConfigProvider`
{: #configprovider}

Use the `com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration.ConfigProvider` interface to map the settings of the data source and to list the crawl-space settings on the data source. The interface has the following methods:

|Method               |Description
|---------------------|-----------------------|
|`get`                |Get a map of the settings in a section|
|`getCrawlspaceSettings` |Get a list of crawl-space settings|

### `SubspaceConsumer`
{: #subspaceconsumer}

Use the `com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration.SubspaceConsumer` interface to add a path to a crawl space. The interface has the following method:

|Method               |Description
|---------------------|-----------------------|
|`add`                |Add a path to the crawl space|

## Crawler interface
{: #ccs-crawler-interface}

### `RecordKeeper`
{: #recordkeeper}

Use the `com.ibm.es.ama.custom.crawler.CustomCrawler.RecordKeeper` interface to keep records of crawls and to publish crawled documents. The interface has the following methods:

|Method               |Description
|---------------------|-----------------------|
|`canContinue`        |Boolean that lists whether the crawler can continue. The custom crawler must poll this value periodically and terminate if it returns `false`.|
|`check`              |Get metadata fields from the last crawled document|
|`upsert`             |Publish a document for further processing |
|`delete`             |Delete a document|


## Security interface
{: #ccs-security-interface}

### `CustomCrawlerSecurityHandler`
{: #customcrawlersecurityhandler}

Use the `com.ibm.es.ama.custom.crawler.CustomCrawlerSecurityHandler` interface to implement security for your custom crawler. Note that this interface is not used in the example connector code. The interface has the following methods:

|Method               |Description
|---------------------|-----------------------|
|`term`               |Terminate a security handler |
|`getUserAndGroups`   |Get the ACLs of a given user|
|`getSecurityFilter`  |Return a customized security filter that the crawler can use to filter documents|

  This interface is not supported in the current release.
  {: note}


## For more information
{: #see-jdoc}

For detailed documentation of all of the interfaces and methods that are available in the `com.ibm.es.ama.custom.crawler` package, see the JavaDoc, which is available as indicated in [Interfaces and JavaDoc](#ccs-interfaces-jdoc).
