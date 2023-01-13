---

copyright:
  years: 2019, 2023
lastupdated: "2022-01-07"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# LDAP directory
{: #connector-ldap-cp4d}

Crawl records in an external directory that supports the Lightweight Directory Access Protocol (LDAP).
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} **{{site.data.keyword.icp4dfull_notm}} only**

This information applies only to installed deployments.
{: note}

As the directory data is added to your collection, {{site.data.keyword.discoveryshort}} interprets and stores key attributes of each record according to the configuration that you specify. Later, you can find relevant records by filtering on the attributes that are of interest to you. For example, you can capture department and location information, and then filter records by location later.

For more information about the Lightweight Directory Access Protocol, see [RFC 4511](https://datatracker.ietf.org/doc/html/rfc4511){: external}.

## What documents are crawled
{: #connector-ldap-cp4d-docs}

- Each LDAP record is crawled and added to the collection as one document.
- All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

## Data source requirements
{: #connector-ldap-cp4d-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-collection-types#requirements) for all installed deployments, your Salesforce data source must meet the following requirements:

-   The LDAP directory data source supports connections to the following types of directories:

    -   IBM Security Directory Server
    -   Microsoft Active Directory (On premises only)
    -   Oracle Directory Server

-   The LDAP directory data source collection does *not* support the following capabilities:

    -   Document-level security
    -   Mutual authentication. Verifying the server certificate is supported, but also verifying the client certificate is not.
    -   Proxy server access to the data source

## Prerequisite step
{: #connector-ldap-cp4d-prereq}

When you set up the collection, you must provide details such as the LDAP host name and port, for your directory server type. For more information about how to discover these values, see the documentation from the vendor:

- [IBM Security Directory Server](https://www.ibm.com/docs/en/sdse/6.4.0?topic=do-security-directory-server-overview){: external}
- [Microsoft Active Directory](https://docs.microsoft.com/en-us/machine-learning-server/operationalize/configure-authentication#active-directory-and-ldapldap-s){: external}
- [Oracle Directory Server](https://docs.oracle.com/cd/E20295_01/html/821-1220/bcalm.html#scrolltoc){: external}

## Connecting to an LDAP directory data source
{: #connector-salesforce-cp4d-task}

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **LDAP directory**, and then click **Next**.
1.  Name the collection.
1.  If the language of the documents in Salesforce is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    The crawler schedule options work as follows for LDAP directories:

    Full crawling
    :   Crawls all entries.
    
    Crawling updates
    :   Crawls all entries, then filters out any entries that were inserted, updated, or deleted since the last crawl.
    
    Crawling new and modified content
    :   Runs an LDAP query against the data source server to pick up any entries that were inserted or updated only.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  Configure a secure connection to the directory.

    Server type
    :   Choose your server type from the following options:

        -   IBM Security Directory Server
        -   Microsoft Active Directory
        -   Oracle Directory Server

    LDAP protocol
    :   If you want to encrypt data and verify the server certificate over Transport Layer Security (TLS), choose `ldaps`.
    
    LDAP host name
    :   Specify the hostname of the directory server. For example: `<ldap-hostname>.mydomain.com`.

    LDAP host port
    :   By default, the LDAP port is `389` and the LDAP-S port is `636`.

    LDAP binding username
    :   If the directory server requires credentials, the username that is used to bind to the directory service.

        In most cases, this username is a distinguished name (DN). The username is case-sensitive.

    LDAP binding user password
    :   The password that is associated with the username.
1.  Specify the information that you want to index from the directory.

    LDAP Base DN
    :   The object where you want to start the crawl.

        LDAP directories have a hierarchical tree structure of objects. The base search distinguished name specifies the subtree in which you want the crawl to be constrained.

        DN is a *distinguished name* that is defined by a series of *relative distinguished names* separated by commas. Each relative distinguished name consists of an *attribute* name-and-value pair that represents an object in a directory.

        For example, in Active Directory, attributes can include a common name (CN) such as `Jane Doe` and an organizational unit (OU) such as `Research`. Most distinguished names include one or more domain component (DC) attributes, which define the namespace where the LDAP directory is hosted.

        Here's an example of a distinguished name for Jane:

        ```text
        CN=Jane Doe,OU=Research,DC=IBM,DC=COM
        ```
        {: screen}

    LDAP user filter
    :   A filter to apply to the search to use to find LDAP entries that you want to crawl.

        If unspecified, a default value is applied that is considered the best filter for the server type that you selected. You can edit the predefined filter value.

        -   Expand the *Advanced configuration* section to list specific attributes to include or exclude from the search.

            For example, you might need to know the country in which an employee works, so you want to include a `c` attribute that stores the ISO country code. Or maybe you never want to return an employee's serial number, so you exclude the `serialnumber` attribute.

        -   Specify the search scope. You can choose to crawl records that are one level from the search base DN or to crawl the entire subtree that is associated with the search base DN.

        -   If the LDAP directory data source has binary attributes, you can enable the **Allow binary attributes** option.

            When enabled, the crawler creates a separate document for each binary attribute that is specified. The document also contains any other non-binary LDAP attribute values.

            For more information about the binary option, see [RTF 4522](https://datatracker.ietf.org/doc/html/rfc4522){: external}.

            In the **Binary attributes** field, specify the names of the binary attributes that you want to index.
1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
