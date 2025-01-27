---

copyright:
  years: 2019, 2025
lastupdated: "2022-09-28"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Microsoft SharePoint On Prem
{: #connector-sharepoint-onprem-cp4d}

Crawl documents that are stored in an on-premises Microsoft SharePoint data source.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments. For more information about connecting to an on-premises SharePoint site from a managed deployment, see [SharePoint On Prem](/docs/discovery-data?topic=discovery-data-connector-sharepoint-onprem-cloud).
{: note}

## What documents are crawled
{: #connector-sharepoint-onprem-cp4d-docs}

- Only documents that are supported by {{site.data.keyword.discoveryshort}} are crawled; all others are ignored. For more information, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
- Document-level security is supported. When this option is enabled, your users can crawl and query the same content that they can access when they are logged in to SharePoint. For more information, see [Supporting document-level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).
- When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index.
- All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

## Data source requirements
{: #connector-sharepoint-onprem-cp4d-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements) for all installed deployments, your SharePoint On Prem data source must meet the following requirements:

- The data source connection supports SharePoint 2013, 2016, or 2019.
- You must obtain any required service licenses for the data source that you want to connect to. For more information about licenses, contact the system administrator of the data source.

For more information about SharePoint On Prem, see [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}.

## Prerequisite steps
{: #connector-sharepoint-onprem-cp4d-prereq}

Before you create a SharePoint On Prem collection, you must do the following things:

1.  Work with the Sharepoint administrator to coordinate the set up of full read access for the web application. 

    For more information, see [Manage permissions for a web application in Sharepoint Server](https://docs.microsoft.com/en-us/sharepoint/administration/manage-permissions-for-a-web-application){: external}.

1.  If you want to enable document-level security, you must take some steps to set it up. For more information, see [Supporting document-level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).

    You must collect the following information from the LDAP administrator:

    LDAP server URL
    :   The LDAP server URL to connect to, for example `ldap://<ldap_server>:<port>`.

    LDAP binding username
    :   The username used to bind to the directory service. In most cases, this username is a distinguished name (DN). The logon name might sometimes work with Active Directory. But unlike the general Windows logon, it is case sensitive. The distinguished name always works.

    LDAP binding user password
    :   The password used to bind to the directory service.

    LDAP base DN
    :   The starting point for searching user entries in LDAP, for example `CN=Users,DC=example,DC=com`.

    LDAP user filter
    :   The user filter to search user entries in LDAP. If unspecified, the default value is `(userPrincipalName={0})`.

If you are using version 2.2.1 or earlier, then you must complete some extra prerequisite tasks before you can connect to the data source. For more information, see [SharePoint On Prem prerequisite steps for prior releases](#prior-prereqs).

## Connecting to a SharePoint On Prem data source
{: #connector-sharepoint-onprem-cp4d-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **SharePoint On Prem**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents in SharePoint is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  In the *Enter your credentials* section, complete the following fields:

    Username
    :   The username of the SharePoint user with access to all sites and lists that need to be crawled and indexed.
    
    Password
    :   The password of the SharePoint user.

    This value is never returned and is only used when you create or modify credentials.
1.  **Optional**: If you want to use Security Assertion Mark-up Language (SAML) claims-based authentication, set the **Enable SAML authentication** switch to `On`. Otherwise, Windows NT LAN Manager (NTLM) authentication is used. Add values to the following fields:

    Identity Provider endpoint
    :   The URL of the Identity Provider endpoint, for example `https://adfs.server.example.com/adfs/services/trust/2005/UsernameMixed`.
    
    Relying Party endpoint
    :   Optional. The URL of the Relying Party Trust endpoint. If unspecified, the following value is used: `https://<sharepoint_server>:<port>/_trust/`.
    
    Relying Party Trust identifier
    :   The URL of the Relying Party Trust identifier, for example `urn:sharepoint:sample`. If unspecified, the following value is used: `https://<sharepoint_server>:<port>/_trust/`. This feature is available in the 2013, 2016, and 2019 versions.

1.  In the *Specify what you want to crawl* section, add the SharePoint web service URL to the **Web Application Url** field. For example, `https://<host>:<port>`.
1.  **Optional**: If you are using a proxy server to access the data source server, then in the *Proxy settings* section, set the **Enable proxy settings** switch to `On`. Add values to the following fields:

    Username
    :   Optional. The proxy server username to authenticate, if the proxy server requires authentication. If you do not know your username, you can obtain it from the administrator of your proxy server.
    
    Password
    :   Optional. The proxy server password to authenticate, if the proxy server requires authentication. If you do not know your password, you can obtain it from the administrator of your proxy server.

    Proxy server host name or IP address
    :   The hostname or the IP address of the proxy server.

    Proxy server port number
    :   The network port that you want to connect to on the proxy server.

1.  **Optional**: If you want to activate document-level security, in the *Security* section, set the **Enable Document Level Security** switch to `On`.

    When this option is enabled, your users can crawl and query the same content that they can access when they are logged in to SharePoint. Complete the [prerequisite steps](#connector-sharepoint-onprem-cp4d-prereq) to add support.

    When you enable this option, you must provide values for the following fields:

    LDAP server URL
    :   The LDAP server URL to connect to, for example `ldap://<ldap_server>:<port>`.

    LDAP binding username
    :   The username used to bind to the directory service. In most cases, this username is a distinguished name (DN). The logon name might sometimes work with Active Directory. But unlike the general Windows logon, it is case sensitive. The distinguished name always works.

    LDAP binding user password
    :   The password used to bind to the directory service.

    LDAP base DN
    :   The starting point for searching user entries in LDAP, for example `CN=Users,DC=example,DC=com`.

    LDAP user filter
    :   The user filter to search user entries in LDAP. If unspecified, the default value is `(userPrincipalName={0})`.

1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1. Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.

### Prerequisite steps for prior releases
{: #prior-prereqs}

If you are using version 2.2.1 or earlier, then you must complete these extra steps before you can connect to the data source:

- Obtain a web services package from your {{site.data.keyword.discoveryshort}} cluster. This web services package is a custom module that the crawler uses to obtain the necessary information to crawl successfully. For more information, see [Get the web services package](#connector-sharepoint-onprem-cp4d-prereq1).
- Deploy the web service package on the SharePoint server. For more information, see [Deploy the web services on the SharePoint server](#connector-sharepoint-onprem-cp4d-prereq2).

### Get the web services package
{: #connector-sharepoint-onprem-cp4d-prereq1}

To obtain the web services package from your {{site.data.keyword.discoveryshort}} cluster, complete the following steps:

1.  Log in to your {{site.data.keyword.discoveryshort}} cluster.
1.  Enter the following command to obtain your `crawler` pod name:

    ```sh
    oc get pods | grep crawler
    ```
    {: pre}

    You might see output that is similar to the following message:

    ```text
    wd-discovery-crawler-57985fc5cf-rxk89     1/1     Running     0          85m
    ```

1.  Enter the following command to obtain the `ESSPSolution.wsp` file, replacing `{crawler-pod-name}` with the `crawler` pod name that you obtained in the previous step:

    ```sh
    oc exec {crawler-pod-name} -- ls -l /opt/ibm/wex/zing/resources/ | grep ESSPSolution
    ```
    {: pre}

    You might see output that is similar to the following message:

    ```text
    -rw-r--r--. 1 dadmin dadmin  8600 Feb  3 08:23 ESSPSolution-${build-version}.wsp
    ```

1.  Enter the following command to copy the `ESSPSolution.wsp` file to the host server, replacing `{build-version}` with the build version number from the previous step and `{crawler-pod-name}` with the `crawler` pod name:

    ```sh
    oc cp {crawler-pod-name}:/opt/ibm/wex/zing/resources/ESSPSolution-${build-version}.wsp ESSPSolution.wsp
    ```
    {: pre}

### Deploy the web services on the SharePoint server
{: #connector-sharepoint-onprem-cp4d-prereq2}

You can either manually deploy the web services on the SharePoint server or run a script that automatically deploys them.

To run the script that automatically deploys the web services:

1.  Run the `ESSPSolution.wsp` script on the SharePoint server by entering the following Windows PowerShell cmdlet: `Add-SPSolution -LiteralPath C:\files\ESSPSolution.wsp`
1.  In SharePoint, open SharePoint Central Administration and then open system settings.
1.  Deploy the package by using farm solutions.
1.  Select the `esspsolution.wsp` solution, and deploy the solution.

    After the deployment is complete, the farm solution is listed in the SharePoint administration console. An administrator can enable or disable the solution and can schedule triggers.
1.  Optional: Regardless of the approach that you used to deploy the web services, to complete the deployment in some environments, you might need to apply the following configurations to the Internet Information Services (IIS) server that hosts the SharePoint server and the web services:

    -   Allow .NET impersonation on IIS
    -   Change the ASP.NET trust level to WSS_Medium

    You can apply these configurations in the Internet Information Services Manager.
