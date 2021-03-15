---

copyright:
  years: 2020, 2021
lastupdated: "2021-03-12"

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

# Assembling and compiling a custom crawler plug-in
{: #crawler-plugin-assemble}

After you write the source code for your crawler plug-in, you must assemble and compile it.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{:note}

## Prerequisites
{: #plugin-composition-prereqs}

You must have the following items to compile a crawler plug-in:

- JDK 1.8 or higher
- [Gradle](https://gradle.org/install/){: external}
- curl
- sed
- The SDK package, see [Obtaining the crawler plug-in SDK package](/docs/discovery-data?topic=discovery-data-crawler-plugin-build#obtain-sdk)

## Assembling and compiling the crawler plug-in
{: #compile-plugin}

1. Specify the class name of the crawler plug-in by opening the `config/template.xml` file and modifying the `initial-value` of the `crawler_plugin_class` element.
1. Ensure that you are in the crawler plug-in SDK directory on your development server.
1. Enter `gradle packageCrawlerPlugin` to use Gradle to compile your Java source code and to create a .zip file that includes all of the required components for the crawler plug-in.
1. Confirm that you have access to the crawler plug-in package, which is in the `build/distributions/wd-crawler-plugin-sample.zip` file.
