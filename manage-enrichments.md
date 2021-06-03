---

copyright:
  years: 2020, 2021
lastupdated: "2021-06-03"

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

# Managing enrichments
{: #manage-enrichments}

Apply enrichments to fields in your documents to make meaningful information easier to find and return in searches.
{: shortdesc}

You typically apply enrichments to fields at the time that you create the enrichment. However, you can apply enrichments to fields later. You might want to apply an existing enrichment to a new custom field that you create by using the SDU tool, for example. You can remove enrichments that you applied to fields also.

For more information about available enrichments, see the following topics:

- [Adding domain-specific resources](/docs/discovery-data?topic=discovery-data-domain)
- [Applying prebuilt enrichments](/docs/discovery-data?topic=discovery-data-nlu)

To manage enrichments, complete the following steps:

1.  From the navigation pane, open the **Manage collections** page, and then click a collection to open it. 
1.  Click the **Enrichments** tab.
1.  Find the enrichment that you want to apply or remove.
1.  Click the twistie in the associated field to expand a list of fields.
1.  Do one of the following things:

    - To apply an enrichment to documents, select the field or fields that you want to enrich.

      Do not choose a field that starts with `extracted_metadata`,`enriched_{field_name}`, or `metadata`. You cannot apply enrichments to them. To find out which fields you can apply enrichments to, check the field names that are listed in the *Manage fields* page.
      {: note}
    - To remove an enrichment, clear the checkboxes for fields that you want to remove the enrichment from.
1. Click **Apply changes and reprocess** to apply your changes to the collection.
