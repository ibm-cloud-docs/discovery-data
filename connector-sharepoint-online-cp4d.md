---

copyright:
  years: 2019, 2025
lastupdated: "2025-08-29"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Microsoft SharePoint Online
{: #connector-sharepoint-online-cp4d}

Crawl documents that are stored in an online Microsoft SharePoint data source.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} [IBM Software Hub]{: tag-teal}

This information applies only to installed deployments. For more information about connecting to an online SharePoint site from a managed deployment, see [SharePoint Online](/docs/discovery-data?topic=discovery-data-connector-sharepoint-online-cloud).
{: note}

## What documents are crawled
{: #connector-sharepoint-online-cp4d-docs}

- During the initial crawl of the content, documents from all of the objects that can be accessed from the site collection path that you specify are crawled and added to your collection. Custom metadata that is associated with the SharePoint content is crawled also.
- You can crawl one site collection path per collection.
- Only documents that are supported by {{site.data.keyword.discoveryshort}} are crawled; all others are ignored. For more information, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
- Document-level security is supported. When this option is enabled, your users can crawl and query the same content that they can access when they are logged in to SharePoint. For more information, see [Supporting document-level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).
- When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index.
- All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

{{site.data.keyword.discoveryshort}} can crawl the following objects:

-   Site Collections
-   Sites
-   SubSites
-   Lists
-   List Items
-   Document Libraries
-   List Item Attachments

## Data source requirements
{: #connector-sharepoint-online-cp4d-reqs}

In August 2025, Microsoft blocked SharePoint Online legacy authentication protocols. Due to this change, SharePoint Online collection with the authentication principal type *User* is no longer able to crawl documents. Instead, you must move to the *Service* type authentication.
{: deprecated}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements) for all installed deployments, your SharePoint Online data source must meet the following requirements:

-   The Site Collection that you connect to must be one that was created with an Enterprise plan. It cannot be a collection that was created with a frontline worker plan.
-   Authentication support differs based on the principal type you specify when you configure the authentication method. Determine which principal type you want to use before you create the collection; you cannot change the principal type later. The following options are available:

    -   **User**: The following requirements must be met by the crawl user account:

        -    Account must have an Azure Active Directory user ID with permission to access all of the objects that you want to crawl. For example, `admin_user@company.onmicrosoft.com`. The user ID must have `Site Collection Administrator` permission.
        -   Account must have legacy authentication enabled. To enable legacy authentication, go to the [Azure portal](https://portal.azure.com/){: external} or contact your Azure Active Directory administrator.

            The connector supports the `Password hash synchronization (PHS)` method for enabling hybrid identity only. Use any other type (such as Pass-through authentication or Federation) at your own risk. Unless you created your SharePoint Online account before January 2020, two-factor authentication is enabled for the account by default. You must disable two-factor authentication.

            To view and change your multifactor authentication status, see [View the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#view-the-status-for-a-user){: external} or [Change the status for a user](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-userstates#change-the-status-for-a-user){: external}.

    -   **Service**: When you connect to your data as an Azure Active Directory service principal, you can use multifactor authentication.

For more information about SharePoint Online, see [Microsoft SharePoint developer documentation](https://docs.microsoft.com/en-us/sharepoint/dev/){: external}.

### Prerequisite steps when using a User principal
{: #connector-sharepoint-online-cp4d-prereqs-user-principal}

If you want to enable document-level security, you must take some steps to set it up. For more information, see [About document-level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).

The following table lists the permissions to set for a User principal authentication method.

1.  Register your app. 

    For more information, see the [Microsoft documentation](https://docs.microsoft.com/en-us/graph/auth-register-app-v2){: external}.
1.  Configure API permissions.

| API  | Permissions | Type   |
| --------------- | ------------------------------- | ------------- |
| Microsoft Graph (Groups) | `Group.Read.All` or `Group.ReadWrite.All` | Delegated |
| Microsoft Graph (Directories) | `Directory.AccessAsUser.All` or `Directory.Read.All` or `Directory.ReadWrite.All` | Delegated |
| SharePoint Online | `User.Read.All` or `User.ReadWrite.All` | Delegated |
{: caption="User principal API configuration" caption-side="top"}

### Prerequisite steps when using a service principal
{: #connector-sharepoint-online-cp4d-prereq-service-principal}

A service principal is a security identity that is used by user-created apps, services, and automation tools to access specific Azure resources. It is like a user identity (verified with a certificate) that has a specific role, and tightly-controlled permissions. If you connect to SharePoint Online as a service principal user, you can access your data without disabling multifactor authentication.

To prepare to connect as a service principal, complete the following steps:

1.   [Create a certification file](#service-principal-cert-file).
1.   [Register an application with SharePoint Online](#register).
1.   [Add a certificate](#add-certificate).
1.   [Configure API permissions](#api-permissions).
1.   [Enable the Azure Access Control Service (ACS)](#enable-azure-acs).
1.   [Create a site permission](#site-permission).

#### Create a certification file
{: #service-principal-cert-file}

The crawler supports the following formats for a private key:

-   PKCS #1
-   PKCS #1 with password
-   PKCS #8
-   PKCS #8 with password

The following procedure shows you how to create a private key with the PKCS #1 format without a password.

1.  Create a private key.

    ```bash
    openssl genrsa 2048 > spo-private.key
    ```
    {: codeblock}

1.  Create a public key.

    ```bash
    openssl rsa -in spo-private.key -pubout -out spo-public.key
    ```
    {: codeblock}

1.  Create a Certificate Signing Request (CSR) file.

    ```bash
    openssl req -new -key spo-private.key > spo-request.csr
    ```
    {: codeblock}

1.  Create a certification file.

    ```bash
    openssl x509 -req -in spo-request.csr -signkey spo-private.key -out spo.crt -days 3650
    ```
    {: codeblock}

#### Register an application with SharePoint Online
{: #register}

Follow the Microsoft documentation instructions for [registering an Azure AD application](https://docs.microsoft.com/en-us/sharepoint/dev/solution-guidance/security-apponly-azuread#setting-up-an-azure-ad-app-for-app-only-access){: external}.

Make the following choices:

-   Choose the *Accounts in this organizational directory only* option.
-   Set the client type as a public client.
-   Make a note of the Azure application (client) ID that is assigned to your app when you register it.

When you register an application in the portal, an application object and a service principal object are automatically created in your home tenant.

#### Add a certificate
{: #add-certificate}

Upload the certificate that you created earlier.

#### Configure API permissions
{: #api-permissions}

Follow the [Microsoft documentation](https://docs.microsoft.com/en-us/sharepoint/dev/solution-guidance/security-apponly-azuread#setting-up-an-azure-ad-app-for-app-only-access){: external} to add API permissions.

The following table lists the permissions to set for a Service principal authentication method and document-level security is enabled.

| API  | Permissions | Type   |
| --------------- | ------------------------------- | ------------- |
| Microsoft Graph (Groups) | `Group.Read.All` | Application |
| Microsoft Graph (Directories) | `Directory.Read.All` | Application |
| SharePoint | `Sites.FullControl.All` | Application |
{: caption="Service principal with document-level security enabled API configuration" caption-side="top"}

The following table lists the permissions to set for a Service principal authentication method and document-level security is disabled.

| API  | Permissions | Type   |
| --------------- | ------------------------------- | ------------- |
| Microsoft Graph | `Sites.Read.All` | Application |
| SharePoint | `Sites.Read.All` | Application |
{: caption="Service principal with document-level security disabled API configuration" caption-side="top"}

1.  After configuring API permissions, click **Grant admin consent for {tenant-name}**.

#### Enable the Azure Access Control Service (ACS)
{: #enable-azure-acs}

This procedure is required only if you want to configure the application permissions for each site collection.

1.  Open a SharePoint Online Management Shell.

    For more information, see [Get started with SharePoint Online Management Shell](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online?view=sharepoint-ps){: external}. 

1.  Enable ACS-based app-only authentication by running the following command:

    ```bash
    Set-PnPTenant -DisableCustomAppAuthentication $false
    ```
    {: codeblock}

    For more information, see [Set-PnPTenant](https://pnp.github.io/powershell/cmdlets/Set-PnPTenant.html?q=Set-PnPTenant){: external}.

1.  Follow the steps in the Microsoft documentation to [Grant access using SharePoint App-Only](https://docs.microsoft.com/en-us/sharepoint/dev/solution-guidance/security-apponly-azureacs){: external}.
1.  Copy the Client ID and Client Secret values.
1.  Define the appropriate permission request for your deployment.

    Go to https://{tenant-name}.sharepoint.com/sites/{site}/_layouts/15/AppInv.aspx.

    If document-level security is enabled, specify the following XML request:

    ```xml
    <AppPermissionRequests AllowAppOnlyPolicy="true">
      <AppPermissionRequest Scope="http://sharepoint/content/sitecollection" Right="FullControl" />
    </AppPermissionRequests>
    ```
    {: codeblock}

    If document-level security is disabled, specify the following XML request:

    ```xml
    <AppPermissionRequests AllowAppOnlyPolicy="true">
      <AppPermissionRequest Scope="http://sharepoint/content/sitecollection" Right="Read" />
    </AppPermissionRequests>
    ```
    {: codeblock}

1.  Confirm that you trust the app.

#### Create a site permission
{: #site-permission}

Add a `Sites.Selected` permission for the Microsoft Graph API. Require `Sites.FullControl.All` permission to call the following API:

```rest
curl -s -XPOST -H "Authorization: ${access_token}" -H "Content-Type: application/json" \
  https://graph.microsoft.com/v1.0/sites/{site}/permissions -d '{
  "roles": ["read"],
  "grantedToIdentities": [{
    "application": {
      "id": "{azure_ad_app_id}",
      "displayName": "{display_name}"
    }
  }]
}'
```
{: codeblock}

For more information, see the [Microsoft documentation](https://docs.microsoft.com/en-us/graph/api/site-post-permissions?view=graph-rest-1.0&tabs=http){: external}.

## Connecting to a SharePoint Online data source
{: #connector-sharepoint-online-cp4d-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **SharePoint Online**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents in SharePoint is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).

1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).

1.  In the *Authentication method* section, specify the principal type you want to use when you authenticate with SharePoint from the following options:

    -   **User**: A user in your Active Directory organization.

        In the *Enter your credentials* section, complete the following fields:

        Username
        :   The username of the SharePoint user with access to all sites and lists that need to be crawled and indexed, for example `crawl_username@company.onmicrosoft.com`.

        Password
        :   The password of the SharePoint user.

        This value is never returned and is used only when you create or modify credentials.
        
    -   **Service**: A security identity used by user-created apps, services, and automation tools to access specific Azure resources. It is like a user identity (verified with a certificate) that has a specific role, and tightly-controlled permissions.

        Support for using a service principal was added with version 4.0.3.
        {: note}

        In the *Enter your credentials* section, complete the following fields:

        Tenant name
        :   The tenant where the data resides. For example, `ibm.onmicrosoft.com`.
        
        Application ID
        :   The ID of your app. For example, `19ce9f74-cd14-4b68-8dfc-4bcc75ed2fe9`.

        Upload the following files:

        Certification file
        :   The certification file that you created in SharePoint. For example, `myinfo.crt`.

        Private key file
        :   The private key file that you created in SharePoint. For example, `private.app.key`.

            If a private key password is required, specify the password.

        If this crawler has permissions to access the specified site collection only, set the **Azure Access Control Service** switch to `On`, and then provide the following values:

        -   **Client ID**
        -   **Client secret**

1.  In *Specify what you want to crawl* section, add values to the following fields:

    Site Collection Url
    :   The SharePoint web service URL. For example, `https://organization_name.com`.

    User principal only
    :   In the **Site Collection Name** field, specify the name that the site collection uses. Get the name from the site collection settings.

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

    When this option is enabled, your users can crawl and query the same content that they can access when they are logged in to SharePoint. For more information, see [Supporting document-level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).

    **User principal only**: When you enable this option, you must add the Azure ID that was assigned to the application upon registration to the **Application ID** field.

    To enable document-level security, you must register your application with SharePoint. For more information, see the prerequisite steps for the principal type you are using.
1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
