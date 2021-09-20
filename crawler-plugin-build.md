---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-17"

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

# Building a Cloud Pak for Data custom crawler plug-in
{: #crawler-plugin-build}

{{site.data.keyword.discoveryshort}} features the option to build your own crawler plug-in with a Java SDK. By using crawler plug-ins, you can now quickly develop relevant solutions for your use cases. You can download the SDK from your installed {{site.data.keyword.discoveryshort}} cluster. For more information, see [Obtaining the crawler plug-in SDK package](/docs/discovery-data?topic=discovery-data-crawler-plugin-build#obtain-sdk).
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{:note}

Any custom code that you use with {{site.data.keyword.discoveryfull}} is the responsibility of the developer; IBM Support does not cover any custom code that the developer creates.
{: note}

The crawler plug-ins support the following functions:

- Update the metadata list of a crawled document
- Update the content of a crawled document
- Exclude a crawled document
- Reference crawler configurations, masking password values
- Show notice messages in the {{site.data.keyword.discoveryshort}} user interface
- Output log messages to the crawler pod console

However, the crawler plug-ins cannot support the following functions:

- Split a crawled document into multiple documents
- Combine content from multiple documents into a single document
- Modify access control lists

## Crawler plug-in requirements
{: #plugin-reqs}

Make sure that the following items are installed on the development server that you plan to use to develop a crawler plug-in by using this SDK:

- Java SE Development Kit (JDK) 1.8 or higher
- [Gradle](https://gradle.org/install/){: external}
- cURL
- sed (stream editor)

## Obtaining the crawler plug-in SDK package
{: #obtain-sdk}

1. Log in to your {{site.data.keyword.discoveryshort}} cluster.
1. Enter the following command to obtain your crawler pod name:

   ```curl
   oc get pods | grep crawler
   ```
   {: pre}

   The following example shows sample output.

   ```curl
   wd-discovery-crawler-57985fc5cf-rxk89     1/1     Running     0          85m
   ```
   {: codeblock}

1. Enter the following command to obtain the SDK package name, replacing `{crawler-pod-name}` with the crawler pod name that you obtained in step 2:

   ```curl
   oc exec {crawler-pod-name} -- ls -l /opt/ibm/wex/zing/resources/ | grep wd-crawler-plugin-sdk
   ```
   {: pre}

   The following example shows sample output.

   ```curl
   -rw-r--r--. 1 dadmin dadmin 35575 Oct  1 16:51 wd-crawler-plugin-sdk-${build-version}.zip
   ```
   {: codeblock}

1. Enter the following command to copy the SDK package to the host server, replacing `{build-version}` with the build version number from the previous step:

   ```curl
   oc cp {crawler-pod-name}:/opt/ibm/wex/zing/resources/wd-crawler-plugin-sdk-${build-version}.zip wd-crawler-plugin-sdk.zip
   ```
   {: pre}

1. If necessary, copy the SDK package to the development server.

## Building a crawler plug-in package
{: #build-plugin-pkg}

1. Extract the SDK compressed file.
1. Implement the plug-in logic in `src/`. Ensure that the dependency is written in `build.gradle`.
1. Enter `gradle packageCrawlerPlugin` to create the plug-in package. The package is generated as `build/distributed/wd-crawler-plugin-sample.zip`.
