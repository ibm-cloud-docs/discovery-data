---

copyright:
  years: 2015, 2022
lastupdated: "2022-07-22"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Analyze your data ![Enterprise plan](images/enterprise.png) ![Premium plan](images/premium.png) ![Cloud Pak for Data](images/cp4d.png)
{: #contentminerapp}

Analyze your data to find patterns, trends, and anomalies.
{: shortdesc}

Only users of installed deployments ({{site.data.keyword.icp4dfull_notm}}) or Enterprise and Premium plan managed deployments can use the Content Mining application.
{: note}

## Overview video
{: #cmvideo}

![IBM Watson Discovery Content Mining](https://www.kaltura.com/p/1773841/sp/177384100/embedIframeJs/uiconf_id/27941801/partner_id/1773841?iframeembed=true&entry_id=1_7m4thupw){: video output="iframe" data-script="#video-transcript-ui" id="mediacenterplayer" frameborder="0" width="560" height="315" allowfullscreen webkitallowfullscreen mozAllowFullScreen}

### Video transcript
{: #video-transcript-ui}
{: notoc}

Watson Discovery Content Mining Project presented by Stuart Strolin. (Music intro) The purpose of this video is to familiarize you with the content mining project in Watson Discovery.

Content mining is one of the primary use cases for Watson Discovery and is used for analyzing and exploring both structured and unstructured data to find insights and extract hidden meaning. It is used by both the citizen analyst and the data scientist.

The content mining project can be used for all types of analysis because the user interface is not specific to a particular industry or set of data.

In this scenario, you are an analyst for a fictitious automobile company. Operational reports have alerted the company to an unusual accident rate for one of their cars. Your job is to find out why.

Using the content mining project, you begin your analysis by looking at the unstructured data from the national motor vehicle incident reports. You are presented with an interface that allows you to select the car model and begin your analysis (on the Collections page). In this case, you are interested in the Hill Walker. You could type that information into the search section at the top of the page. But it's easier just to click on the item. You can add as many search terms and conditions as you like. But in reality, you want to let the application guide your analysis.

What you see now is the navigation view (in Guided mode). It keeps track of your analysis and provides options for next steps. It also provides a count of the number of documents that match your current state of analysis. In this small collection, the number of documents relating to the Hill Walker is only 51. In a production data set, the number would usually be much larger. Analyzing trends and anomalies is often a good way to start as it allows you to see if anything seems out of the ordinary.

Immediately, you notice that the Hill Walker has problems in December and January. You decide to investigate further by narrowing this initial exploration to just the month of December.

Notice how the navigation view at the top always keep you informed of where you are in your analysis. Next, you select 'Analyze cause and characteristics' because you are interested in why things are happening.

You notice that words like 'snow' and 'brake' are highlighted together (in the Part of Speech section), so you add these to your analysis.

The Content Miner project has narrowed your investigation to a small number of complaints that can be easily read. (clicks Show Documents)

The common theme here is that there is an unexpected problem with the way the brakes are working in snowy conditions. You now have the information you need to ask the engineering department to perform a detailed inspection of the braking system and determine why it is not working as expected in snowy conditions.

In this demonstration, you saw how a citizen analyst using Watson Discovery and content mining can easily discover hidden meaning in unstructured text. (list of features, functionality, and use cases)

What will you do with Watson Discovery? (Music outro)

## How it works
{: cm-explained}

To analyze your data, you use *facets*. Facets give you a way to slice your data and visualize a subset of information so it is easier to comprehend. 

When you create a *Content Mining* project type, the *Part of Speech* facet is applied to your data automatically. This facet is a great place to start because it is valid for all data, no matter the subject. The output gives you a quick look at the terminology that is most common in the data. 

![Watson Discovery content mining launch page](images/miningloginapp.png "Content mining app initial launch page that asks you what you want to analyze"){: caption="Figure 1. The Discovery Content Mining application showing the page you see after launching the app" caption-side="bottom"}

From this starting point, you can determine other ways to filter the data that might be useful. 

If your data consists of traffic reports, for example, the *Part of Speech* facet might show that high frequency keywords include terms such as *engine*, *brake*, *fire*, *smoke*, and *spark*. Given this common terminology, you can create dictionaries to help you categorize and filter the data. The keywords from the example might lead you to create the following dictionaries:

-   *`component`* dictionary for terms such as engine and brake
-   *`phenomenon`* dictionary for terms such as fire, smoke, and spark

When you apply the dictionary enrichment to your data, it generates *annotations*. You can think of annotations as tags that you add to words or phrases, where the tag categorizes or identifies the meaning of the word or phrase. 
The resulting annotations function as new facets that you can use to filter and dissect your data further. 

With your new *`component`* and *`phenomenon`* facets, for example, you can look for correlations between components and phenomena that are involved in traffic incidents.

## Digging deeper
{: cm-deeper}

To dig even deeper into your data, apply or create AI models that can find different types of information in your documents. You can apply built-in natural language processing models, such as the *Entities* enrichment that can recognize mentions of commonly known things, such as business or location names and other types of proper nouns. Or you can apply a custom model that recognizes terms and categories that are unique to your data.

-   [Learn about the ways that you can analyze your data](/docs/discovery-data?topic=discovery-data-cm-analyze-data).
-   [Extend your analysis by adding your own facets](/docs/discovery-data?topic=discovery-data-cm-add-facets).
-   [Share what you learn by generating reports](/docs/discovery-data?topic=discovery-data-cm-report).

## Getting started
{: #cmstart}

Before you can use the application, you must create a {{site.data.keyword.discoveryshort}} Content Mining project. After the project is created and data is uploaded, you can open the Content Mining application. For more information, see [Creating projects](/docs/discovery-data?topic=discovery-data-projects).

You can't get out useful insights if you don't put the right type of information in. Be sure to include consistent data. If you want to find trends over time, your data must include data points that specify a date. 

Data that is submitted in CSV file format is optimal. For a sample of a CSV file that provides interesting analysis capabilities, see [Analyzing CSV files](/docs/discovery-data?topic=discovery-data-cm-csv-file). When you start with structured data, such as records in a CSV file, facets are created automatically from the fields in your documents. To view these domain-specific facets, switch the *Facets* view to show **Metadata facets**.
