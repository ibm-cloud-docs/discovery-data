---

copyright:
  years: 2019, 2025
lastupdated: "2025-02-13"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Web crawl
{: #connector-web-cp4d}

Crawl a website. You can crawl public websites and websites that require authentication.
{: shortdesc}

[IBM Cloud Pak for Data]{: tag-cp4d} [IBM Software Hub]{: tag-teal}

This information applies only to installed deployments. For more information about crawling a website from a managed deployment, see [Web crawl](/docs/discovery-data?topic=discovery-data-connector-web-cloud).
{: note}

## What documents are crawled
{: #connector-web-cp4d-docs}

-   The website content is processed as HTML files.
-   The web crawler does not crawl dynamic websites that use JavaScript to render content. You can confirm the use of JavaScript by viewing the source code of the website in your browser.
-   When a source is recrawled, new documents are added, updated documents are modified to the current version, and deleted documents are deleted from the collection's index during refresh.
-   All {{site.data.keyword.discoveryshort}} data source connectors are read-only. Regardless of the permissions that are granted to the crawl account, {{site.data.keyword.discoveryshort}} never writes, updates, or deletes any content in the original data source.

## Prerequisite step
{: #connector-web-cp4d-prereq}

If you want to connect to a web site that requires authentication, you need to know the authentication credentials that are required to access the site.

-   For a website that requires basic authentication, get the following information:

    Username
    :   The username of a user with access to the content that you want to connect to on the website.
    
    Password
    :   The password that is associated with the username.

-   For a website that requires Windows NT LAN Manager (NTLM) authentication, get the following information:

    Username
    :   The username of a user with access to the content that you want to connect to on the website.

    Password
    :   The password that is associated with the username.

    NTLM domain name
    :   The NTLM domain name of the user that is authenticating with the site.

    NTLM host name
    :   The hostname of the NTLM server.

-   For a website that requires form-based authentication, choose how you want to access the site from the following options:

    -   Direct access: Submits the form without getting the login page.

        Form action URL
        :   The URL to send the form data to when the form is submitted. For example, `/action_page.php`.

        Required fields
        :   Find out the field values that must be provided in the form.

    -   Indirect access: Fetches the login page and fills in the form fields. Make a note of the following information so you can provide it later:

        Form login URL
        :   URL of the website's login page.

        Form name
        :   Name of the login form.

        Required fields
        :   Find out the field values that must be provided in the login form.

## Connecting to a web crawl data source
{: #connector-web-cp4d-task}

If you want to crawl a group of URLs that includes some websites that require authentication and some that don't, consider creating a different collection for each authentication type.

From your {{site.data.keyword.discoveryshort}} project, complete the following steps:

1.  From the navigation pane, choose **Manage collections**.
1.  Click **New collection**.
1.  Click **Web crawl**, and then click **Next**.
1.  Name the collection.
1.  If the language of the website is not English, select the appropriate language.

    For a list of supported languages, see [Language support](/docs/discovery-data?topic=discovery-data-language-support).
1.  **Optional**: Change the synchronization schedule.

    The Web crawl data source is designed to be used with websites that change only once or twice a week. To ensure that your collection captures all website updates, schedule the crawl to occur weekly.
    {: tip}

    For more information, see [Crawl schedule options](/docs/discovery-data?topic=discovery-data-collections#crawlschedule).
1.  In the *Specify where you want to crawl* section, add the website URL to the **Starting URLs** field, and then click **Add**. Continue adding starting URLs.

    The URLs where the crawler begins crawling. By default, the web crawl can crawl subtrees, and URLs can be crawled from the path that is supplied in the seed only. Use the full URL, for example `http://www.example.com/`. The start URL in the web crawl has two limitations as to what is crawled:

    -   It crawls the same domain name as the start URL.
    -   It crawls all URL content up to and including the last slash (`/`) in **Starting URLs**. If your start URL has a subtree, the web crawl does not crawl that subtree, unless you specify its URL in **Starting URLs**.

1.  **If the URL starts with HTTPS**: In the *Advanced Configuration* section, set the **Ignore certificate** switcher to **On** to ignore any SSL certificates on the target website.

1.  **Optional**: Click **Authentication settings** to specify the authentication type to apply to one or more of the starting URLs:

    -   Choose the starting URL.
    -   Choose the authentication type from the following options:

        -   Basic authentication
        -   NTLM authentication
        -   FORM authentication

    -   For **Basic authentication**, provide the following details:

        Username
        :   The username of a user with access to the content that you want to connect to on the website.

        Password
        :   The password that is associated with the user.

    -   For **NTLM authentication**, provide the following details:

        Username
        :    The username of a user with access to the content that you want to connect to on the website.

        Password
        :   The password that is associated with the user.

        NTLM domain name
        :   The NTLM domain name that belongs to the user who is authenticating.

        NTLM host name
        :   The hostname of the NTLM server.

    -   For **FORM authentication**, provide the following details:

        -   In **Form type**, select one of the following options:

            Direct
            :   Click this option if you do not want to fetch the login page.

            Indirect
            :   Click this option if you want to fetch the login page and you want to fill the parameters in the login form.

        -   Complete the following fields if you choose Direct:

            Form action url
            :   The form action URL that is required to submit the form.

            Form method
            :   Specify **GET**.

        -   Complete the following fields if you choose Indirect:

            Form login url
            :   This field is required if you select the **Indirect** form type.

            Form name
            :   This field is required if you select the **Indirect** form type.

            Form method
            :   Specify **POST**.

        -   In the *Form parameters* section, list of the key-value pairs of form parameters.

            Complete the **Key** and **Value** fields, and then click **+** to add one or more form parameters.
1.  **Optional**: If you are using a proxy server to access the data source server, then in the *Proxy settings* section, set the **Enable proxy settings** switch to `On`. Add values to the following fields:

    Username
    :   The proxy server username to use to authenticate with the proxy server if the proxy server requires authentication.

    Password
    :   The proxy server password to use to authenticate with the proxy server if the proxy server requires authentication.

    Proxy server domains
    :   The domain or domains that the hosts reside in. You can specify a wildcard in this field, such as an asterisk (`*`) to crawl all domains or a leading asterisk (`*.server1.bar.com`) to crawl domains that match a pattern.

    Proxy server host name or IP address
    :   The hostname if you want to access the server by using a LAN, or the IP address of the server that you want to use as the proxy server.

    Proxy server port number
    :   The network port that you want to connect to on the proxy server.

1. **Optional**: Complete the following fields in *Advanced Configuration*:

    Code page to use
    :   Specify the character encoding of the website pages. If unspecified, the default value of `UTF-8` is used.

        If you are crawling Chinese websites, specify `UTF-8`.
        {: tip}

    URL Path Depth
    :   The level of site paths to crawl. 
    
        For example, if you specify the starting URL of `https://www.example.com` and a path depth of `4`, then the crawler will access the page `https://www.example.com/some/more/examples/index.html`, which is located at a path that is four levels away from the root URL. 
      
        You can enter a positive value only. If unspecified, the default value is `5`. The maximum path depth allowed is `20`.

    Maximum hops
    :   The number of consecutive links to follow from the start URL. 
    
        If unspecified, the default value is `5`. The maximum number of links that the crawler can follow is `20`. To not allow any hops, enter `0`.

    Ignore robots.txt
    :   Enable this setting if you want the crawler to ignore the allow and deny rules that are outlined by the website in its robots.txt file. 
    
        Keep in mind that sites typically use the file to improve crawl results. For example, they might use the robots.txt file to prevent duplicate information from being crawled, to prevent draft content from being read, or to delay crawling so as not to overload their site.

    Rules to crawl domain
    :   Specify the domain names that you want to either allow or forbid the crawler to crawl. 
    
        Domain names are case sensitive and the wildcard character (*) can occur anywhere in the domain name.

        The order of the rules is significant. The crawler applies the first rule that matches a candidate URL. The default rule, forbid domain *, forbids all Web crawling and must occur last in the list of domain rules.

        You can define the following types of rules, for example:

        -   To exclude the entire ibm.com domain:

            ```text
            forbid domain www.ibm.com
            ```
            {: codeblock}

        -   To crawl any domain that ends with `ibm.com`: 
      
            ```text
            allow domain *.ibm.com
            ```
            {: codeblock}

        -   To crawl only port `443` on IBM domains that begin with `server`: 
      
            ```text
            allow domain server*.ibm.com:443
            ```
            {: codeblock}
    
    Rules to crawl URL prefixes
    :   Specify the HTTP and HTTPS prefixes that you want to either allow or forbid the crawler to crawl. 
    
        The wildcard character (*) can occur one or more times in the URL.

        The order of the rules is significant. The crawler applies the first rule that matches a candidate URL.

        You can define the following types of rules, for example:

        -   To crawl pages in the public directory on this domain: 
      
            ```text
            allow prefix http://*.ibm.com/public/*
            ```
            {: codeblock}

        -   To exclude all other directories on this domain:
      
            ```text
            forbid prefix http://*.ibm.com/*
            ```
            {: codeblock}

    Advanced crawler properties
    :   Only use when instructed to do so by IBM Support.

1.  **Optional**: If you want to ignore any SSL certificates on the target website, set the **Ignore certificate** switch to `On`.

    This option applies to HTTPS URLs only.
1.  If you want the crawler to extract text from images on the site, expand *More processing settings*, and set **Apply optical character recognition (OCR)** to `On`.

    When OCR is enabled and your documents contain images, processing takes longer. For more information, see [Optical character recognition](/docs/discovery-data?topic=discovery-data-collections#ocr).
    {: note}

1.  Click **Finish**.

The collection is created quickly. It takes more time for the data to be processed as it is added to the collection.

If you want to check the progress, go to the Activity page. From the navigation pane, click **Manage collections**, and then click to open the collection.
