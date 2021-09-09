---

copyright:
  years: 2019, 2021
lastupdated: "2021-09-09"

keywords: preview link, share link

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

# Previewing your project
{: #preview}

Preview your project and share it with others.
{: shortdesc}

Try out your project and share it with others on your team for testing purposes. A test implementation of your project is created and hosted by IBM. Use this application preview to test your search results. 

To preview and share your project, complete the following steps:

1.  From the **Integrate and Deploy** > **Preview Link** page, follow the instructions to give your team members access to your project. (In Content Mining projects, the page is named **Share Link**.)

    ![IBM Cloud only](images/ibm-cloud.png) **Managed deployments only**: If you want people you invite to be able to invite others, give them *Editor* or *Administrator* platform roles. For more information about access in {{site.data.keyword.cloud_notm}}, see [Setting up access groups](https://cloud.ibm.com/docs/account?topic=account-groups&interface=ui){: external}.
    {: note}

1.  Click the copy icon for the **Copy Link** field to copy the URL of the preview application.

    ![Cloud Pak for Data only](images/desktop.png) **{{site.data.keyword.icp4dfull_notm}}**: When you copy the link for the content mining project, ensure that the URL is similar to the format, `https://{installation-domain}/discovery/{ID}/cm/miner`. If it isn't, refresh the page before you copy the URL.
1.  Paste the URL into a web browser to test it yourself or send the URL to team members.

    Don't forget to send any login credentials that are needed to access the project when you send the link to your colleagues.
 