---

copyright:
  years: 2020, 2025
lastupdated: "2025-06-25"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

In an upcoming release, the bundled JVM for the crawler plug-in and customer connector features will be transitioned to IBM Semeru Runtimes, Version 21. If your crawler plug-in or custom connectors utilize any features that are incompatible between IBM SDK, Java Technology Edition, Version 8 and IBM Semeru Runtimes, Version 21, you need to revise your code to ensure compatibility with future releases, such as Discovery 5.2.x and later.
{: note}

For JVM migration, see the following pages:
* https://www.ibm.com/support/pages/semeru-runtimes-migration-guide
* https://www.ibm.com/support/pages/semeru-runtimes-security-migration-guide

# Building a custom crawler plug-in
{: #crawler-plugin-build}

{{site.data.keyword.discoveryshort}} features the option to build your own crawler plug-in with a Java SDK. By using crawler plug-ins, you can now quickly develop relevant solutions for your use cases. You can download the SDK from your installed {{site.data.keyword.discoveryshort}} cluster. For more information, see [Obtaining the crawler plug-in SDK package](/docs/discovery-data?topic=discovery-data-crawler-plugin-build#obtain-sdk).
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} [IBM Software Hub]{: tag-teal}

This information applies only to installed deployments.
{: note}

Any custom code that you use with {{site.data.keyword.discoveryfull}} is the responsibility of the developer; IBM Support does not cover any custom code that the developer creates.
{: note}

The crawler plug-ins support the following functions:

- Update the metadata list of a crawled document
- Update the content of a crawled document
- Exclude a crawled document
- Reference crawler configurations, masking password values
- Show notice messages in the {{site.data.keyword.discoveryshort}} user interface
- Output log messages to the `crawler` pod console

However, the `crawler` plug-ins cannot support the following functions:

- Split a crawled document into multiple documents
- Combine content from multiple documents into a single document
- Modify access control lists

## Crawler plug-in requirements
{: #plugin-reqs}

Make sure that the following items are installed on the development server that you plan to use to develop a `crawler` plug-in by using this SDK:

- Java SE Development Kit (JDK) 1.8 or higher
- [Gradle](https://gradle.org/install/){: external}
- cURL
- sed (stream editor)

## Obtaining the crawler plug-in SDK package
{: #obtain-sdk}

1. Log in to your {{site.data.keyword.discoveryshort}} cluster.
1. Enter the following command to obtain your `crawler` pod name:

   ```sh
   oc get pods | grep crawler
   ```
   {: pre}

   The following example shows sample output.

   ```sh
   wd-discovery-crawler-57985fc5cf-rxk89     1/1     Running     0          85m
   ```
   {: codeblock}

1. Enter the following command to obtain the SDK package name, replacing `{crawler-pod-name}` with the `crawler` pod name that you obtained in step 2:

   ```sh
   oc exec {crawler-pod-name} -- ls -l /opt/ibm/wex/zing/resources/ | grep wd-crawler-plugin-sdk
   ```
   {: pre}

   The following example shows sample output.

   ```sh
   -rw-r--r--. 1 dadmin dadmin 35575 Oct  1 16:51 wd-crawler-plugin-sdk-${build-version}.zip
   ```
   {: codeblock}

1. Enter the following command to copy the SDK package to the host server, replacing `{build-version}` with the build version number from the previous step:

   ```sh
   oc cp {crawler-pod-name}:/opt/ibm/wex/zing/resources/wd-crawler-plugin-sdk-${build-version}.zip wd-crawler-plugin-sdk.zip
   ```
   {: pre}

1. If necessary, copy the SDK package to the development server.

## Building a crawler plug-in package
{: #build-plugin-pkg}

1. Extract the SDK compressed file.
1. Implement the plug-in logic in `src/`. Ensure that the dependency is written in `build.gradle`.
1. Enter `gradle packageCrawlerPlugin` to create the plug-in package. The package is generated as `build/distributed/wd-crawler-plugin-sample.zip`.
