---

copyright:
  years: 2021, 2023
lastupdated: "2023-05-19"

keywords: IAM, add users, share

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Managing IAM access for Discovery
{: #admin}

Share a preview of your search application or build a team to work on a project. You can give team members access to your Discovery service instance through {{site.data.keyword.cloud_notm}}.
{: shortdesc}

[IBM Cloud]{: tag-ibm-cloud}

The information in this topic applies to managed deployments only.
{: important}

Access to {{site.data.keyword.cloud_notm}} service instances is controlled by {{site.data.keyword.cloud}} Identity and Access Management (IAM). Every person who accesses {{site.data.keyword.discoveryshort}} in your account must be assigned an access policy with an IAM role.

Only an owner of the service account can add users. For more information, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).

## Platform roles
{: #admin-platform}

A platform role controls a person's ability to access a service instance in {{site.data.keyword.cloud_notm}}. 

To give someone access to your service instance, assign them any platform role other than *Viewer*. A person with the *Viewer* role cannot access the product user interface. All of the other roles allow users to perform all tasks.

## Service roles 
{: #admin-service}

A service role controls what a person can do in {{site.data.keyword.discoveryshort}}. 

With {{site.data.keyword.discoveryshort}}, anyone who can access a {{site.data.keyword.discoveryshort}} instance can perform all actions. The only limitation is with the *Reader* role; anyone with reader-level access cannot submit API POST requests.
