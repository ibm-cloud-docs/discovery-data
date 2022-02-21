---

copyright:
  years: 2015, 2022
lastupdated: "2022-02-21"

keywords: api version,api,request syntax

subcollection: assistant-data
---

{{site.data.keyword.attribute-definition-list}}

# Building custom applications with the API
{: #api-use}

Use the {{site.data.keyword.discoveryshort}} API to build a custom application or component that searches your data.
{: shortdesc}

- For {{site.data.keyword.discoveryshort}} API reference documentation, see [API reference](https://cloud.ibm.com/apidocs/discovery-data){: external}.
- For more information about using the Analyze API to process documents without storing them, see [Analyze API](/docs/discovery-data?topic=discovery-data-analyzeapi).
- For more information about using the API to define more complex queries by using the Discovery Query Language, see [Query overview](/docs/discovery-data?topic=discovery-data-query-concepts).

## Service API Versioning
{: #apiversioning}

API requests require a version parameter that takes a date in the format `version=YYYY-MM-DD`. Whenever we change the API in a backwards-incompatible way, we release a new minor version of the API.

Send the version parameter with every API request. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.

The current version is `2020-08-30`.

## Getting your project ID ![IBM Cloud only](images/ibm-cloud.png)
{: #api-use-cloud}

This information applies to {{site.data.keyword.cloud_notm}} only.
{: important}

To use the API, you must construct the URL to use in your requests. Many of the API methods require the project ID.

1.  From the [IBM Cloud Resource list](https://cloud.ibm.com/resources){: external}, find the service page for your Discovery service instance.
1.  From the *Credentials* section, copy the URL. You specify this value as the `{url}` in your API requests.
1.  While you're on this page, copy the API key. You specify this value as the `{apikey}`.
1.  Open your project in {{site.data.keyword.discoveryshort}}, and then go to the **Integrate and deploy** > **API Information** page.
1.  Copy the project ID. You specify this value as the `{project_id}`.
1.  Construct a request URL by using the IDs you copied.

    For example, the following request lists the collections in the project:

    ```sh
    curl -X {request_method} -u "apikey:{apikey}" \
    "{url}/v2/projects/{project_id}/collections?version=2019-11-29 -k"
    ```
    {: codeblock}

## Using the API from Cloud Pak for Data ![Cloud Pak for Data only](images/desktop.png)
{: #api-use-cpd}

This information applies to {{site.data.keyword.discovery-data_short}} only.
{: important}

To use the API, you must construct the URL to use in your requests.

1.  From the {{site.data.keyword.icp4dfull_notm}} web client main menu, expand **Services**, and then click **Instances**.
1.  Find your instance, and then click it to open its summary page.
1.  Scroll to the *Access information* section of the page, and then copy the URL. You will specify this value as the `{url}`.

1.  Copy the bearer token also. You will need to pass the token when you make an API call.
1.  From the launched application instance, go to the **Integrate and Deploy** > **API Information** page.
1.  Copy the project ID. You will specify this value as the `{project_id}`.
1.  Construct a request URL by using the IDs you copied.

    For example, the following request lists the collections in the project:

    ```sh
    curl -H "Authorization: Bearer {token}" \
    "{url}/v2/projects/{project_id}/collections?version=2019-11-29 -k"
    ```
    {: codeblock}

The bearer token that is generated for an administrator can access any instance regardless of the access settings that are configured for the instance.
{: important}
