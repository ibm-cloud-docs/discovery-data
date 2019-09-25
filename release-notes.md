---

copyright:
  years: 2019
lastupdated: "2019-08-30"

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Release notes
{: #release-notes}

The release notes provide information about changes to {{site.data.keyword.discovery-data_long}} since the previous release.
{: shortdesc}

## Service API Versioning
{: #apiversioning}

API requests require a version parameter that takes a date in the format `version=YYYY-MM-DD`. Whenever we change the API in a backwards-incompatible way, we release a new minor version of the API.

Send the version parameter with every API request. The service uses the API version for the date you specify, or the most recent version before that date. Don't default to the current date. Instead, specify a date that matches a version that is compatible with your app, and don't change it until your app is ready for a later version.

The current version is `2019-06-28`.

## Beta features
{: #beta-features}

IBM releases services, features, and language support for your evaluation that are classified as beta. These features might be unstable, might change frequently, and might be discontinued with short notice. Beta features also might not provide the same level of performance or compatibility that generally available features provide and are not intended for use in a production environment. Beta features are supported only on the [IBM Developer Answers](https://developer.ibm.com/answers/topics/watson-assistant/){: external}.

## Changes
{: #change-log}

The following new features and changes to the service are available.

## 2.0.1, 30 August 2019
{: #30aug2019}

**{{site.data.keyword.discovery-data_long}} version 2.0.1 is available.** {{site.data.keyword.discovery-data_short}} now works with {{site.data.keyword.icp4dfull}} 2.1.0.1 The following changes were made in this release:

- Added the Windows File System and Database connectors.  See [Database connector](/docs/services/discovery-data?topic=discovery-data-databaseconnect#databaseconnect)
and [Windows File System connector](/docs/services/discovery-data?topic=discovery-data-windowsfilesystemconnect#windowsfilesystemconnect) for details.
- Added support for Traditional Chinese. For more information, see [Language support](/docs/services/discovery-data?topic=discovery-data-language-support#supported-languages).
- Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.discovery-data_long}} offerings purchased on or after August 30, 2019. FISMA support is also available to those who purchased the June 28, 2019 version and upgrade to the August 30, 2019 version. {{site.data.keyword.discovery-data_long}} is FISMA High Ready.
- Released the Classifier enrichment. See [Classifier enrichment](/docs/services/discovery-data?topic=discovery-data-classifier-enrichment#classifier-enrichment) for details.
- Added support for installing {{site.data.keyword.icp4dfull}} on Red Hat OpenShift. 

### Known issues in this release:
{: #30aug2019ki}

  -  After you create a Machine Learning enrichment using a {{site.data.keyword.knowledgestudiofull}} model, two identically named enrichments may display on the **Enrich fields** page. This will not affect the enrichments, but it is best to use only one of them to select and apply the enrichment to one or more fields.
  -  When you upload documents to a collection with existing documents, a `Documents uploaded!` message displays on the **Overview** page, but no further processing status displays until the number of documents increases.
  -  If a web crawl appears to be stuck processing at a fixed number of documents, and the message displayed on the **Logs** page is `The ingestion job <jobid> is terminated incorrectly`, contact IBM support for assistance restarting the crawl.
  -  If one or more of your collections is trained, the training data from one of those collection may display on the **Train** page of an untrained collection. Refresh the page to clear that training data.
  -  The following types of documents will not be processed if they do not have the proper file extension: .docx, .pptx, .xlsx.


The following known issues remain from the GA release:

  -  If you are working in the {{site.data.keyword.discovery-data_short}} tooling, and your {{site.data.keyword.icp4dfull}} session expires, you will receive a blank page. To return to the tooling, refresh the browser and log back in.
  -  All JSON files ingested into {{site.data.keyword.discovery-data_short}} should include the .json file extension.
  -  When querying  on the `collection_id` of a trained collection, the `training_status.notices` value may occasionally display as `0` instead of the correct value.
  -  Not all query limitations are enforced in this release. See [query limitations](/docs/services/discovery-data?topic=discovery-data-query-limitations#query-limitations) for the complete list of banned fields.
  -  In JSON source documents, you should not duplicate the following system-generated fields: `document_id`, `parent_document_id`, `filename`, and `title`. This will cause the duplicate fields to nest within arrays and break certain features, such as ranker training.
  -  Do not include a top-level `metadata` property in your JSON documents. If you upload a JSON document that already contains a top-level `metadata` property, then the `metadata` property of the indexed document will be converted to an array in the index.
  -  CSV files must use commas (`,`) or semicolons (`;`) as delimiters; other delimiters are not supported. If your CSV file includes values containing either commas or semicolons, you should surround those values in double quotation marks so they are not separated. If header rows are present, the values within them are processed in the same manner as values in all other rows. The last row of CSV files will not be processed if not followed by a CRLF (carriage return).
  -  Currently, unique collection names are not enforced. Using duplicate collection names is not recommended and should be avoided.
  
## 2.0.0 (General Availability release), 28 June 2019
{: #28jun2019}

The {{site.data.keyword.discovery-data_long}} service brings the cognitive capabilities of {{site.data.keyword.discoveryfull}} to the {{site.data.keyword.icp4dfull}} platform.

## Known issues in the GA release
{: #known-issues-ga}

The following known issues apply to the GA release:

  -  [Update: fixed in {{site.data.keyword.discovery-data_long}} offerings purchased on or after August 30, 2019.] During an active web crawl, if you add an enrichment, then click the **Recrawl collection** button on the **Overview** page, the collection will stop processing. If the collection does not return to a Syncing state on its own, clicking the **Recrawl collection** button an additional time might be required.
  -  [Update: fixed in {{site.data.keyword.discovery-data_long}} offerings purchased on or after August 30, 2019.] While training a collection in the tooling , if you rate the relevancy of a result (for example, as`Relevant`), then switch to the opposite rating (`Not relevant`), the page may go blank. To restore the page, refresh the browser. Your updated rating will be retained.
  -  [Update: fixed in {{site.data.keyword.discovery-data_long}} offerings purchased on or after August 30, 2019.] Chinese, Japanese, and Korean language Microsoft Word, Excel, and PowerPoint documents will not display correctly in the index or the Smart Document Understanding editor.
  -  If you are working in the {{site.data.keyword.discovery-data_short}} tooling, and your {{site.data.keyword.icp4dfull}} session expires, you will receive a blank page. To return to the tooling, refresh the browser and log back in.
  -  All JSON files ingested into {{site.data.keyword.discovery-data_short}} should include the .json file extension.
  -  [Update: fixed in {{site.data.keyword.discovery-data_long}} offerings purchased on or after August 30, 2019.] If you upload a zip, gzip, or tar file to your collection, and that file contains multiple files/file types supported by Smart Document Understanding (PDF, Word, Excel, PowerPoint, PNG, TIFF, JPEG), only one of the files in that zip, gzip, or tar file will be available for training in the SDU editor (unless the SDU document limit has already been met). All of the documents will be available in the index. Unzip the file before uploading to avoid this issue.
  -  [Update: fixed in {{site.data.keyword.discovery-data_long}} offerings purchased on or after August 30, 2019.] Query expansion and autocomplete return the wrong error code when the `collection_id` is invalid. Query expansion will return a `500` error code instead of a `404`. Autocomplete will return a `400` when the `collection_id` is invalid and the `prefix` parameter isn’t set. It should also return a `404`.
  -  When querying  on the `collection_id` of a trained collection, the `training_status.notices` value may occasionally display as `0` instead of the correct value.
  -  Not all query limitations are enforced in this release. See [query limitations](/docs/services/discovery-data?topic=discovery-data-query-limitations#query-limitations) for the complete list of banned fields.
  -  In JSON source documents, you should not duplicate the following system-generated fields: `document_id`, `parent_document_id`, `filename`, and `title`. This will cause the duplicate fields to nest within arrays and break certain features, such as ranker training.
  -  Do not include a top-level `metadata` property in your JSON documents. If you upload a JSON document that already contains a top-level `metadata` property, then the `metadata` property of the indexed document will be converted to an array in the index.
  -  CSV files must use commas (`,`) or semicolons (`;`) as delimiters; other delimiters are not supported. If your CSV file includes values containing either commas or semicolons, you should surround those values in double quotation marks so they are not separated. If header rows are present, the values within them are processed in the same manner as values in all other rows. The last row of CSV files will not be processed if not followed by a CRLF (carriage return).
  -  [Update: fixed in {{site.data.keyword.discovery-data_long}} offerings purchased on or after August 30, 2019.] When crawling Microsoft SharePoint 2019 collections, only HTML documents will be crawled and indexed. This is a SharePoint issue with how it processes mime-types. See this Microsoft [blog post](https://blog.stefan-gossner.com/2018/11/30/common-issue-sp2019-items-in-document-libraries-are-downloaded-with-mime-type-application-octet-stream-rather-than-the-accurate-one/) for a workaround.
  -  Currently, unique collection names are not enforced. Using duplicate collection names is not recommended and should be avoided.
  -  [Update: fixed in {{site.data.keyword.discovery-data_long}} offerings purchased on or after August 30, 2019.] If you delete an installation of the {{site.data.keyword.discovery-data_short}} add-on, the instance will not uninstall completely and your re-installation will fail. See the {{site.data.keyword.discovery-data_short}} Readme for post-cleanup steps.
  -  [Update: fixed in {{site.data.keyword.discovery-data_long}} offerings purchased on or after August 30, 2019.] If a JSON document that contains nested JSON objects is ingested, the nested JSON will be indexed as a JSON string.
