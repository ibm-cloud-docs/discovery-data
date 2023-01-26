---

copyright:
  years: 2015, 2023
lastupdated: "2023-01-26"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Web crawl
{: #connector-web-cloud}

Add a web crawl collection to crawl a website, analyze its page content, and store meaningful information. Specify one or more base web page URLs and configure how many linked pages for the web crawl to follow. You can configure how often to synchronize with the website, so you control how up to date the data in your collection is.
{: shortdesc}

[IBM Cloud]{: tag-ibm-cloud} **{{site.data.keyword.cloud_notm}} only**

This information applies only to managed deployments. For more information about connecting to a website from an installed deployment, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cp4d).
{: note}

## What documents are crawled
{: #connector-web-cloud-objects}

You can connect to the following types of web content:

-   Public websites
-   Private company websites or other sites that require authentication
-   Websites that are behind a corporate firewall

The web crawler can crawl web pages that use JavaScript to render content, but crawler works best on individual pages, not entire websites. It cannot crawl sites that use dynamic URLs; if you can't see any content when you view the source code of a web page in your browser, then the service cannot crawl it.

If you want to crawl a group of URLs that includes some websites that require authentication and some that don't, consider creating a different collection for each authentication type. The connector does not support cookie-based crawling.

During the initial crawl of the content, all website pages that match your search settings are crawled and added to the document index of your collection.

During subsequent scheduled recrawls, a full recrawl is performed and any changes are reflected in your collection. Documents that were added to your collection from website pages that are later deleted from the external website are not deleted from the collection. However, starting with collections that were created after April 2022, when you remove a starting URL from the web crawl configuration, any associated documents are deleted. Deleted documents include indexed documents that were added to the collection based on the content of the web page at the starting URL and documents that were derived from web pages that the starting URL linked to. You cannot limit the number of indexed documents by changing other settings, such as reducing the maximum number of links to follow to 0. Only by deleting the URL can you remove the indexed documents that are associated with it.

All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

The following table illustrates the objects that {{site.data.keyword.discoveryshort}} can crawl.

| Objects that are crawled |
|--------------------------|
| Websites, website subdirectories |
{: caption="Table 1. Data sources crawling support" caption-side="top"}

## Prerequisite step
{: #connector-web-cloud-prereq-task}

If you want to connect to a website that is hosted behind a firewall, set up an {{site.data.keyword.SecureGatewayfull}} connection first.

Valuable content is often stored on your company's internal website. Typically, such intranet websites are accessible only from a computer that is connected to your office network or through a VPN connection. You can establish a persistent and more secure connection between the web crawler and this type of internal site by using {{site.data.keyword.SecureGateway}}.

For more information about how to set up the connection, see [Installing IBM Secure Gateway for on-premises data](/docs/discovery-data?topic=discovery-data-sources#gatewaypublic).

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

    -   If the site you want to crawl requires a login, set **Basic authentication** to `On`, add the URL of the page to the **Starting URL** field, and then click **Add**.

        Add a username and password with access to the site, and then click **Save credentials**. You can specify only one set of credentials per collection.

        For example, you can specify `https://cloud.ibm.com` as the starting URL and add your IBMid as the credentials.

        If you want to start the crawl from a specific section of the site, specify it in the **Starting URLs** field. The domain name of the subsection must match the domain in the URL you specified earlier.

        For example, you might change the starting URL to `https://cloud.ibm.com/unifiedsupport/supportcenter`.

    -   For any public web pages that you want to crawl, add the URL for the root page of the website to the **Starting URLs** field, and then click **Add**. You can add more than one starting page.

        The final forward slash (`/`) in the URL determines the subtree to crawl. If you specify `https://www.example.com/banking/faqs.html`, all URLs that begin with `https://www.example.com/banking/` are crawled, for example. If you specify `https://www.example.com/banking` all URLs that begin with `https://www.example.com/` are crawled.

        By default, the number of consecutive links that the crawl follows from the starting URL is `2`. To change the number of hops or to list website sections to exclude from the crawl, click the edit icon.

        -   The maximum number of hops allowed is `20`.
        -   To specify URL paths to exclude, add the site path. For example, if the starting URL is `https://example.com`, you can exclude `https://example.com/pricing` by entering `/pricing/`. 
      
            Any section of the web address that contains the site path you specify is excluded. For example, if you specify `/licenses/`, the page `https://example.com/products/licenses/europe` is excluded, among others.

        -   If you want to restrict the crawl to a single page, add the URL to the **Starting URLs** field. For example, `https://www.example.com/banking/faqs.html`. Click the edit icon to set the **Maximum number of links to follow** to `0`.

    -   If the website that you want to crawl uses JavaScript to customize the page content before it is displayed, you must take an extra step.

        After you enter the starting URL and click **Add**, edit the URL by clicking the edit icon ![Edit icon](images/web-crawl-edit-url.png). Set the *Execute JavaScript during crawl* switcher to **On**, and then click **Save**.

        When JavaScript processing is enabled, it takes 3 to 4 times longer to crawl a page. Use it only on individual web pages where you know it is necessary because the page renders its content dynamically. If you see timeout messages or the crawl ends without adding content to the collection, decrease the number of web pages that are included in the crawl. For example, you can specify the exact page to crawl in the *Starting URLs* field, and set *Maximum number of links to follow* to 0.
        {: note}

    -   To connect to a website that is hosted behind a firewall, [set up an {{site.data.keyword.SecureGatewayfull}} connection first](#connector-web-cloud-prereq-task).

        Expand *More connection settings*, and then set **Connect to on-premises network** to `On`. Provide details about your {{site.data.keyword.SecureGateway}} connection.

1.  Optional: Add another web address to the **Starting URLs** field.

    The number of starting URLs for a single collection must be less than 100. If you have a requirement to crawl a large number of websites, see [I need to crawl lots of sites. What's my limit?](#connector-web-cloud-max-starting-urls).
    {: important}

    The number of web pages that are crawled is limited to 250,000, so the web crawler might not crawl all the specified websites.

    The number of child URLs per URL that are crawled is limited to 10,000. If the number of child URLs within any crawled URL exceeds 10,000, the crawler cannot process any of the content in the child URLs.

1.  If you want to look for and extract question-and-answer pairs, select **Apply FAQ extraction**.

    For more information, see [FAQ extraction](/docs/discovery-data?topic=discovery-data-sources#faq-extraction).

1.  If you want the web crawl to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.

### I need to crawl lots of sites. What's my limit?
{: #connector-web-cloud-max-starting-urls}

The service can support a total of 500 crawler connections per {{site.data.keyword.discoveryshort}} service instance. All of the data sources except Web crawl use one crawler connection each. For Web crawl, one connection is required for every 5 starting URLs. If you add 10 starting URLS, for example, Discovery generates the extra crawler connection that is needed to support the extra 5 URLs. Therefore, the maximum number of starting URLs that you can use depends on the other data collections that are configured in your service instance. You can calculate the limit yourself.

To calculate the starting URL limit, complete the following steps:

1.  Calculate the number of other data source collections in the service instance, meaning this project and any other projects in the same {{site.data.keyword.discoveryshort}} instance.

    For example, you might have 2 IBM Cloud Object Store collections in one project and 2 Salesforce collections and 1 SharePoint Online collection in another project. In this example, the total number of other data source collections is 5.

1.  Subtract the number of other data source collections from the maximum allowed number of crawler connections, which is 500.

    For example, 500 - 5 = 495.

1.  Multiply the remainder by 5 to determine the total number of starting URLs that you can use.

    For example, 495 x 5 = 2,475.

To use the maximum-allowed number of starting URLs in the example, you would need 25 web crawl collections because each collection allows a maximum of 100 starting URLs to be configured. However, don't configure your instance to use the absolute maximum number allowed. If one or more additional data sources are added subsequently to a project in this service instance, it will impact the number of starting URLs that the instance can crawl successfully.
{: note}

### Troubleshooting crawler issues
{: #connector-web-cloud-ts}

A 403 Forbidden error is returned
:    The website that you want to crawl might block requests from all but a specific set of named entities. If possible, add the crawler to the allowlist for the site. The identifying header for the crawler is `User-Agent: IBM-AppConnect/V1`.
