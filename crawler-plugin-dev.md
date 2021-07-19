---

copyright:
  years: 2020, 2021
lastupdated: "2021-07-19"

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

# Developing and implementing a Cloud Pak for Data custom crawler plug-in
{: #crawler-plugin-dev}

The crawler plug-in includes a file that is called `com.ibm.es.ama.plugin.CrawlerPlugin`. This file is the [Initialization interface](/docs/discovery-data?topic=discovery-data-crawler-plugin-dev#plugin-init-interface) that includes methods that you can use when you work with your crawler plug-in.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{:note}

## Interfaces and Javadoc
{: #plugin-interfaces-jdoc}

The interface library is available as `lib/ama-zing-crawler-plugin-${build-version}.jar` in the SDK directory. The Javadoc for the .jar file is available as `lib/ama-zing-crawler-plugin-${build-version}-javadoc.jar` in the same directory.

## Initialization interface
{: #plugin-init-interface}

Use the `com.ibm.es.ama.plugin.CrawlerPlugin` interface to start or stop a crawler plug-in or to update the crawled documents. The interface has the following methods:

| Method               | Description
|----------------------|------------------------------|
| `init`               | Start a crawler plug-in |
| `term`               | Stop a crawler plug-in  |
| `updateDocument`     | Update crawled documents     |
{: caption="Supported methods" caption-side="top"}

## Dependency management
{: #dep-mgmt}

The file `build.gradle` manages the Java dependency.

## Crawler plug-in example
{: #plugin-example}

The example crawler plug-in `src/main/java/com/ibm/es/ama/plugin/sample/SampleCrawlerPlugin.java` adds, updates, and deletes metadata. The plug-in example also updates and deletes the content of documents that the local file system connector crawls.
