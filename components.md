---

copyright:
  years: 2019
lastupdated: "2019-11-27"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'} 
{:url: data-credential-placeholder='url'}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Building and deploying components
{: #deploy}

<!-- c/s help for the *Integrate and deploy* page. Do not delete. -->

The **Integrate and deploy** page in the {{site.data.keyword.discovery-data_long}} can be used to share and deploy your projects. The components available will vary based on your **Project type**.
{: shortdesc}

The code for the {{site.data.keyword.discovery-data_short}} components can be found on [GitHub](https://github.com/watson-developer-cloud/discovery-components){: external}. You can learn more about the components and preview them in [Storybook](https://watson-developer-cloud.github.io/discovery-components/storybook){: external}. 
{: tip}

For all project types:

-  The **Share preview link** or **Share link** tab makes it easy to share your project with others. Follow the instructions to add a user, then send those login credentials and the provided link to your colleague.
-  The **View API information** tab displays the **Project ID** for your project.

## Document Retrieval project components
{: #dr-deploy}

The following components are available on the **Explore UI components** tab:

-  **Search bar** - A search box that uses a natural language understanding query to fetch the most relevant results.
-  **Search results** - A set of results that rank the most relevant passages and tables to a query. 
-  **Facets** - Refine your results with facets that help drill down to specific categories and domains.
-  **Document preview** - Displays your documents in a browser, regardless of the format of the original document. This view makes it easier for you to see search results as highlighted passages within the text of the original document — making the context clearer.
-  **Document preview with Content Intelligence** - (Available only if you have purchased and installed {{site.data.keyword.discovery-data_short}} for Content Intelligence. See [Understanding Discovery for Content Intelligence](/docs/discovery-data?topic=discovery-data-output_schema) for more information.) Displays contract, invoices, or purchase orders in a browser, regardless of the format of the original document. In addition, it recognizes key elements of the documents and gives you the ability to navigate to them quickly. For example, if you are searching for the payment terms clauses in a contract, **Document preview with Content Intelligence** detects those clauses and highlights the passages.


## Conversational Search project components
{: #cs-deploy}

A **Conversational Search** project can be integrated with a {{site.data.keyword.conversationfull}} for {{site.data.keyword.icp4dfull}} search skill to supply answers to a virtual agent. For more information on building a {{site.data.keyword.conversationfull}} search skill, see [Creating a search skill](/docs/assistant-data?topic=assistant-data-skill-search-add).



## Content Mining application
{: #cm-deploy}

You can launch your **Content Mining** application by selecting the **Launch application** tab and clicking the **Launch app** button. For more information about the app, see [Mining content](/docs/discovery-data?topic=discovery-data-contentminerapp).

When you copy the link for the content mining app, ensure that the URL is similar to the format, `https://{installation domain}/discovery/{ID}/cm/miner`. If the URL isn't complete, such as, `/cm/miner`, before copying the link, refresh the page.
{: important}
