---

copyright:
  years: 2015, 2021
lastupdated: "2021-06-15"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:beta: .beta}
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

# Web crawl
{: #connector-web-cloud}

Add a web crawl collection to crawl a website, analyze its page content, and store meaningful information. Specify one or more base web page URLs and configure how many linked pages for the web crawl to follow. You can configure how often to synchronize with the website, so you control how up to date the data in your collection is.
{: shortdesc}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments. For more information about connecting to a website from an installed deployment, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cp4d).
{: note}

## What documents are crawled
{: #connector-web-cloud-objects}

You can connect to the following types of web content:

- Public websites
- Private company websites or other sites that require authentication
- Websites that are behind a corporate firewall

The web crawler does not crawl dynamic websites that use JavaScript to render content. You can confirm the use of JavaScript by viewing the source code of the website in your browser.
{: note}

If you want to crawl a group of URLs that includes some websites that require authentication and some that don't, consider creating a different collection for each authentication type.

During the initial crawl of the content, all website pages that match your search settings are crawled and added to the document index of your collection.

During subsequent scheduled recrawls, a full recrawl is performed and any changes are reflected in your collection. Documents that were added to your collection from website pages that are later deleted from the site are not deleted from the collection.

All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

The following table illustrates the objects that {{site.data.keyword.discoveryshort}} can crawl.

| Data source | Objects that are crawled |
|-------------|--------------------------|
| Web crawl | Websites, website subdirectories |
{: caption="Table 1. Data sources crawling support" caption-side="top"}

## Prerequisite step
{: #connector-web-cloud-prereq-task}

If you want to connect to a website that is hosted behind a firewall, set up an {{site.data.keyword.SecureGatewayfull}} connection first.
    
Valuable content is often stored on your company's internal website. Typically, such intranet websites are accessible only from a computer that is connected to your office network or through a VPN connection. You can establish a persistent and more secure connection between the web crawler and this type of internal site by using {{site.data.keyword.SecureGateway}}.
    
For more information about how to set up the connection, see [Installing IBM Secure Gateway for on-premises data](#gatewaypublic). 

## Connecting to the data source
{: #connector-web-cloud-task}

To configure the web crawl collection, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Web crawl**, and then click **Next**.
1.  Name the collection.
1.  If the language of the content on the website is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: You can change the synchronization schedule. 

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  Specify the URL of the website that you want to crawl.

    - If the site you want to crawl requires a login, set **Basic authentication** to `On`, add the URL of the page to the **Starting URL** field, and then click **Add**.

      Add a username and password with access to the site, and then click **Save credentials**. You can specify only one set of credentials per collection.

      For example, you can specify `https://cloud.ibm.com` as the starting URL and add your IBMid as the credentials.
      
      If you want to start the crawl from a specific section of the site, specify it in the **Starting URLs** field. The domain name of the subsection must match the domain in the URL you specified earlier.

      For example, you might change the starting URL to `https://cloud.ibm.com/unifiedsupport/supportcenter`.
    - For any public web pages that you want to crawl, add the URL for the root page of the website to the **Starting URLs** field, and then click **Add**.

      You can add more than one starting page for public websites.

      The final forward slash (`/`) in the URL determines the subtree to crawl. If you specify `https://www.example.com/banking/faqs.html`, all URLs that begin with `https://www.example.com/banking/` are crawled, for example. If you specify `https://www.example.com/banking` all URLs that begin with `https://www.example.com/` are crawled.

      By default, the number of consecutive links that the crawl follows from the starting URL is `2`. To change the number of hops or to list website sections to exclude from the crawl, click the edit icon. 
      
      - The maximum number of hops allowed is `20`. 
      - To specify URL paths to exclude, add the site path. For example, if the starting URL is `https://example.com`, you can exclude `https://example.com/licenses` and `https://example.com/pricing` by entering `/licenses/, /pricing/`. 
      - If you want to restrict the crawl to a single page, add the URL to the **Starting URLs** field. For example, `https://www.example.com/banking/faqs.html`. Click the edit icon to set the **Maximum number of links to follow** to `0`.

      The number of web pages that are crawled is limited to 250,000, so the web crawler might not crawl all the specified websites.

      The number of child URLs per URL that are crawled is limited to 10,000. If the number of child URLs within any crawled URL exceeds 10,000, the crawler cannot process any of the content in the child URLs.

    - To connect to a website that is hosted behind a firewall, [set up an {{site.data.keyword.SecureGatewayfull}} connection first](#connector-web-cloud-prereq-task).
    
      Expand *More connection settings*, and then set **Connect to on-premise network** to `On`. Provide details about your {{site.data.keyword.SecureGateway}} connection.

1.  If you want to look for and extract question-and-answer pairs, select **Apply FAQ extraction**.

    For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction).

1.  If you want the web crawl to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    The processing time increases when this feature is enabled.
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection. 

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.