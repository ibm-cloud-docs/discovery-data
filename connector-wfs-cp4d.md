---

copyright:
  years: 2019, 2023
lastupdated: "2022-10-06"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Windows File System
{: #connector-wfs-cp4d}

Crawl documents that are stored in a Microsoft Windows file system.
{: shortdesc}

![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

## What documents are crawled
{: #connector-wfs-cp4d-docs}

-   Only documents that are supported by {{site.data.keyword.discoveryshort}} in your file path are crawled; all others are ignored. For more information, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
-   Document-level security is supported. When this option is enabled, your users can crawl and query the same content that they can access when they access the file system directly.
-   When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index.
-   All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

## Data source requirements
{: #connector-wfs-cp4d-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements) for all installed deployments, your Windows File System data source must meet the following requirements:

-   The connector supports Microsoft Windows Server 2012 R2, 2016, 2019, and 2022.
-   The remote agent server and the file servers to be crawled must belong to the same Windows domain. The crawler can gather access control list (ACL) data from a single Windows domain only.

Support for Microsoft Windows Server 2022 was added with the 4.6 release.
{: note}

## Prerequisite steps
{: #connector-wfs-cp4d-prereq}

- If you want to enable document-level security, you must take some steps to set it up. For more information, see [Supporting document-level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).

    To configure document-level security, you need to collect the following information:

    LDAP server URL
    :   The LDAP server URL to connect to. For example, `ldap://<ldap_server>:<port>`.

    LDAP binding username
    :   The username to use to bind to the directory service.

    In most cases, this username is a distinguished name (DN). An Active Directory username might work, but, unlike the general Windows logon, it is case sensitive.

    LDAP binding user password
    :   The password that is associated with the binding username.

    LDAP base DN
    :   The starting point for searching user entries in LDAP. For example, `CN=Users,DC=example,DC=com`.

    LDAP user filter
    :   The user filter to search user entries in LDAP. If empty, the default value is `(userPrincipalName={0})`.

-   Before you configure a Windows File System collection, you must install the IBM Watson Discovery Agent for Windows File Systems on a remote Windows file server or on a remote Windows server. The agent is a Windows service that retrieves data from data source servers and sends it to {{site.data.keyword.discoveryshort}}. The agent can crawl remote Windows file systems, drives that are local to the agent, and shared network folders.

    If you install the agent on a remote Windows server, the remote Windows server must be able to mount one or more file servers so that the agent can crawl the remote Windows file systems.

    To install and configure the agent, complete the following tasks:

    -   [Install the agent](#connector-wfs-cp4d-prereq1).
    -   [Configure shared directories on the agent server](#connector-wfs-cp4d-prereq2).
    -   [Start and monitor the status of the agent server](#connector-wfs-cp4d-prereq3).

### Install the agent
{: #connector-wfs-cp4d-prereq1}

With the 4.6 release, the IBM Watson Discovery Agent for Windows File Systems was updated to run with 64-bit versions of Windows. If you installed the agent with a release prior to 4.6, you must uninstall the previous version, delete it, and then reinstall the agent. 

Do one of the following tasks:

-  You are using the connector for the first time: [Install the agent](#connector-wfs-cp4d-prereq1-new)
-  You have a previous installation: [Replace the previous agent](#connector-wfs-cp4d-prereq1-replace)

#### Replacing the previous agent
{: #connector-wfs-cp4d-prereq1-replace}

Required for deployments where a version of the IBM Watson Discovery Agent for Windows File Systems that is earlier than 4.6.0.0 is installed.

To replace an earlier version of the agent, complete the following steps:

1.  Copy the configuration file that defines the shared network directories that the Windows File System agent can access to a directory that is outside the agent's file path, which is `C:\Program Files (x86)\IBM\es`. 

    For example, copy the `C:\Program Files (x86)\IBM\es\distributed\esadmin\config\esfsexport.txt` file to a directory such as `C:\temp` directory.
1.  From the Microsoft Windows *Apps & features* utility, find the earlier version of *IBM Watson Discovery Agent for Windows File Systems*, and then click *Uninstall*.
1.  Choose *Completely delete IBM Watson Discovery Agent for Windows File Systems*, and then click *Uninstall*.
1.  Restart your system.
1.  Complete the steps in [Installing the agent](#connector-wfs-cp4d-prereq1-task) to install the latest version of the agent.
1.  Replace the new version of the `C:\Program Files\IBM\es\distributed\esadmin\config\esfsexport.txt` file with the file that you copied in Step 1.

    This step adds the configuration of the shared directories that you set up for the previous version of the agent to the new installation. When you reuse the file share, you can skip the step of configuring the shared directories.
1.  Run the following command to verify that the directory is shared with the agent service:

    ```screen
    C:\Users\Administrator> esagent --lsshare
    ```
    {: codeblock}

#### Installing the agent
{: #connector-wfs-cp4d-prereq1-new}

To install the IBM Watson Discovery Agent for Windows File Systems for the first time, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Windows File System**, and then click **Next**.
1.  Scroll to the *Download & install Windows Agent* section, and then click **Download Windows Agent Installer**.

    A ZIP file is downloaded.
1.  Extract the files from the `WindowsAgentServer.zip`.
1.  You can choose one of the following methods to run the installation program:

    - Double-click the `install.exe` file to launch the installation wizard.
    - To run the installation program in text mode from a console, complete the following steps:

        -   Change to the agent directory.
        -   Enter the following command:

            ```bash
            install.exe -i console
            ```
            {: pre}

            The screens are rendered in text and prompt you for the same information as the graphical installation.

            After you enter the command, a process runs in the background for several seconds before the console installation program is displayed.
            {: note}

    -   To install the agent server silently, complete the following steps:

        -   Change to the `Agent/responseFiles` directory.
        -   Edit the `DistributedFileSystemCrawler.properties` template response file to provide information about your environment. To run the installation program, change to the agent directory, and then specify the name of the file that you edited.

            See the following example:

            ```bash
            install.exe -i silent -f responseFiles/DistributedFileSystemCrawler.properties
            ```
            {: pre}

        If you copy a template file to another location to edit, specify the fully qualified path for the file when you run the installation program. If the response file path includes a space, enclose the path in double quotation marks (`"`). See the following example:

        ```bash
        install.exe -i silent -f "c:\My Documents\DistributedFileSystemCrawler.properties"
        ```
        {: pre}

1.  You must provide the following information during the installation process:

    -   `hostname`: Enter or verify the fully-qualified hostname of the computer you are installing the agent server on.

        You cannot specify an IPv6 address as the hostname of the server.
        {: important}

    -   `username`: Enter the username of an account that can be used to authorize access to the agent server.

        If the username does not exist, select the checkbox to create the account.

        To crawl a domain in a secure collection, the username must be an existing domain user with administration privileges for the Windows system to be crawled. To specify a domain user, use the format `<username>@<domain name>`.
        {: important}

    -   `password`: Provide the password that is associated with the username.

1.  **Optional**: If you want to change the default path and port settings, click **Advanced Options**.

    -   You can change the paths for the installation directory and data directory.
    -   The agent server uses three TCP/IP ports for authenticating connections to the server, transferring data between the file systems and {{site.data.keyword.discoveryshort}}, and monitoring the agent server. The default port numbers are `8397` and `8398`. If those values conflict with other port assignments in your system, change the port numbers.
1.  On the summary page, review the options that you selected, and click **Install** to start installing the software.
1.  Restart your computer.

### Configuring shared directories on the agent server
{: #connector-wfs-cp4d-prereq2}

After the software is installed, you must set up shared network directories that the Windows File System agent can access. To define a new file system share, export a local or remote network directory. 

If you are replacing an agent that you installed with a release that is earlier than 4.6.0.0, skip this procedure. The replacement instructions explain how to reuse the file share that was defined previously.
{: important}

1.  Export a local directory from the server where the agent is installed:

    ```bash
    esagent --addshare <d:><\example>
    ```
    {: pre}

    Where `d:` represents the drive letter you want to use and where `\example` represents the path to the local directory.
1.  Export a remote network directory that is accessible from the server where the agent is installed:

    ```bash
    esagent --addshare <\\files.example.com\data>
    ```
    {: pre}

    Where `\\files.example.com\data` represents the hostname or IP address of the remote server or the path to the remote directory.
1.  List shares that are defined on the server where the agent is installed:

    ```bash
    esagent --lsshare
    ```
    {: pre}

1.  If you want to delete a share that is defined on the server where the agent is installed, you can use the following command:

    ```bash
    esagent --rmshare \\files.example.com\data
    ```
    {: pre}

### Server status commands
{: #connector-wfs-cp4d-prereq3}

After you install the agent server, you can enter commands to start, stop, and check the status of the server.

Stopping the agent server also stops the crawler. For example, if the crawler stops unexpectedly, you can close connections and release resources for that crawler.

-   To start the server, enter the following command:

    ```bash
    esagent start
    ```
    {: pre}

-   To stop the server, enter the following command:

    ```bash
    esagent stop
    ```
    {: pre}

-   To get the status of the agent server, enter the following command:

    ```bash
    esagent getStatus
    ```
    {: pre}

The output of the `getStatus` command is an XML file with the following output:

```xml
<AgentStatus>
  <SpaceStatus>
    <SpaceId>012</SpaceId>
    <RootFolder>E:\\Projects\Analytics\\data\test1</RootFolder>
    <ConnectionNumber>9</ConnectionNumber>
    <StartTime>1244709336093</StartTime>
    <LastTime>1244709385843</LastTime>
    <IdlePeriod>219</IdlePeriod>
  </SpaceStatus>
  <SpaceStatus>
    <SpaceId>013</SpaceId>
    <RootFolder>E:\\Projects\Analytics\\data\test2</RootFolder>
    <ConnectionNumber>10</ConnectionNumber>
    <StartTime>1244709336093</StartTime>
    <LastTime>1244709385843</LastTime>
    <IdlePeriod>219</IdlePeriod>
  </SpaceStatus>
```
{: codeblock}

## Connecting to a Windows File System data source
{: #connector-wfs-cp4d-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps.

If you completed the prerequisite steps, return to the Windows File System data source collection that you started to create, and then skip to Step 4.
{: note}

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Windows File System**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents that you want to crawl is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  In the *Enter your credentials* section, add values to the following fields. You provided these fields during the installation of the agent server, which was described in the [Prerequisite steps](#connector-wfs-cp4d-prereq) section.

    Host
    :   The hostname of the remote Microsoft Windows server, for example `<hostname>.mydomain.com`.

    Username
    :   The username to connect the agent server. You use the username to connect {{site.data.keyword.discoveryshort}} to the shared network folders and crawl content.

    Password
    :   The password that is associated with the username.

    Agent Authentication Port
    :   The port to use for authentication. The default port value is `8397`.

    Port
    :   The port to use for transferring data. The default port value is `8398`.

1.  In the *Specify what you want to crawl* section, enter the file path that you want to crawl in the **Path** field, and then click **Add**.

    The file path is case sensitive.

    Optionally, add more file paths.
1.  **Optional**: Customize the types of files that are crawled.

    The crawler is configured automatically to exclude a list of file extensions for file types that can be unsafe to crawl. You can add more file extensions to the excluded filter list, or list only the file extensions for file types that you want to include in the crawl. Listing the types of files to include is even more secure.

    To change the file types that are crawled, in the *Extension filter* section, choose whether to use an Excluded or Included filter list. And then list the file extensions for the types of files you want to exclude or include.

    This configuration option was introduced with the 4.0.3 release.
    {: note}

1.  **Optional**: Specify the character set of the data to crawl.

    The converter that is used by the crawler is configured automatically to detect the character set of the files before it converts them. However, you can choose to specify a different character encoding to use for the data conversion. To specify a character encoding, complete the following steps:
    
    -   Set the **Automatic code page detection** switch to `Off`. 
    -   In the *Code page to use* field, specify the character encoding as a [Java Charset](https://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html){: external} value. For example, `UTF-8` or `UTF-16`. If you don't specify a character set, ISO-8859-1 is used.

    This configuration option was introduced with the 4.0.3 release.
    {: note}

1.  **Optional**: If you want to enable document-level security, in the *Security* section, set the **Enable Document Level Security** switch to `On`.

    When you enable this option, your users can crawl and query content that they have access to. You must provide the details about the LDAP directory you want to use.

    LDAP server URL
    :   The LDAP server URL to connect to. For example, `ldap://<ldap_server>:<port>`.

    LDAP binding username
    :   The username to use to bind to the directory service.

    LDAP binding user password
    :   The password that is associated with the binding username.

    LDAP base DN
    :   The starting point for searching user entries in LDAP. For example, `CN=Users,DC=example,DC=com`.

    LDAP user filter
    :   The user filter to search user entries in LDAP. If empty, the default value is `(userPrincipalName={0})`.

1.  If you want the crawler to extract text from images in documents, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
