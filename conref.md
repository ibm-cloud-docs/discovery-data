---

copyright:
  years: 2019, 2024
lastupdated: "2024-04-10"

subcollection: discovery-data

content-type: conref

---

{{site.data.keyword.attribute-definition-list}}

# Content references for overview subcollection
{: #conref}

## Supported data sources
{: #data-sources-reuse}

The following table shows the supported data sources for each deployment type.

| Data source | IBM Cloud | IBM Cloud Pak for Data |
|-------------|-----------|------------------------|
| Box | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Database (IBM Data Virtualization, IBM Db2, Microsoft SQL, Oracle, Postgres) | | ![checkmark icon](../icons/checkmark-icon.svg) |
| FileNet P8 | | ![checkmark icon](../icons/checkmark-icon.svg) |
| HCL Notes | | ![checkmark icon](../icons/checkmark-icon.svg) |
| IBM Cloud Object Storage | ![checkmark icon](../icons/checkmark-icon.svg) | |
| Local file system | | ![checkmark icon](../icons/checkmark-icon.svg) |
| Salesforce | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Microsoft SharePoint Online | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Microsoft SharePoint On Premises | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Website | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Microsoft Windows file system | | ![checkmark icon](../icons/checkmark-icon.svg) |
{: row-headers}
{: class="comparison-table"}
{: caption="Supported data sources" caption-side="top"}
{: summary="This table has row and column headers. The row headers identify supported data sources. The column headers identify the different product deployment type options. To understand which data sources are available for your deployment type, go to the row that describes the data source, and find the columns for the type of deployment you're interested in."}

## Project descriptions
{: #projects-reuse}

| Need | Goal | Project type |
|--------------------|------|--------------|
| [IBM Cloud]{: tag-ibm-cloud} *I want to extract data to support automation of repetitive document processing tasks.* | I want to understand quickly what data is extracted from my documents and improve the data by applying enrichments.| **Intelligent Document Processing** |
| *Which document contains the answer to my question?* | Find meaningful information in sources that contain a mix of structured and unstructured data, and surface it in a stand-alone enterprise search application or in the search field of a business application. | **Document Retrieval** |
| *Where is the part of the contract that I need for my task?* | Quickly extract critical information from contracts. | **Document Retrieval for Contracts** |
| *I want the chatbot I'm building to use knowledge that I own.* | Give a virtual assistant quick access to technical information that is stored in various external data sources and document formats to answer customer questions. | **Conversational Search** |
| *I want to uncover insights I didn't know to ask about.* | Gain insights from pattern analysis or perform root cause analysis. | **Content Mining** |
{: caption="Project type use cases" caption-side="top"}

## Default enrichments per project type
{: #enrichment-defaults-reuse}

Some prebuilt enrichments are applied automatically to collections in a project based on the project type. The following table shows the default enrichments that are applied to each project type.

| Enrichment | Document Retrieval | Document Retrieval for Contracts | Conversational Search | Content Mining |
|------------|--------------------|----------------------------------|-----------------------|----------------|
| Contracts | | ![checkmark icon](../icons/checkmark-icon.svg) | | |
| Entities | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) | | |
| Keywords | | | | |
| Part of Speech |  |  |  | ![checkmark icon](../icons/checkmark-icon.svg) |
| Sentiment of Document | | | | |
| Table Understanding | | ![checkmark icon](../icons/checkmark-icon.svg) | | |
{: row-headers}
{: class="comparison-table"}
{: caption="Default enrichments per project type" caption-side="top"}
{: summary="This table has row and column headers. The row headers identify project types. The column headers identify different enrichments. To understand which enrichments are applied to a project type by default, go to the row that describes the enrichments, and find the columns for the project type that you are interested in."}

## Basic project defaults
{: #project-defaults-reuse}

Some enrichments and query result settings are applied to each project type by default.

| Project type | Default enrichments | Default query result settings |
|--------------|---------------------|-------------------------------|
| [IBM Cloud]{: tag-ibm-cloud} Intelligent Document Processing | Entities | Facets (by Entity), Passages |
| Document Retrieval | Entities | Facets (by Entity), Passages |
| Document Retrieval for Contracts | Entities, Table Understanding, and Contracts | Facets (by Category, Nature, Contract Term, Contract Payment Term, Contract Type, Contract Currency, Invoice Buyer, Invoice supplier, Invoice Currency, Purchase Order Buyer, Purchase Order Supplier, Purchase Order Payment Term) and Table Retrieval |
| Conversational Search | None | Passages |
| Content Mining | Part of Speech | None |
| Custom | None | Passages |
{: caption="Basic project defaults" caption-side="top"}

## Webhook security
{: #webhook-security-reuse}

To authenticate the webhook request, verify the JSON Web Token (JWT) that is sent with the request. The webhook microservice automatically generates a JWT and sends it in the `Authorization` header with each webhook call. It is your responsibility to add code to the external service that verifies the JWT.

The system can generate a JWT based on the `sample secret` that you specify, and in the `Authorization` header, you can pass this system-generated JWT to the external application. If you specify a value in the `header`, then the webhook microservice sends that value to the external application instead of the JWT.
{: note}

For example, if you specify `sample secret` in the `Secret` field of the Webhooks object in the [Create collection](https://{DomainName}/apidocs/discovery-data#createcollection){: external} or [update collection](https://{DomainName}/apidocs/discovery-data#updatecollection){: external} APIs, you might add sample code such as the following in Node.js:

```sh
const jwt = require('jsonwebtoken');
...
const token = request.headers.authentication; // grab the "Authentication" header
try {
  const decoded = jwt.verify(token, 'sample secret');
} catch(err) {
  // error thrown if token is invalid
}
```
{: codeblock}

## Data model of the `ping` event
{: #ping-event-reuse}

Following are the `ping` event parameters:

| Parameter | Description |
|-----------|----------------------|
| `event` | The event name is `ping`. |
| `instance_id` | The {{site.data.keyword.discoveryshort}} instance ID. |
| `version` | The {{site.data.keyword.discoveryshort}} API version in the format `yyyy-mm-dd`. |
| `data` | An object with the event information: `url`, `events`, and `metadata`.  \n  \n  - `url`: The configured webhook endpoint (URL).  \n  \n  - `events`: An array of event string values. The events in this array are sent to the webhook URL.  \n  \n  - `metadata`: An object with information that is specific to the created webhook.|
| `created_at` | The date and time the event was created. |
{: caption="Ping event" caption-side="top"}
