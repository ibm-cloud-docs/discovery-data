---

copyright:
  years: 2019, 2022
lastupdated: "2022-11-16"

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
{: summary="This table has row and column headers. The row headers identify supported data sources. The column headers identify the different product deployment options. To understand which data sources are available for your deployment type, go to the row that describes the data source, and find the columns for the type of deployment you're interested in."}

## Project descriptions
{: #projects-reuse}

| Need | Goal | Project type |
|--------------------|------|--------------|
| *Which document contains the answer to my question?* | Find meaningful information in sources that contain a mix of structured and unstructured data, and surface it in a stand-alone enterprise search application or in the search field of a business application. | **Document Retrieval** |
| *Where is the part of the contract that I need for my task?* | Quickly extract critical information from contracts. | **Document Retrieval for Contracts** |
| *I want the chatbot I'm building to use knowledge that I own* | Give a virtual assistant quick access to technical information that is stored in various external data sources and document formats to answer customer questions. | **Conversational Search** |
| *I want to uncover insights I didn't know to ask about.* | Gain insights from pattern analysis or perform root cause analysis. | **Content Mining** |
{: caption="Project type use cases" caption-side="top"}

## Default enrichments per project type
{: #enrichment-defaults-reuse}

Some prebuilt enrichments are applied automatically to collections in a project based on the project type. The following table shows the default enrichments that are applied to each project type.

| Enrichment | Document Retrieval | Document Retrieval for Contracts | Conversational Search | Content Mining |
|------------|--------------------|----------------------------------|-----------------------|----------------|
| Contracts | | ![checkmark icon](../icons/checkmark-icon.svg) | | |
| Entities v2 | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) | | |
| Keywords | | | | |
| Part of Speech | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) | ![checkmark icon](../icons/checkmark-icon.svg) |
| Sentiment of Document | | | | |
| Table Understanding | | ![checkmark icon](../icons/checkmark-icon.svg) | | |
{: row-headers}
{: class="comparison-table"}
{: caption="Default enrichments per project type" caption-side="top"}
{: summary="This table has row and column headers. The row headers identify project types. The column headers identify different enrichments. To understand which enrichments are applied to a project type by default, go to the row that describes the enrichments, and find the columns for the project type that you are interested in."}
