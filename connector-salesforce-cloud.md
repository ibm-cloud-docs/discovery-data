---

copyright:
  years: 2015, 2023
lastupdated: "2022-07-21"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Salesforce
{: #connector-salesforce-cloud}

Crawl documents that are stored in a Salesforce data source.
{: shortdesc}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments. For more information about connecting to Salesforce from an installed deployment, see [Salesforce](/docs/discovery-data?topic=discovery-data-connector-salesforce-cp4d).
{: note}

## What documents are crawled
{: #connector-salesforce-cloud-objects}

During the initial crawl of the content, documents from all of the objects that can be accessed from the URL that you specify are crawled and added to your collection. Knowledge Articles are crawled only if their **version** is `published` and their languages is `en-us`.

During subsequent scheduled recrawls, only new and modified documents are crawled and any changes are reflected in your collection. Documents that are deleted from the external data source are not deleted from the collection.

All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

{{site.data.keyword.discoveryshort}} can crawl the following objects:

-   Any default and custom objects that you have access to
-   Accounts
-   Contacts
-   Cases
-   Contracts
-   Knowledge articles
-   Attachments

## Data source requirements
{: #connector-salesforce-cloud-reqs}

In addition to the [data source requirements](/docs/discovery-data?topic=discovery-data-sources#public-requirements) for all managed deployments, your Salesforce data source must meet the following requirements:

- The instance that you plan to connect to must be part of an Enterprise plan or higher.
- You must obtain any required service licenses for the data source that you want to connect to. For more information about licenses, contact the system administrator of the data source.

## What you need before you begin
{: #connector-salesforce-cloud-prereqs}

You must have the following information ready. If you don't know it, ask your Salesforce administrator to provide the information or consult the [Salesforce developer documentation](https://developer.salesforce.com/docs/){: external}.

Username
:   The `username` of an account that has access to the Salesforce site. For example, `jdoe@example.com`

Password
:   The password associated with the username. For example, `myP@ssw0rd`.

Service token
:   A valid Salesforce security token. For example, `mnaO8jsRET5CiJww9JnURlNN`.

URL
:   The URL of the Salesforce site that you want to crawl. For example, `https://my.salesforce.com`

## Connecting to the data source
{: #connector-salesforce-cloud-task}

To configure the Salesforce data source, complete the following steps in {{site.data.keyword.discoveryshort}}:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Salesforce**, and then click **Next**.
1.  Add values to the following fields:

    - Username
    - Password plus service token

      To form the password, concatenate the Password and Service token values that you noted earlier. For example, `myP@ssw0rdmnaO8jsRET5CiJww9JnURlNN`. The password and token values are never returned and are used only when credentials are created or modified.
    - URL

    Click **Next**.
1.  Name the collection.
1.  If the language of the documents on the site is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  Select the objects that you want to crawl.

    The more objects that you select, the longer the processing of the documents takes.
1.  If you want to look for and extract question-and-answer pairs, select **Apply FAQ extraction**.

    For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction).

1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
