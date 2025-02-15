---

copyright:
  years: 2019, 2025
lastupdated: "2023-03-23"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Start getting value from your data
{: #product-overview}

Learn what {{site.data.keyword.discoveryfull}} can do to help you find answers, recognize patterns, and gain insights from your data.
{: shortdesc}

Find checklists of the high-level steps to follow to achieve the following goals:

- [Pinpoint answers](#product-overview-answers)
- [Extract meaning](#product-overview-enrich)
- [Enhance your chatbot](#product-overview-chat)
- [Find trends](#product-overview-mining)
- [Analyze contracts](#product-overview-contracts)

## Pinpoint answers
{: #product-overview-answers}

Help customers find answers faster. Analyze content from various connected data sources, pinpoint the most relevant passage or phrase, and return the right information when someone asks for it.

![Shows the search bar with search results after it.](images/dr-search.png){: caption="Search bar with search results" caption-side="bottom"}

If pinpointing answers is your goal, complete the steps that are listed in the following table.

| Step |  Task | Related information |
|------|-------|---------------------|
| ![checkbox](images/checkbox.png) | Create a *Document Retrieval* project. | [Creating projects](/docs/discovery-data?topic=discovery-data-projects) |
| ![checkbox](images/checkbox.png) | Add up to 5 collections that connect to external data sources or contain uploaded files. | [Creating collections](/docs/discovery-data?topic=discovery-data-collections) |
| ![checkbox](images/checkbox.png) | Run test queries to assess the quality of the initial results. | [Previewing the default query results](/docs/discovery-data?topic=discovery-data-query-results) |
| ![checkbox](images/checkbox.png) | Take actions to improve your results. For example, you can customize the search bar to enable autocompletion. | [Improving your query results](/docs/discovery-data?topic=discovery-data-improvements) |
| ![checkbox](images/checkbox.png) | Deploy your search solution. | [Deploying your project](/docs/discovery-data?topic=discovery-data-deploy) |
{: caption="Checklist for getting answers" caption-side="top"}

## Extract meaning
{: #product-overview-enrich}

Use award-winning natural language processing technology to enrich your data and ensure that the right information is found when someone searches for answers.

![Shows a custom machine learning facet.](images/nlu-search.png){: caption="Machine learning facet for filtering search results with custom enrichment values" caption-side="bottom"}

If extracting meaning is your goal, complete the steps that are listed in the following table.

| Step | Task | Related information |
|------|------|---------------------|
| ![checkbox](images/checkbox.png) | Create any project type. | [Creating projects](/docs/discovery-data?topic=discovery-data-projects) |
| ![checkbox](images/checkbox.png) | Add collections that connect to external data sources or contain uploaded files. | [Creating collections](/docs/discovery-data?topic=discovery-data-collections) |
| ![checkbox](images/checkbox.png) | Chunk large documents into many smaller documents so you can apply more targeted enrichments to the content. | [Using Smart Document Understanding](/docs/discovery-data?topic=discovery-data-configuring-fields) |
| ![checkbox](images/checkbox.png) | Enhance your data by applying built-in NLU enrichments. | [Applying prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu) |
| ![checkbox](images/checkbox.png) | Identify and promote terms and patterns from your data with special significance to your use case. | [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain) |
| ![checkbox](images/checkbox.png) | Submit test queries to assess the results. | [Testing your project](/docs/discovery-data?topic=discovery-data-test) |
| ![checkbox](images/checkbox.png) | Create a facet that surfaces the enriched data from your documents. | [Facets](/docs/discovery-data?topic=discovery-data-facets) |
| ![checkbox](images/checkbox.png) | Take actions to improve your results. | [Improving your query results](/docs/discovery-data?topic=discovery-data-improvements) |
| ![checkbox](images/checkbox.png) | Deploy your solution. | [Deploying your project](/docs/discovery-data?topic=discovery-data-deploy) |
{: caption="Checklist for extracting meaning" caption-side="top"}

## Enhance your chatbot
{: #product-overview-chat}

Delight your customers by fortifying your chatbot with an answer to every question. Discovery is designed to work seemlessly with {{site.data.keyword.conversationshort}} to search and deliver answers from help content that you already own.

![Shows a chat bot with emphasize the answer enabled.](images/convo-search.png){: caption="Answer finding enabled in the {{site.data.keyword.conversationshort}} web chat" caption-side="bottom"}

If enhancing your chatbot is your goal, complete the steps that are listed in the following table.

| Step | Task | Related information |
|------|------|---------------------|
| ![checkbox](images/checkbox.png) | Create a *Conversational Search* project. | [Creating projects](/docs/discovery-data?topic=discovery-data-projects) |
| ![checkbox](images/checkbox.png) | Add a collection that connects to an external data source or contains uploaded files. | [Creating collections](/docs/discovery-data?topic=discovery-data-collections) |
| ![checkbox](images/checkbox.png) | Run test queries to assess the quality of the initial results. | [Previewing the default query results](/docs/discovery-data?topic=discovery-data-query-results) |
| ![checkbox](images/checkbox.png) | Take actions to improve your results. | [Improving your query results](/docs/discovery-data?topic=discovery-data-improvements) |
| ![checkbox](images/checkbox.png) | Connect your project to a virtual assistant that is built with Watson Assistant. | [Deploying your project](/docs/discovery-data?topic=discovery-data-deploy) |
| ![checkbox](images/checkbox.png) | From the Watson Assistant user interface, deploy the web chat that is associated with your assistant. | [Deploying your assistant](/docs/watson-assistant?topic=watson-assistant-web-chat-overview){: external} |
{: caption="Checklist for enhancing your chatbot" caption-side="top"}

For a more detailed look at these steps, take a tutorial that walks you through them. For more information, see [Power your assistant with answers from web resources](/docs/discovery-data?topic=discovery-data-tutorial-assistant-fred).

Alternatively, you can add a generative language service named NeuralSeek between the Watson {{site.data.keyword.discoveryshort}} and {{site.data.keyword.conversationshort}} services. For more information, see [Use NeuralSeek to return polished answers from existing help content](/docs/watson-assistant?topic=watson-assistant-tutorial-neuralseek){: external}.

## Find trends
{: #product-overview-mining}

Uncover patterns, trends, and relationships in structured and unstructured data. Use text analytics to gain insights into social media, e-commerce trends, and user behavior. Or start to address problems by finding their root cause.

Only users of installed deployments or Premium or Enterprise plan-managed deployments can create this type of project.
{: note}

![Shows the content mining application user interface.](images/mining-search.png){: caption="Analyzing data with the Content Mining application" caption-side="bottom"}

If finding trends in your data is your goal, complete the steps that are listed in the following table.

| Step | Task | Related information |
|------|------|---------------------|
| ![checkbox](images/checkbox.png) | Create a *Content Mining* project. | [Creating projects](/docs/discovery-data?topic=discovery-data-projects) |
| ![checkbox](images/checkbox.png) | Add a collection that connects to an external data source or contains uploaded files. | [Creating collections](/docs/discovery-data?topic=discovery-data-collections) |
| ![checkbox](images/checkbox.png) | Use the built-in Content mining application to analyze your data. | [Analyzing your data with the content mining application](/docs/discovery-data?topic=discovery-data-contentminerapp) |
{: caption="Checklist for finding trends" caption-side="top"}

## Analyze contracts
{: #product-overview-contracts}

Accelerate the pace at which experts can analyze complex documents.

Only users of installed deployments or Premium or Enterprise plan-managed deployments can create this type of project.
{: note}

![Shows the Contract Info tab for a contract document query result.](images/contract-search.png){: caption="Analyzing contracts" caption-side="bottom"}

If analyzing contracts is your goal, complete the steps that are listed in the following table.

| Step | Task | Related information |
|------|------|---------------------|
| ![checkbox](images/checkbox.png) | Create a *Document Retrieval for Contracts* project. | [Creating projects](/docs/discovery-data?topic=discovery-data-projects) |
| ![checkbox](images/checkbox.png) | Add up to 5 collections that connect to external data sources or contain uploaded files. | [Creating collections](/docs/discovery-data?topic=discovery-data-collections) |
| ![checkbox](images/checkbox.png) | Run test queries to assess the quality of the initial results. | [Previewing the default query results](/docs/discovery-data?topic=discovery-data-query-results) |
| ![checkbox](images/checkbox.png) | Take actions to improve your results. | [Improving your query results](/docs/discovery-data?topic=discovery-data-improvements) |
| ![checkbox](images/checkbox.png) | Analyze the data. | [Understanding contracts](/docs/discovery-data?topic=discovery-data-contracts-schema) |
{: caption="Checklist for analyzing contracts" caption-side="top"}
