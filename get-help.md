---

copyright:
  years: 2015, 2023
lastupdated: "2022-06-16"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Getting help
{: #get-help}

Get help to solve issues that you encounter when you use the product.
{: shortdesc}

Use these resources to get answers to your questions:

-   Walk through a guided tour to learn about a project type or a feature. Click **Guided tours** from the page header to see a list of available tours.
-   For answers to frequently asked questions, see the [FAQ](/docs/discovery-data?topic=discovery-data-faqs).
-   Find answers to common questions or ask questions where experts and other community members can answer. Go to the [Watson Discovery Community forum](https://community.ibm.com/community/user/watsonai/communities/community-home?CommunityKey=80650291-2ff4-4a43-9ff8-5188fdb9552f){: external}.

## ![IBM Cloud only](images/ibm-cloud.png)  Contacting IBM Cloud Support for managed deployments
{: #get-help-support-cloud}

Managed deployments are deployments that are hosted on IBM Cloud, including {{site.data.keyword.icp4dfull_notm}} as a Service deployments.

If your service plan covers it, you can get help by opening a case from [IBM Cloud Support](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.

Be ready to share the following information with IBM Support:

### Account information
{: #get-help-support-cloud-account}

-   Account name or customer name.
-   Business impact so IBM Support understands the urgency of the issue and can prioritize it.
-   Case information for any related cases or a parent case.
-   Cloud location where the service instance is hosted (Dallas, Frankfurt, and so on).
-   Your service plan (Plus, Premium and so on).

### Problem description
{: #get-help-support-cloud-description}

-   What outcome were you expecting and what happened?
-   Message text that is displayed when the error occurs, especially the document ID, if specified.
-   Steps to take to reproduce the issue.
-   Any screen captures that illustrate the problem.
-   When did the problem occur?
-   Instance ID. (The instance ID is part of the URL that is specified in the *Credentials* section of the service page on IBM Cloud. You can copy the full URL and provide that.)
-   Collect and share the HTTP archive (HAR) file from your browser. The HAR file contains a log of trace information from within a browser session. It records web requests that are made by the browser to the website page including request and response headers, the body, and the time it takes to load the assets.
-   If you are using the API, share example API calls, including the version parameter value that was specified, and the API response body. 

    Do not share code examples. IBM Support cannot debug custom code.
    {: note}

-   If the problem is related to a particular project or collection, provide the project ID and collection ID.

    -   Project ID. (You can copy the Project ID from the *API Information* tab of the *Integrate and deploy* page in the product user interface.)
    -   Collection ID, if you were able to create a collection. (To get the ID, open the *Manage collections* page, and then click the collection to open it. From the web browser location field, scroll to the end of the URL. Look for the `collections/` section, and then copy the ID that is displayed after it. For example, in the URL `/collections/5a525eb7-b175-3820-0000-017d00f0fcd1/activity`, the collection ID is `5a525eb7-b175-3820-0000-017d00f0fcd1`.)

-   If the problem has to do with documents failing to load, provide the following information if known:

    -   What kind of documents are being uploaded (such as PDF, Json, CSV). Was optical character recognition (OCR) enabled for the collection?
    -   How were the documents loaded into the collection? (using the API, from the product UI, data source connector)
    -   Did you identify fields in the collection by using Smart Document Understanding? If so, what type of SDU model was applied to the collection (user-trained or pretrained)?
    -   What enrichments were applied to the collection?

-   If the problem is related to a particular document (of a small set of documents), provide the `document_id` of the document, if known. You can share example documents if they might be helpful.

-   If the problem is related to querying documents, describe the kind of query being used.

## [IBM Cloud Pak for Data]{: tag-cp4d}  Contacting IBM Support for installed deployments 
{: #get-help-support-cp4d}

Installed deployments are deployment that you provision on {{site.data.keyword.icp4dfull_notm}}.

You can get help by opening a case from IBM Support from [IBM Support](https://www.ibm.com/mysupport/s/topic/0TO50000000IYkUGAW/cloud-pak-for-data){: external}.

Be ready to share the following information with IBM Support:

### Account information
{: #get-help-support-cp4d-account}

-   Account name or customer name.
-   Business impact so IBM Support understands the urgency of the issue and can prioritize it.
-   Case information for any related cases or a parent case.
-   Software versions of both the {{site.data.keyword.discoveryshort}} service version and {{site.data.keyword.icp4dfull_notm}} version.
-   Relevant details about configuration choices that were made during installation and deployment.

### Problem description
{: #get-help-support-cp4d-description}

-   What outcome were you expecting and what happened?
-   Message text that is displayed when the error occurs, especially the document ID, if specified.
-   Steps to take to reproduce the issue.
-   Any screen captures that illustrate the problem.
-   When did the problem occur?
-   Instance ID. (From the IBM Cloud Pak for Data web client main menu, expand *Services*, and then click *Instances*. Find your instance, and open its summary page. Scroll to the *Access information* section of the page, and then copy the URL. The instance ID is part of the URL. You can provide the full URL to IBM Support.)
-   If you are using the API, share example API calls, including the version parameter value that was specified, and the API response body. 

    Do not share code examples. IBM Support cannot debug custom code.
    {: note}
-   Relevant logs, including the Red Hat OpenShift collector logs.

    The IBM Support representative can share a script with you that collects relevant logs from your cluster.

-   If the problem is related to a particular project or collection, provide the project ID and collection ID.

    -   Project ID. (You can copy the Project ID from the *API Information* tab of the *Integrate and deploy* page in the product user interface.)
    -   Collection ID, if you were able to create a collection. (To get the ID, open the *Manage collections* page, and then click the collection to open it. From the web browser location field, scroll to the end of the URL. Look for the `collections/` section, and then copy the ID that is displayed after it. For example, in the URL `/collections/5a525eb7-b175-3820-0000-017d00f0fcd1/activity`, the collection ID is `5a525eb7-b175-3820-0000-017d00f0fcd1`.)

-   If the problem has to do with documents failing to load, provide the following information if known:

    -   What kind of documents are being uploaded (such as PDF, Json, CSV). Was optical character recognition (OCR) enabled for the collection?
    -   How were the documents loaded into the collection? (using the API, from the product UI, data source connector)
    -   Did you identify fields in the collection by using Smart Document Understanding? If so, what type of SDU model was applied to the collection (user-trained or pretrained)?
    -   What enrichments were applied to the collection?

-   If the problem is related to a particular document (of a small set of documents), provide the `document_id` of the document, if known. You can share example documents if they might be helpful.

-   If the problem is related to querying documents, describe the kind of query being used.
