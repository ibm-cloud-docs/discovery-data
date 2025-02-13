---

copyright:
  years: 2019, 2025
lastupdated: "2025-02-13"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Developing custom Cloud Pak for Data connector code
{: #connector-dev}

The custom connector example includes a Java package named `com.ibm.es.ama.custom.crawler`. The package includes the following Java interfaces that you can use when you write your own custom connector.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} [IBM Software Hub]{: tag-teal}

This information applies only to installed deployments.
{: note}

## Interfaces and Javadoc
{: #ccs-interfaces-jdoc}

The interfaces that are listed in this document are available in the JAR package file that is included with the custom connector compressed file. After you download and expand the `custom-crawler-docs.zip` file as described in [Downloading the `custom-crawler-docs.zip` file in Discovery 2.2.1 and later](#download-ccs-zip) and [Downloading the `custom-crawler-docs.zip` file in Discovery 2.2.0 and earlier](#download-ccs-zip-old), the interface JAR file is available as `wexlib/ama-zing-custom-crawler-{version_numbers}.jar` from the root level of the expanded compressed file. Javadoc for the JAR file is available as `wexlib/ama-zing-custom-crawler-{version_numbers}-javadoc.jar` at the same level.

## Initialization interface
{: #ccs-init-interface}

### `CustomCrawler`
{: #customcrawler}

Use the `com.ibm.es.ama.custom.crawler.CustomCrawler` interface to start or stop a custom crawler or to crawl documents from a path. The interface has the following methods.

|Method               |Description
|---------------------|-----------------------|
|`init`               | Start a custom crawler |
|`term`               | Stop a custom crawler |
|`crawl`              | Crawl documents from a specified path|
{: caption="CustomCrawler methods" caption-side="top"}

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
{: caption="CustomCrawlerConfiguration methods" caption-side="top"}

### `ConfigProvider`
{: #configprovider}

Use the `com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration.ConfigProvider` interface to map the settings of the data source and to list the crawl-space settings on the data source. The interface has the following methods:

|Method               |Description
|---------------------|-----------------------|
|`get`                |Get a map of the settings in a section|
|`getCrawlspaceSettings` |Get a list of crawl-space settings|
{: caption="ConfigProvider methods" caption-side="top"}

### `SubspaceConsumer`
{: #subspaceconsumer}

Use the `com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration.SubspaceConsumer` interface to add a path to a crawl space. The interface has the following method:

|Method               |Description
|---------------------|-----------------------|
|`add`                |Add a path to the crawl space|
{: caption="SubspaceConsumer methods" caption-side="top"}

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
{: caption="RecordKeeper methods" caption-side="top"}

## Security interface
{: #ccs-security-interface}

### `CustomCrawlerSecurityHandler`
{: #customcrawlersecurityhandler}

Use the `com.ibm.es.ama.custom.crawler.CustomCrawlerSecurityHandler` interface to implement security for your custom crawler. The interface has the following methods:

|Method               |Description
|---------------------|-----------------------|
|`term`               |Terminate a security handler |
|`getUserAndGroups`   |Get the ACLs of a given user|
{: caption="CustomCrawlerSecurityHandler methods" caption-side="top"}

When the `getUserAndGroups` logic of a connector is updated, it can take up to 10 minutes after the connector is redeployed for the change to take effect.
{: important}

## Custom connector example
{: #example-connector}

The example connector is a Secure File Transfer Protocol (SFTP) connector that crawls files that are located on an SFTP server.
{: shortdesc}

The example connector includes three components:

- Java source code for the connector
- An XML definition file that defines the parameters that the connector uses to connect to and crawl the data source
- A properties file that defines optional behaviors for the connector

### Requirements
{: #example-connection-requirements}

The Java source code for the example connector has the following dependencies:

- Java SE Development Kit (JDK) 1.8 or higher.
- The `custom-crawler-docs.zip` file from an installed {{site.data.keyword.discoveryshort}} instance as described at [Downloading the `custom-crawler-docs.zip` file in Discovery 2.2.1 and later](#download-ccs-zip) and [Downloading the `custom-crawler-docs.zip` file in Discovery 2.2.0 and earlier](#download-ccs-zip-old).
- The [JSch](http://www.jcraft.com/jsch/){: external} Java package, as described [Downloaded JSch](#download-jsch). You can download the package in [ZIP format](https://sourceforge.net/projects/jsch/files/jsch/0.1.55/jsch-0.1.55.zip/download){: external} or [JAR format](https://sourceforge.net/projects/jsch/files/jsch.jar/0.1.55/jsch-0.1.55.jar/download){: external}.

#### Downloading the `custom-crawler-docs.zip` file in Discovery 2.2.1 and later
{: #download-ccs-zip}

In {{site.data.keyword.discoveryshort}} version 2.2.1 and later, perform the following steps to download the `custom-crawler-docs.zip` file to your local machine. You need root access to an installed {{site.data.keyword.discoveryshort}} instance:

1.  Log in to your {{site.data.keyword.discoveryshort}} cluster.

1.  Enter the following command to obtain your `crawler` pod name:

     ```sh
     oc get pods | grep crawler
     ```
     {: pre}

     You might see output that looks like this:

     ```text
     wd-discovery-crawler-57985fc5cf-rxk89     1/1     Running     0          85m
     ```
     {: codeblock}

1.  Enter the following command to obtain the `custom-crawler-docs.zip` file, replacing `{crawler-pod-name}` with the `crawler` pod name that you obtained in step 2:

     ```sh
     oc exec {crawler-pod-name} -- ls -l /opt/ibm/wex/zing/resources/ \
     | grep custom-crawler-docs
     ```
     {: pre}

     You might see output that is similar to the following:

     ```text
     -rw-r--r--. 1 dadmin dadmin 59451 Jan 19 03:50 custom-crawler-docs-${build-version}.zip
     ```
     {: codeblock}

1.  Enter the following command to copy the `custom-crawler-docs.zip` file to the host server, replacing `{build-version}` with the build version number in step 3:

     ```sh
     oc cp {crawler-pod-name}:/opt/ibm/wex/zing/resources/custom-crawler-docs-${build-version}.zip custom-crawler-docs.zip
     ```
     {: pre}

1.  Enter the following command to expand the `custom-crawler-docs.zip` file:

     ```sh
     unzip custom-crawler-docs.zip -d custom-crawler-docs-primary
     ```
     {: pre}

     If necessary, copy the `custom-crawler-docs.zip` file to the development server.
     {: note}

     If your local machine does not have the `unzip` utility, try using the `gunzip` command instead, or see the documentation of the operating system of your local machine for other alternatives to expand compressed files.
     {: note}

     If you are using a version of {{site.data.keyword.discoveryshort}} that is earlier than 2.1.2 and you want to access the `custom-crawler-docs.zip` file, enter the following command: `scp root@{instance_name}:/root/bob/sdk/custom-crawler-docs.zip {local_directory}`.
     {: tip}

For information about downloading the `custom-crawler-docs.zip` file to {{site.data.keyword.discoveryshort}} 2.2.0 and earlier, see [Downloading the custom-crawler-docs.zip file to Discovery 2.2.0 and earlier](#download-ccs-zip-old).

##### Downloading the `custom-crawler-docs.zip` file to Discovery 2.2.0 and earlier
{: #download-ccs-zip-old}

In {{site.data.keyword.discoveryshort}} version 2.2.0 and earlier, perform the following steps to download the `custom-crawler-docs.zip` file to your local machine. You need root access to an installed {{site.data.keyword.discoveryshort}} instance:

1. Obtain the entitlement key by navigating to your [container software library](https://myibm.ibm.com/products-services/containerlibrary){: external}.

1. Enter the following command to log in to the Docker registry where your {{site.data.keyword.discoveryshort}} images are available. Include your entitlement key in the following command:

   ```sh
   docker login cp.icr.io -u cp -p {entitlement_key}
   ```
   {: pre}

1. Enter the following command to pull the `custom-crawler-sdk` image:

   ```sh
   docker pull cp.icr.io/cp/watson-discovery/custom-crawler-sdk:2.1.3
   ```
   {: pre}

1. Enter the following command to run the `custom-crawler-sdk` image:

   ```sh
   docker run cp.icr.io/cp/watson-discovery/custom-crawler-sdk:2.1.3
   ```
   {: pre}

1. Enter the following command to copy `custom-crawler-docs.zip` from the container where the image is running:

   ```sh
   docker cp {container_name}:/crawler/custom-crawler-docs.zip .
   ```
   {: pre}

   To find the image, enter `docker ps -a | grep custom-crawler-sdk`.

1. Expand the `custom-crawler-docs.zip` file:

   ```sh
   cd {local_directory}
   ```
   {: pre}

    where `{local_directory}` is the directory on your local machine to which you downloaded the `custom-crawler-docs.zip` file.

    ```sh
    unzip custom-crawler-docs.zip
    ```
    {: pre}

    If your local machine does not have the `unzip` utility, try using the `gunzip` command instead, or see the documentation of the operating system of your local machine for other alternatives to expand compressed files.
    {: note}

    If you are using a version of {{site.data.keyword.discoveryshort}} that is earlier than 2.1.2 and you want to access the `custom-crawler-docs.zip` file, enter the following command: `scp root@{instance_name}:/root/bob/sdk/custom-crawler-docs.zip {local_directory}`.
    {: tip}

For information about downloading the `custom-crawler-docs.zip` file on {{site.data.keyword.discoveryshort}} version 2.2.1 and later, see [Downloading the `custom-crawler-docs.zip` file in Discovery 2.2.1 and later](#download-ccs-zip).

#### Understanding the `custom-crawler-docs.zip` file
{: #ccs-grok-crawler-zip-file}

The `custom-crawler-docs.zip` file expands into a directory named `custom-crawler-docs-primary` that includes the following contents:

```text
custom-crawler-docs-primary
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
|                                           └── SftpSecurityHandler.java
└── wexlib
    ├── META-INF
    │   └── MANIFEST.MF
    ├── README.md
    ├── ama-zing-custom-crawler-{version_numbers}-javadoc.jar
    └── ama-zing-custom-crawler-{version_numbers}.jar

15 directories, 12 files
```
{: codeblock}

### Downloading JSch
{: #download-jsch}

JSch is a Java implementation of the Secure Shell protocol version 2 (SSH2) protocol and, by extension, `sftp`. It is derived from the [Java Cryptography Extension (JCE)](https://www.ibm.com/support/knowledgecenter/en/SSYKE2_7.0.0/com.ibm.java.security.component.70.doc/security-component/JceDocs/jce.html){: external}. You can find specifications for SSH2 at [www.openssh.com/specs.html](https://www.openssh.com/specs.html){: external}.

The current version of JSch is 0.1.55 and is supported by the example connector.

Download JSch to your development directory (`{local_directory}`). You can download the package in [ZIP format](https://sourceforge.net/projects/jsch/files/jsch/0.1.55/jsch-0.1.55.zip/download){: external} or [JAR format](https://sourceforge.net/projects/jsch/files/jsch.jar/0.1.55/jsch-0.1.55.jar/download){: external}. If you download the package in .zip format, extract it as described in the previous section.

### Files for the example connector
{: #example-files}

The example custom connector includes three files that get built together:

- Java source files that are named `SftpCrawler.java` and `SftpSecurityHandler.java`
- An XML definitions file named `template.xml`
- A properties file named `message.properties`

You can locate and examine these files by referencing the directory tree listing in [Understanding the `custom-crawler-docs.zip` file](#ccs-grok-crawler-zip-file).

## For more information
{: #see-jdoc}

For detailed documentation of all of the interfaces and methods that are available in the `com.ibm.es.ama.custom.crawler` package, see the Javadoc, which is available as indicated in [Interfaces and Javadoc](#ccs-interfaces-jdoc).
