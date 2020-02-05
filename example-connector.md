---

copyright:
  years: 2019
lastupdated: "2019-11-27"

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
{:xml: .ph data-hd-programlang='xml'}
{:properties: .ph data-hd-programlang='properties'}

# Custom connector example
{: #example-connector}

The example connector is a Secure File Transfer Protocol (SFTP) connector that crawls files located on an SFTP server.
{: shortdesc}

The example connector includes three components:
  - Java source code for the connector
  - An XML definition file that defines the parameters the connector uses to connect to and crawl the data source
  - A properties file that defines optional behaviors for the connector

## Requirements
{: #example-connection-requirements}

The Java source code for the example connector has the following dependencies:

  - JDK 1.8 or higher.
  - The `custom-crawler-docs.zip` file from an installed {{site.data.keyword.discovery-data_short}} instance as described at [Downloading the `custom-crawler-docs.zip` file](#download-ccs-zip).
  - The [JSch](http://www.jcraft.com/jsch/){: external} Java package, as described [Downloaded JSch](#download-jsch). You can download the package in [ZIP format](https://sourceforge.net/projects/jsch/files/jsch/0.1.55/jsch-0.1.55.zip/download){: external} or [JAR format](https://sourceforge.net/projects/jsch/files/jsch.jar/0.1.55/jsch-0.1.55.jar/download){: external}.

### Downloading the `custom-crawler-docs.zip` file
{: #download-ccs-zip}

Perform the following steps to download the `custom-crawler-docs.zip` file to your local machine. You need root access to an installed {{site.data.keyword.discovery-data_short}} instance.

  1. Verify that you can access the installed {{site.data.keyword.discovery-data_short}} instance:
     ```sh
     ssh root@{instance_name}
     ```
     {: pre}
     where `{instance_name}` is the name of an installed {{site.data.keyword.discovery-data_short}} instance.
  1. Download the `custom-crawler-docs.zip` file to your local machine by using Secure Copy (`scp`) or a similar utility:
     ```sh
     scp root@{instance_name}:/root/bob/sdk/custom-crawler-docs.zip {local_directory}
     ```
     {: pre}
     where:
     - `{instance_name}` is the name of the installed {{site.data.keyword.discovery-data_short}} instance
     - `{local_directory}` is the directory on your local machine where you want to build and compile your custom connector
  1. Expand the `custom-crawler-docs.zip` file:
     ```sh
     cd {local_directory}
     ```
     {:pre}
     where `{local_directory}` is the directory on your local machine to which you downloaded the `custom-crawler-docs.zip` file.
   
     ```sh
     unzip custom-crawler-docs.zip
     ```
     {: pre}

     If your local machine does not have the `unzip` utility, try using the `gunzip` command instead, or see the documentation for your local machine's operating system for other alternatives to expanding ZIP files.
     {: note}

### Understanding the `custom-crawler-docs.zip` file
{: #ccs-grok-crawler-zip-file}

The `custom-crawler-docs.zip` file expands into a `custom-crawler-docs-master` directory that includes the following contents:

```
custom-crawler-docs-master/
├── README.md
├── build.gradle
├── config
│   ├── README.md
│   ├── messages.properties
│   └── template.xml
├── scripts
│   └── manage_custom_crawler.sh
├── settings.gradle
├── src
│   └── main
│       └── java
│           └── com
│               └── ibm
│                   └── es
│                       └── ama
│                           └── custom
│                               └── crawler
│                                   └── sample
│                                       └── sftp
│                                           └── SftpCrawler.java
└── wexlib
    ├── META-INF
    │   └── MANIFEST.MF
    ├── README.md
    ├── onewex-custom-crawler-{version_numbers}-javadoc.jar
    └── onewex-custom-crawler-{version_numbers}.jar

15 directories, 12 files
```
{: codeblock}

## Downloading JSch
{: #download-jsch}

JSch is a Java implementation of the Secure Shell protocol version 2 (SSH2) protocol and, by extension, `sftp`. It is derived from the [Java Cryptography Extension (JCE)](https://www.ibm.com/support/knowledgecenter/en/SSYKE2_7.0.0/com.ibm.java.security.component.70.doc/security-component/JceDocs/jce.html){: external}. You can find specifications for SSH2 at [www.openssh.com/specs.html](https://www.openssh.com/specs.html){: external}.

The current version of JSch is 0.1.55. This is the version supported by the example connector.

Download JSch to your development directory (`{local_directory}`) You can download the package in [ZIP format](https://sourceforge.net/projects/jsch/files/jsch/0.1.55/jsch-0.1.55.zip/download){: external} or [JAR format](https://sourceforge.net/projects/jsch/files/jsch.jar/0.1.55/jsch-0.1.55.jar/download){: external}. If you download the package in ZIP format, unzip it as described in the previous section.

## Files for the example connector
{: #example-files}

The example custom connector includes three files that get built together:

 - A Java source file named `SftpCrawler.java`
 - An XML definitions file named `template.xml`
 - A properties file named `message.properties`

You can locate and examine these files by referencing the directory tree listing in [Understanding the `custom-crawler-docs.zip` file](#ccs-grok-crawler-zip-file).


