---

copyright:
  years: 2015, 2022
lastupdated: "2022-03-09"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Microsoft SharePoint Online
{: #connector-sharepoint-online-cloud}

Crawl documents that are stored in a Microsoft SharePoint Online data source.
{: shortdesc}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments. For more information about connecting to SharePoint Online from an installed deployment, see [SharePoint Online](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cp4d). If you are using a Discovery service instance that was created with a Lite or an Advanced plan, or that was created with a Premium plan before 16 July 2020, see [SharePoint Online](/docs/discovery?topic=discovery-sources#connectsp){: external}.
{: note}

## What documents are crawled
{: #connector-sharepoint-online-cloud-objects}

During the initial crawl of the content, documents from all of the objects that can be accessed from the site collection path that you specify are crawled and added to your collection. Custom metadata that is associated with the SharePoint content is crawled also. You can crawl one site collection path per collection. You cannot crawl *Personal SiteCollections*.

During subsequent scheduled recrawls, only new and modified documents are crawled and any changes are reflected in your collection. Documents that are deleted from the external data source are not deleted from the collection.

All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

{{site.data.keyword.discoveryshort}} can crawl the following objects:

-   SiteCollections
-   Sites
-   SubSites
-   Lists
-   List Items
-   Document Libraries
-   List Item Attachments

## Data source requirements
{: #connector-sharepoint-online-cloud-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-sources#public-requirements) for all managed deployments, your SharePoint Online data source must meet the following requirements:

-   The Site Collection that you connect to must be one that was created with an Enterprise plan. It cannot be a collection that was created with a frontline worker plan.
-   You must have an Azure Active Directory user ID with permission to read all of the objects that you want to crawl. For example, `<admin_user>@.onmicrosoft.com`. The user ID does not need `SiteCollection Administrator` permission.

You can choose how to authenticate with the external Microsoft SharePoint account from the following options:

Open Authentication (OAuth)
:   Authenticates with the external data source by using a token so that your user credentials do not need to be shared. With this authentication method, you can log in to your Microsoft account directly during the set up of the connector. Select *Sign in with Microsoft* to log in to your Microsoft account in a separate dialog, which generates a token that is used by {{site.data.keyword.discoveryshort}} to connect to your data.

    You cannot currently change the user account that is associated with the OAuth setup later, nor any of the details of the existing user account that the connector is configured to use. For example, you cannot update the password that was used to set up the connection after a password change in SharePoint.

    The *Sign in with Microsoft* option that uses Open Authentication to authenticate with the external data source is a beta feature.
    {: beta}

Security Assertion Markup Language (SAML)
:   An older mechanism for authentication and authorization that requires user credentials to be shared with the {{site.data.keyword.discoveryshort}} service.

    If you choose to use this authentication method, your Microsoft SharePoint account must meet the following requirements:

    -   Unless you created your SharePoint Online account before January 2020, two-factor authentication is enabled for the account by default. You must disable two-factor authentication.

        To view and change your multifactor authentication status, see [View the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#view-the-status-for-a-user){: external} or [Change the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#change-the-status-for-a-user){: external}.
    -   The crawl user account must have legacy authentication and `Contribute` level permissions enabled.

        To enable legacy authentication, go to the [Azure portal](https://portal.azure.com/){: external} or contact your SharePoint administrator.
    -   The connector supports the `Password hash synchronization (PHS)` method for enabling hybrid identity only. Use any other type (such as Pass-through authentication or Federation) at your own risk. 

Support for the OAuth method of authentication was added with a software update in February 2022. If you want to update an existing connector to use OAuth instead of SAML, you must re-create the connector. You cannot currently change the authentication mechanism for an existing connector.
{: note}

## What you need before you begin
{: #connector-sharepoint-online-cloud-prereqs}

You must have the following information ready. If you don't know it, ask your SharePoint administrator to provide the information or consult the [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}:

Username
:   The username of the user account to use to connect to the SharePoint Online SiteCollection that you want to crawl.

    For example, `<janedoe>@exampledomain.onmicrosoft.com`.

Password
:   The password to connect to the SharePoint Online SiteCollection that you want to crawl.

    This value is never returned and is only used when credentials are created or modified.

Organization URL
:   The root URL of the source that you want to crawl. Specify the domain name of the URL, for example `https://<company>.<domain>.com`.

Site collection path
:   The `site_collection_path` to the section of the site where you want to start the crawl.

    For example, if the content that you want to crawl is available from `https://<company>.<domain>.com/sites/test`, then you can specify `https://<company>.<domain>.com` as the Organization URL and `/sites/test` as the Site collection path.

    -   You cannot specify folder paths as input.
    -   You cannot specify a path to an Active Server Page Extended (ASPX) file, such as URLs to document libraries, lists, and subsites.
    -   If you don't specify a path, the default value of `/` is used, and the root site collection is crawled.
-   **Application ID**: ID of the data source that you want to crawl. This information is required only if you want to store ACL information that is associated with the source documents.

## Connecting to the data source
{: #connector-sharepoint-online-cloud-task}

To configure the Microsoft SharePoint Online data source, complete the following steps in {{site.data.keyword.discoveryshort}}:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **SharePoint Online**, and then click **Next**.
1.  Add a URL to the **Organization URL** field.
1.  To enable access to your external data source, do one of the following things:

    -   If you want to use Open Authentication to connect to your data, click **Sign in with Microsoft**.

        Pop-ups must be enabled for this site in your web browser.
        {: note}

        Log in to your Microsoft SharePoint account with your user name and password, and then complete two-factor authentication, if necessary.
        
        If you are not prompted for a user name and password, take note. You might be logged in to a Microsoft Sharepoint account already. If you are logged in to an account that you don't want to use for this connector, stop here. (Any account where you are logged in will be used automatically. And you cannot change the account configuration later.) Open a web browser in incognito mode and start this procedure over from step 1.
        {: important}

        The *Sign in with Microsoft* option that uses Open Authentication to authenticate with the external data source is a beta feature.
        {: beta}

    -   Otherwise, you can specify a username and password for a user that is authorized to access the site you want to crawl, and then click **Next**.
    
        This method uses Security Assertion Markup Language (SAML) to authenticate with the external data source on your behalf.

1.  Specify the path you want to crawl in the **Site collection path** field.
1.  Name the collection.
1.  If the language of the documents on the site is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  **Optional**: If you want to store any access control information that exists in the SharePoint documents that you crawl, in the *Security* section, set the **Include Access Control List** switch to `On`.

    When you enable this option, information about SharePoint access rules that is stored in SharePoint source documents is retained and stored as metadata in the documents that are added to your collection.

    This feature is not the same as enabling document-level security for the collection. The access rules in the document metadata are not used by {{site.data.keyword.discoveryshort}} search. Enabling this feature merely stores the information so that you can leverage the access rules when you build a custom search solution.

    Use of this feature increases the size of the documents that are generated in the collection and increases the crawl time. Only enable the feature if your use case requires that you store the SharePoint document ACL information.
    {: important}
1.  If you want to look for and extract question-and-answer pairs, select **Apply FAQ extraction**.

    For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction).
1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.

### Sample access control list information
{: #connector-sharepoint-online-cloud-acl-sample}

The following screen capture illustrates the type of ACL information that is stored in the document when you include the access control list.

![Shows the Microsoft ACL information stored in the source object in the document metadata.](images/acl-in-output.png)
