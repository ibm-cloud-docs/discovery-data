---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-28"

keywords: passages, query results

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
{:curl: .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Previewing the default query results
{: #query-results}

See the types of query results that are returned automatically and learn about how they are derived. Understanding how default results are created can help you decide next steps to improve your results.
{: shortdesc}

When a document is ingested, the text is extracted and indexed in the`text` field. When a customer searches a collection at run time, you don't want every word in a 10,000-word document to be returned as the query result. Instead, you want to return a subsection of the text from the original document that contains only information that is relevant to the query. {{site.data.keyword.discoveryshort}} achieves this goal by returning *passages* from the `text` field in all project types except Content Mining. For more information about passages, see [How passages are derived](#query-results-passages).

Preview the default query results.

1.  From the navigation pane, open the **Improve and customize** page.
1.  Take the appropriate action for your project type:

    - **Document Retrieval project**:

      - Click **Run search** for one of the keywords that {{site.data.keyword.discoveryshort}} calculated to have special meaning in your collection.
      - Submit your own phrase or keyword from the search bar.

        You can see that the query results that are returned consist of passages. Entities that are recognized in your documents (based on the Entities enrichment that is applied to the project by default) are displayed as facets by which you can filter the query results.

        If the result text shows `Excerpt unavailable`, the search results might be configured to show a field that doesn't exist in your collection. You can change the results to consist of information from a different field or to switch between showing passages or field content. For more information, see [Changing the result content](#query-results-content).
        {: important}

    - **Conversational Search project**: A single search field is displayed that mimics the user interface of a virtual assistant. 
    
      - Submit a phrase or keyword. 
      
        The query results are returned as passages by default. You can configure the search to return a field instead. See [Changing the result content](#query-results-content).
    - **Custom project**: 
    
      - Submit your own phrase or keyword from the search bar. 
    
        The query results that are returned consist of passages.
    - **Document Retrieval for Contracts project**: Contract-related elements that are recognized in your collection are displayed. 
    
      - Filter the documents by one of the highlighted elements or by entities that are recognized in your documents (based on the Entities enrichment that is applied to the project by default).
      - To view the contract elements in more detail, click a document result to open it. Open the *Contract Data* tab. 
      
      For more information about the elements, see [Understanding contracts](/docs/discovery-data?topic=discovery-data-contracts-schema).
    - **Content Mining project**: 
    
      - Choose a facet by which to filter the documents. 
    
        Facets based on the Parts of Speech enrichment that is applied to the project by default are shown.

    ![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**: The following optional project configuration setting impacts how the query results are formatted:

    - If you enable FAQ extraction, each question-and-answer pair that is found in the original document is added to a new, separate document with the question in the `title` field and answer in the `text` field. By separating the pairs into independent documents, the correct answer can be returned quickly when a phrase that is the same or similar to the associated question is submitted as the query.

      If the results are not useful, try changing the search result content. Set the Search results to use the `text` field. Answers from the FAQ pairs are stored in the `text` field by default.

      If your source document contains 10 question-and-answer pairs, then 10 documents are generated during processing. If you want to see all of the documents that were generated, submit an empty search string.

- If you want to learn more about what information is indexed per document, see [Interpreting the results](/docs/discovery-data?topic=discovery-data-test#test-json).
- For tips on how you can improve the quality of your results, see [Improving your query results](/docs/discovery-data?topic=discovery-data-improvements).

### Changing the result content
{: #query-results-content}

For all project types, you can control where the data comes from that is returned in query results. By default, results consist of passages from the `text` field. The passages that {{site.data.keyword.discoveryshort}} calculates to contain the most relevant information are returned. However, you can change the result content to return content from a field other than the `text` field.

To change the content of the query results, complete the following steps:

1.  From the *Improvement tools* pane, expand **Customize display**, and then click **Search results**.
1.  **Optional**: Change the field that is shown as the title of the query result.

    The title is displayed after the text excerpt. 
    
    This option is not available for *Conversational Search* projects.
    {: note}
1.  Choose **Field** to switch to showing excerpts from a specific field, and then select the field that you want to use as the source of the query result text.
1.  Click **Apply**.

### How passages are derived
{: #query-results-passages}

{{site.data.keyword.discoveryshort}} uses sophisticated algorithms to determine the best passages of text from all of the documents that are returned by a query. Passages are returned per document by default. They are displayed as a section within each document query result and are ordered by passage relevance.

{{site.data.keyword.discoveryshort}} uses sentence boundary detection to pick a passage that includes a full sentence. It searches for passages that have an approximate length of 200 characters, then looks at chunks of content that are twice that length to find passages that contain full sentences. Sentence boundary detection works for all supported languages and uses language-specific logic.

For all project types except *Conversational Search*, you can change how the passages are displayed in the search results from the **Customize display > Search results** page. For example, you can configure the number of passages that are shown per document and the maximum character size per passage.
