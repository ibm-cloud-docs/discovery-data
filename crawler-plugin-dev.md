---

copyright:
  years: 2020, 2023
lastupdated: "2022-09-28"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Developing and implementing a Cloud Pak for Data custom crawler plug-in
{: #crawler-plugin-dev}

The `crawler` plug-in includes a file that is called `com.ibm.es.ama.plugin.CrawlerPlugin`. This file is the [initialization interface](/docs/discovery-data?topic=discovery-data-crawler-plugin-dev#plugin-init-interface) that has methods you can use when you work with your `crawler` plug-in.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

## Interfaces and Javadoc
{: #plugin-interfaces-jdoc}

The interface library is stored in the `lib/ama-zing-crawler-plugin-${build-version}.jar` directory of the SDK directory. The Javadoc for the JAR file is available in the `lib/ama-zing-crawler-plugin-${build-version}-javadoc.jar` file in the same directory.

## Initialization interface
{: #plugin-init-interface}

Use the `com.ibm.es.ama.plugin.CrawlerPlugin` interface to manage the `crawler` plug-in. The interface has the following methods:

| Method               | Description
|----------------------|------------------------------|
| `init`               | Start a crawler plug-in |
| `term`               | Stop a crawler plug-in  |
| `updateDocument`     | Update crawled documents     |
{: caption="Supported methods" caption-side="top"}

## Dependency management
{: #dep-mgmt}

The file `build.gradle` manages the Java dependencies.

## Crawler plug-in sample
{: #plugin-example}

A sample `crawler` plug-in is available that illustrates how to add, update, and delete metadata. The plug-in example also updates and deletes documents that are crawled by the local file system connector. The Java source code file is named `src/main/java/com/ibm/es/ama/plugin/sample/SampleCrawlerPlugin.java`.

## Logging messages
{: #logging}

The custom `crawler` plug-in supports the `java.util.logging.Logger` package for logging messages.

Any log messages that you add must meet the following requirements:

-   The log level must be `INFO` or higher.
-   The logger name must start with `com.ibm.es.ama`.

Messages are written to the log file of the `crawler` pod where the plug-in is running. A logging sample is available in the `crawler` plug-in sample.
