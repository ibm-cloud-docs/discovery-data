---

copyright:
  years: 2020, 2024
lastupdated: "2021-09-17"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Assembling and compiling a custom crawler plug-in
{: #crawler-plugin-assemble}

After you write the source code for your crawler plug-in, you must assemble and compile it.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

## Prerequisites
{: #plugin-composition-prereqs}

You must have the following items to compile a crawler plug-in:

- Java SE Development Kit 1.8 or higher
- [Gradle](https://gradle.org/install/){: external}
- cURL
- sed (stream editor)
- Crawler plug-in SDK package, see [Obtaining the crawler plug-in SDK package](/docs/discovery-data?topic=discovery-data-crawler-plugin-build#obtain-sdk)

## Assembling and compiling the crawler plug-in
{: #compile-plugin}

1. Specify the class name of the crawler plug-in by opening the `config/template.xml` file and modifying the `initial-value` of the `crawler_plugin_class` element.
1. Ensure that you are in the crawler plug-in SDK directory on your development server.
1. Enter `gradle packageCrawlerPlugin` to use Gradle to compile your Java source code and to create a compressed file that includes all of the required components for the crawler plug-in.
1. Confirm that you have access to the crawler plug-in package, which is in the `build/distributions/wd-crawler-plugin-sample.zip` file.
