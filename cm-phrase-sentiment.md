---

copyright:
  years: 2015, 2024
lastupdated: "2023-06-20"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Detecting phrases that express sentiment
{: #cm-phrase-sentiment}

Analyze a document to find phrases that express an opinion or reaction and assess whether the sentiment expressed is positive, neutral, or negative. For English and Japanese, you can also detect specific sentiment targets. The Content Mining application marks these extractions as annotations.
{: shortdesc}

For example, if a product feedback form contains the following sentence, you want to find it and indicate that it is a `positive` statement. 

`I love my XYZ blender...`

What's the difference between phrase and document sentiment?
:    Document sentiment is a built-in Natural Language Processing enrichment that is available for all project types. Document sentiment evaluates the overall sentiment that is expressed in a document to determine whether it is positive, neutral, or negative. Phrase sentiment does the same. However, phrase sentiment can detect and assess multiple opinions in a single document and, in English and Japanese documents, can find specific phrases. For more information about the document sentiment enrichment, see [Sentiment](/docs/discovery-data?topic=discovery-data-nlu#nlu-sentiment).

Complete the following steps to enable phrase sentiment analysis:

1.  From the analysis view of your collection, click the **Collections** breadcrumb link in the page header.
1.  In the tile for your collection, click the *open and close list of options* icon, and then choose **Edit collection**.
1.  Click the **Enrichment** tab, and then select the **Sentiment of phrases** annotator.
1.  Click **Save**, and then click **OK** to verify the change.

    The collection is reindexed. Wait for processing to be completed.
1.  Click **Close** to return to the *Collections* page, and then click your collection tile.
1.  In the *What do you want to analyze?* field, enter a term to search for in your documents or select one or more facets, and then click **Search** to filter the documents.

    The search results are displayed in the mining graph. The *Facet analysis* pane is displayed also. By default, *Relevancy* analysis is shown.
1.  In the drop-down menu from the *Facet analysis* pane, select **Sentiment**. 
1.  In *Target facets* from the *Facet analysis* pane, expand the **Sentiment Analysis** option to see facets that are available for analysis in your documents.
1.  Click a facet to explore.

    For example, if you click **Positive Expression**, you can see the following information:
    
    -  Positive expressions that were identified in your documents
    -  Sentiment percentage
    -  Side-by-side comparison of positive and negative expressions
    -  Number of instances of the expression
    -  Expression relevancy

1.  Click one or more options in the facet list, or select one or both facet lists, and then click **Analyze more**. 

    View the phrase, expression, or target in the *Documents* or *Trends* views.

Text from the body field of the document is analyzed. For more information about which field is used for the body text, see [Identifying the text field](/docs/discovery-data?topic=discovery-data-cm-edit-collection#text-field).
{: note}
