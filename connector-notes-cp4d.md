---

copyright:
  years: 2019, 2023
lastupdated: "2022-11-11"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# HCL Notes
{: #connector-notes-cp4d}

Crawl an HCL Notes (formerly Lotus Notes) database.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

## What documents are crawled
{: #connector-notes-cp4d-docs}

- Each document in the HCL Notes database is crawled and added to the collection as a document.
- If an HCL Notes document has a file attachment, and you choose to process file attachments, only documents that are supported by {{site.data.keyword.discoveryshort}} are crawled; all others are ignored. For more information, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
- If you choose to process attachments, the crawler attempts to crawl and index files that are attached to HCL Notes documents. File types that are supported by {{site.data.keyword.discoveryshort}} are indexed. For more information, see [Supported file types](/docs/discovery-data?topic=discovery-data-collections#supportedfiletypes).
- Document-level security is supported. When this option is enabled, your users can crawl and query the same content that they can access when they are logged in to HCL Notes. For more information, see [Supporting document-level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).
- When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index.
- All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

## Data source requirements
{: #connector-notes-cp4d-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements) for all installed deployments, your HCL Notes data source must meet the following requirements:

- The data source can crawl HCL Notes 9.0.1 databases.
- The HCL Notes data source supports the Domino Internet Inter-ORB Protocol (DIIOP) protocol only.
- To crawl documents, including ACLs, you must have at least `Reader` level access to server, database, and document access on the Domino server.
- For group extractions from the internal Domino LDAP directory, you must have `Reader` access to the `names.nsf` directory database.
- For group extractions from the external LDAP directory, you must have the credential for the external LDAP server.

## Prerequisite steps
{: #connector-notes-cp4d-prereq}

-   If you want to enable document-level security, you must take some steps to set it up. For more information, see [Supporting document-level security](/docs/discovery-data?topic=discovery-data-collection-types#configuredls).

    You can use the LDAP server that is used by HCL Notes (either the internal Domino LDAP or an external LDAP directory) as a remote LDAP directory to manage document-level security. Users who search the collection can be listed in an external LDAP directory. However, the user credentials that you use to set up the crawl must belong to a user who is listed in the internal Domino LDAP directory.

    To configure document-level security, you need to collect the following information:

    LDAP server URL
    :   The LDAP server URL to connect to. For example, `ldap://<ldap_server>:<port>`.
    
    LDAP binding username
    :   The username to use to bind to the directory service. This user must have administrative access and be listed in the internal Domino LDAP directory.

    LDAP binding user password
    :   The password that is associated with the user.

    LDAP base DN
    :   The starting point for searching user entries in LDAP. For example, `CN=Users,DC=example,DC=com`.

    LDAP user filter
    :   The filter to apply to searches for user entries in LDAP. If unspecified, the default value is `(userPrincipalName=\{0\})`.
    
    LDAP group filter
    :   The filter to apply to searches for group entries in LDAP.

-   Before you can crawl servers by using the Domino Internet Inter-ORB Protocol (DIIOP) protocol, you must configure the HCL Notes server to use the protocol. The server that you want to crawl must be running the DIIOP and HTTP tasks.

To configure the HCL Notes server to use DIIOP, complete the following steps:

1.  Configure the HCL Notes server document.

    -   In HCL Notes, open the `server` document on the HCL Notes server that you want to crawl. This document is stored in the Domino directory.
    -   On the Configuration page, expand the *server* section.
    -   On the Security page in the Programmability Restrictions section, specify the appropriate security restrictions for your environment in the following three fields:

        -   **Run restricted Lotus Script/Java agents**
        -   **Run restricted Java/Javascript/COM**
        -   **Run unrestricted Java/Javascript/COM**

        For example, you might specify an asterisk (`*`) to allow unrestricted access by LotusScript/Java agents and specify usernames that are registered in the Domino directory for the Java/JavaScript/COM restrictions.

        To crawl a server that uses the DIIOP protocol, your configured crawler must be able to access the usernames that you specify in these fields.
        {: important}

    -   Open the Internet Protocol page, and then open the HTTP page. Set the **Allow HTTP clients to browse database** option to **Yes**.
1.  Configure the user document.

    -   Open the `user` document for the user whose credentials that you want to use for LDAP binding. This document is stored in the Domino directory.
    -   On the Basics page in the **Internet password** field, specify a password.

        You specify this user and password information when you set up the data source.
1.  Restart the DIIOP task on the HCL Notes server.

For more information, see [Running server tasks](https://help.hcltechsw.com/domino/9.0.1/admin/admin/admn_runningservertasks_t.html){: external} in the HCL Notes documentation.

## Connecting to an HCL Notes data source
{: #connector-notes-cp4d-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Notes**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents in HCL Notes is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  In the *Enter your credentials* section, add values to the following fields:

    Host name
    :   The hostname of the HCL Notes server.

    User name
    :   The username to use to crawl the HCL Notes server.
    
    Password
    :   The password that is associated with the user.

1.  In the *Crawl type*, choose what you want to crawl from the following options:

    -   If you want to crawl a specific HCL Notes database, choose **Database**, and then add the file name of the database to the **Database file name** field.
    -   If you want to crawl multiple databases, choose **Directory**. Specify the directory in which the databases that you want to crawl are stored in the **Directory name** field.
1.  **Optional**: In the *Security* section, specify whether you want to enable document-level security.

    -   If you want to enable document-level security, set the **Enable Document Level Security** switch to `On`.

        When set to **On**, your users can crawl the same content that they have access to in a HCL Notes database or directory.
    - To use the Domino LDAP directory, set the **Use remote LDAP directory** switch to `On`. Provide details about the Domino LDAP directory. You collected this information when you performed the prerequisite step.

        LDAP server URL
        :   The LDAP server URL to connect to. For example, `ldap://<ldap_server>:<port>`.

        LDAP binding username
        :   The username to use to bind to the directory service.
        
        LDAP binding user password
        :   The password that is associated with the user.

        LDAP base DN
        :   The starting point for searching user entries in LDAP. For example, `CN=Users,DC=example,DC=com`.
        
        LDAP user filter
        :   The filter to apply to searches for user entries in LDAP. If unspecified, the default value is `(userPrincipalName=\{0\})`.
        
        LDAP group filter
        :   The filter to apply to searches for group entries in LDAP.

1.  **Optional**: In the *Advanced options* section, make choices about the following configuration settings:

    Crawl attachments
    :   If you want to crawl files that are attached to HCL Notes documents, set the switcher to `On`.

    Automatic code page detection
    :   If you want the encoding converter to detect the code of pages to crawl, keep the switch set to `On`. If you set the switcher to `Off`, specify values for the following fields:

        Code page to use
        :   Specify the character encoding of the pages that you want to crawl. If unspecified, the default value of `UTF-8` is used.

        Notes formula
        :   Specify a HCL Notes formula to use to filter the data that you want to crawl. For example, `SELECT @IsAvailable(Year) & Year > 2003`.

        For more information, see [Formula language](https://help.hcltechsw.com/dom_designer/10.0.1/basic/H_NOTES_FORMULA_LANGUAGE.html){: external} in the HCL Notes documentation.
1.  Specify the date that you want to use when you filter the documents. The date is stored in a field that is named `_ _$Date$_ _` in HCL Notes documents. By default, the field stores the last modified date of the document. You can choose a different date to store in the field instead.

    Document modification date
    :   Uses the date that the document was last modified. This option is selected by default.

    Document crawl date
    :   Uses the last crawled date.

    Document creation date
    :   Uses the creation date of the document.

1.  If you want the crawler to extract text from images in documents, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
