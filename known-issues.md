---

copyright:
  years: 2020
lastupdated: "2020-02-10"

keywords: known issues

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

# Known issues
{: #known-issues}

See [Release notes](/docs/discovery-data?topic=discovery-data-release-notes) for the list of {{site.data.keyword.discovery-data_long}} release notes.
{: shortdesc}

Known issues are listed by the release in which they were identified. 

## Known issues identified in the 2.1.1, 24 Jan 2020 release:
{: #24jan2020ki}

  -  When creating a [dictionary](/docs/discovery-data?topic=discovery-data-facets#facetdict), suggested dictionary terms are normalized to lower case by default (for example, Watson Assistant will be normalized to watson assistant). To ensure matching on upper case terms, they should be explicitly included as part of the `Other terms` list or as the `Base term`.
  -  When backing up and restoring data, training data does not restore successfully. Training data can be separately retrieved from a project, see [List training queries](https://cloud.ibm.com/apidocs/discovery/discovery-data-v2#list-training-queries){: external} and uploaded to a new project, see [Create training queries](https://cloud.ibm.com/apidocs/discovery/discovery-data-v2#create-training-query){: external} if needed.
  -  When crawling SharePoint Online or SharePoint OnPrem documents, JSON documents may not be indexed correctly and the `title` returned may be `errored`. This is because SharePoint web services use the `ows_FileRef` property to retrieve JSON files, which will return an error page. To fix this issue, contact your SharePoint Administrator and Microsoft Support.
  -  If you migrate a collection created in version 2.0.1 to either version 2.1.0 or 2.1.1, that collection will not have a **Project type** assigned and the collection will not be available to be queried. To assign a **Project type**, open the **Projects** page by selecting the **Projects** icon on the navigation panel. Name your project and choose one of the Project types: `Document Retrieval`, `Conversational Search`, `Content Mining`, or `Custom`.
  - When installing {{site.data.keyword.discovery-data_short}} on OpenShift, the `ranker-rest` service might intermittently fail to startup, due to an incompatible jar in the `classpath`. To fix the issue:

     1.  Open the `ranker-rest` editor with this command: `kubectl edit deployment {release-name}-{watson-discovery}-ranker-rest`
     2. In the editor, search for the `ranker-rest image` (for example: `{docker-registry}/{namespace}/discovery-ranker-rest-service:20200113-150050-2-d1527c2`) 
     3. Add the following command below `{docker-registry}/{namespace}/discovery-ranker-rest-service:20200113-150050-2-d1527c2`:

        ```bash
        command: ["/tini"]
        args: ["-s", "-v", "--", "java", "-Dkaryon.ssl=true", "-Dkaryon.port=9081", "-Dkaryon.ssl.port=9090", "-Dkaryon.ssl.certificate=/opt/bluegoat/karyon/ssl/karyon-cert.pem", "-Dkaryon.ssl.privatekey=/opt/bluegoat/karyon/ssl/karyon-private-key.pem", "-Djavax.net.ssl.trustStore=/opt/bluegoat/karyon/ssl/keystore.jks", "-Djavax.net.ssl.keyStore=/opt/bluegoat/karyon/ssl/keystore.jks", "-Dlog4j.debug=false", "-Dlitelinks.threadcontexts=log4j_mdc", "-Dwatson.ssl.truststore.path=/opt/bluegoat/karyon/ssl/litelinks-truststore.jks", "-Dwatson.ssl.truststore.password=watson15qa", "-Dlitelinks.delay_client_close=false", "-Drxnetty.http.maxcontentlength=314572800", "-cp", "lib/logback-classic-1.2.3.jar:*:lib/*", "com.ibm.watson.raas.rest.Runner"]
        ```
        {: pre}

Also see the issues identified in all previous releases.

## Known issues identified in the 2.1.0, 27 Nov 2019 release:
{: #29nov2019ki}

  -  When you apply an enrichment to a collection, the enrichment language must match the collection language, or it will fail. The tooling displays all the collections, regardless of language.
  -  Discovery only supports .zip files from MacOS that are generated using a command such as: `zip -r my-folder.zip my-folder -x "*.DS_Store"`. Zips created by right-clicking on a folder name and selecting  `compress` are not supported. 
  -  On the Manage Fields tab, you can edit system-generated fields. The following fields should not be edited by changing the field type or turning off indexing: `document_id`, `extracted_metadata`, `metadata`.
  -  When you delete a Collection and select the option `Don't delete underlying data`, any incomplete document ingestion crawls will continue running in the background, which will impact the new crawl start times, until the existing crawls are completed.
  -  If you have performed relevancy training on an existing collection using the previous version of Discovery (or using the v1 API) then open that collection in a project in {{site.data.keyword.discovery-data_long}} version 2.1.0, and attempt to continue training at the project level via the UI or API, you will cause competing models to be created and block further training. The workaround is to first clear the training data from the original collection if project training is needed.
  -  Discovery can fail to start up correctly due to components getting into a lock state. Manual database intervention may be needed to clear the lock. See [Clearing a lock state](/docs/discovery-data?topic=discovery-data-troubleshoot#troubleshoot-ls) for details on identifying and resolving this issue.
  -  If you upload a document with the Upload Data function, delete that document, and then try to upload either the same document or another document with the same document ID,the upload will fail and the message `Error during creating a document` will be displayed.
  -  Documents that produce an `html` field when processed can not be used with relevancy training. html is produced for documents processed with Smart Document Understanding or Content Intelligence. The `html` field must be removed before relevancy training can complete successfully.
  -  If the Parts of Speech enrichment is not turned on: Dynamic facets will not be created, Dictionary suggestions cannot be used, Content Miner "extracted facets" will not generate.
  -  Discovery for Content Intelligence and Table Understanding enrichments are configured out of the box to be applied on a field named `html`. When a user uploads a JSON document without a top-level field named `html`, these enrichments will not yield results in the index. To run the enrichments on this kind of JSON documents, users must re-configure the enrichments to run on an existing field (or fields) in the JSON document.
  -  When viewing the Content Miner deploy page, sometimes the full application URL is not displayed for copying. To fix, refresh the page.
  -  Deprovisioning a {{site.data.keyword.discovery-data_long}} Instance will not delete the underlying data. Delete the collections and documents manually.
  -  On the Improvement tools panel, the enrichment `Sentiment of phrases` is listed, but is not currently available.
  -  In Content Mining projects, the `dates` fields may not be parsed properly for display in facets.
  -  The Dynamic facets toggle should not appear in Content Mining projects.
  -  A minimum of 50-100 documents should be ingested to see valid dynamic facets generated.
  -  If you click **Stop** to stop a crawler and the converter processes slowly or has errors, you might see a status of the crawler running. 

Also see the issues identified in all previous releases.

### Known issues identified in the 2.0.1, 30 August 2019 release:
{: #30aug2019ki}

  -  After you create a Machine Learning enrichment using a {{site.data.keyword.knowledgestudiofull}} model, two identically named enrichments may display on the **Enrich fields** page. This will not affect the enrichments, but it is best to use only one of them to select and apply the enrichment to one or more fields.
  -  When you upload documents to a collection with existing documents, a `Documents uploaded!` message displays on the **Activity** page, but no further processing status displays until the number of documents increases.
  -  If a web crawl appears to be stuck processing at a fixed number of documents, and the message displayed on the **Logs** page is `The ingestion job <jobid> is terminated incorrectly`, contact IBM support for assistance restarting the crawl.
  -  If one or more of your collections is trained, the training data from one of those collection may display on the **Train** page of an untrained collection. Refresh the page to clear that training data.
  -  The following types of documents will not be processed if they do not have the proper file extension: .docx, .pptx, .xlsx.

Also see the issues identified in the previous release.

## Known issues identified in the General Availability (GA) release, 28 June 2019:
{: #known-issues-ga}

  -  If you are working in the {{site.data.keyword.discovery-data_short}} tooling, and your {{site.data.keyword.icp4dfull}} session expires, you will receive a blank page. To return to the tooling, refresh the browser and log back in.
  -  All JSON files ingested into {{site.data.keyword.discovery-data_short}} should include the .json file extension.
  -  When querying  on the `collection_id` of a trained collection, the `training_status.notices` value may occasionally display as `0` instead of the correct value.
  -  Not all query limitations are enforced in this release. See [query limitations](/docs/discovery-data?topic=discovery-data-query-reference#query-limitations) for the complete list of banned fields.
  -  In JSON source documents, you should not duplicate the following system-generated fields: `document_id`, `parent_document_id`, `filename`, and `title`. This will cause the duplicate fields to nest within arrays and break certain features, such as ranker training.
  -  Do not include a top-level `metadata` property in your JSON documents. If you upload a JSON document that already contains a top-level `metadata` property, then the `metadata` property of the indexed document will be converted to an array in the index.
  -  CSV files must use commas (`,`) or semicolons (`;`) as delimiters; other delimiters are not supported. If your CSV file includes values containing either commas or semicolons, you should surround those values in double quotation marks so they are not separated. If header rows are present, the values within them are processed in the same manner as values in all other rows. The last row of CSV files will not be processed if not followed by a CRLF (carriage return).
  -  Currently, unique collection names are not enforced. Using duplicate collection names is not recommended and should be avoided.