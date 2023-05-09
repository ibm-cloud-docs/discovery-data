---

copyright:
  years: 2015, 2023
lastupdated: "2023-05-05"

keywords: api version,api,request syntax,api key,bearer token

subcollection: assistant-data
---

{{site.data.keyword.attribute-definition-list}}

# Building custom applications with the API
{: #api-use}

Use the {{site.data.keyword.discoveryshort}} API to build a custom application or component that searches your data.
{: shortdesc}

## Service API Versioning
{: #apiversioning}

API requests require a version parameter that takes a date in the format `version=YYYY-MM-DD`. Whenever a backwards-incompatible API change occurs, a new minor version of the API is released.

Send the version parameter with every API request. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.

The current version is `2023-03-31`.

## Getting your project ID [IBM Cloud]{: tag-ibm-cloud}
{: #api-use-cloud}

This information applies to {{site.data.keyword.cloud_notm}} only.
{: important}

To use the API, you must construct the URL to use in your requests. Many of the API methods require the project ID.

1.  From the [IBM Cloud Resource list](https://cloud.ibm.com/resources){: external}, expand *AI/Machine Learning*, and then find the service page for your Discovery service instance.
1.  From the *Credentials* section, copy the URL. You specify this value as the `{url}` in your API requests.
1.  While you're on this page, copy the API key. You specify this value as the `{apikey}`.
1.  Open your project in {{site.data.keyword.discoveryshort}}, and then go to the **Integrate and deploy** > **API Information** page.
1.  Copy the project ID. You specify this value as the `{project_id}`.

    If you're using a Content Mining project, stay on the *Share Link* page. From the web browser's *location* field, copy the URL starting with `/projects`. For example, `projects/a8ce5fed-7f33-4405-aa4b-88ffba322712/deploy/beta`. The ID that is specified after the `/projects/` segment of the URL is your project ID.

1.  Construct a request URL by using the IDs you copied.

    For example, the following request lists the collections in the project:

    ```sh
    curl -X {request_method} -u "apikey:{apikey}" \
    "{url}/v2/projects/{project_id}/collections?version=2019-11-29 -k"
    ```
    {: codeblock}

To get the `{collection_id}`, you can use the [List collections](/apidocs/discovery-data#listcollections){: external} API method. Alternatively, open the collection in the product user interface, and then copy the collection ID, which is displayed after the `/collections/` segment of the page URL, from the web browser location field.

## Using the API from Cloud Pak for Data [IBM Cloud Pak for Data]{: tag-cp4d}
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

    If you're using a Content Mining project, stay on the *Share Link* page. From the web browser's *location* field, copy the URL starting with `/projects`. For example, `projects/a8ce5fed-7f33-4405-aa4b-88ffba322712/deploy/beta`. The ID that is specified after the `/projects/` segment of the URL is your project ID.

1.  Construct a request URL by using the IDs you copied.

    For example, the following request lists the collections in the project:

    ```sh
    curl -H "Authorization: Bearer {token}" \
    "{url}/v2/projects/{project_id}/collections?version=2019-11-29 -k"
    ```
    {: codeblock}

The bearer token that is generated for an administrator can access any instance regardless of the access settings that are configured for the instance.
{: important}

The bearer token expires after 12 hours. For more information about customizing the length of a session, see [Setting the idle session timeout](https://www.ibm.com/docs/SSQNUZ_4.6.x/cpd/admin/post-install-session-timeout.html){: external}.

## Next steps
{: #api-use-next}

A developer can make the following enhancements:

- Use the API to [define more complex queries with the Discovery Query Language](/docs/discovery-data?topic=discovery-data-query-dql-overview).
- Specify the exact document to return in response to a specific query with [curations](/docs/discovery-data?topic=discovery-data-curations).
- Process documents without storing them in a collection by [using the Analyze API](/docs/discovery-data?topic=discovery-data-analyzeapi).
