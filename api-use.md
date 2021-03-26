---

copyright:
  years: 2015, 2021
lastupdated: "2021-03-26"

subcollection: assistant-data


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Building custom applications with the API
{: #api-use}

Use the {{site.data.keyword.discoveryshort}} API to build a custom application or component that searches your data.
{: shortdesc}

- For {{site.data.keyword.discoveryshort}} API reference documentation, see [API reference](https://cloud.ibm.com/apidocs/discovery-data){: external}.
- For more information about using the Analyze API to process documents without storing them, see [Analyze API](/docs/discovery-data?topic=discovery-data-analyzeapi).
- For more information about using the API to define more complex queries by using the Discovery Query Language, see [Query overview](/docs/discovery-data?topic=discovery-data-query-concepts).

## Getting your project ID ![IBM Cloud only](images/ibm-cloud.png)
{: #api-use-cloud}

This information applies to {{site.data.keyword.cloud_notm}} only.
{: important}

To use many of the API methods, you need your project ID.

1.  Open your project in {{site.data.keyword.discoveryshort}}, and then go to the **Integrate and deploy** > **API Information** page.
1.  Copy the project ID. You must specify this value as the `{project_id}` in your API requests.

## Using the API from Cloud Pak for Data ![Cloud Pak for Data only](images/desktop.png)
{: #api-use-cpd}

This information applies to {{site.data.keyword.discovery-data_short}} only.
{: important}

To use the API, you must construct the URL to use in your requests.

1.  From the {{site.data.keyword.icp4dfull_notm}} web client, go to the details page for the provisioned instance.
1.  Copy the URL from the *Access information* section of the page. You will specify this value as the `{url}`.

    You might want to copy the bearer token also. You will need to pass the token when you make an API call.
1.  From the launched application instance, go to the **Integrate and Deploy** > **API Information** page.
1.  Copy the project ID. You will specify this value as the `{project_id}`.
1.  Construct a request URL by using the IDs you copied. 

    For example, the following request lists the collections in the project:

    ```
    curl -H "Authorization: Bearer {token}" "{url}/v2/projects/{project_id}/collections?version=2019-11-29 -k"
    ```
    {: codeblock}
