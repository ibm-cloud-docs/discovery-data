---

copyright:
  years: 2021
lastupdated: "2021-09-10"

keywords: IAM, add users, share

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

# Managing IAM access for Discovery
{: #admin}

Share a preview of your search application or build a team to work on a project. You can give team members access to your Discovery service instance through {{site.data.keyword.cloud_notm}}.
{: shortdesc}

![IBM Cloud only](images/ibm-cloud.png) **{{site.data.keyword.cloud_notm}}**

The information in this topic applies to managed deployments only.
{: important}

Access to {{site.data.keyword.cloud_notm}} service instances is controlled by {{site.data.keyword.cloud}} Identity and Access Management (IAM). Every person who accesses Discovery in your account must be assigned an access policy with an IAM role.

Some services also limit the actions that people are allowed to do by using IAM service roles. With Discovery, anyone who can access a Discovery instance can perform all actions.

Only an administrator of the service account can add users. For more information, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).
