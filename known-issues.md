---

copyright:
  years: 2020
lastupdated: "2020-09-01"

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

See [Release notes](/docs/discovery-data?topic=discovery-data-release-notes) for the list of {{site.data.keyword.discoveryfull}} release notes.
{: shortdesc}

Known issues are listed by the release in which they were identified.

## Known issues identified in the Discovery for Cloud Pak for Data 2.1.4, 1 September 2020 release:
{: #1sept2020ki}

  - When configuring a Web crawl using FORM authentication, if you specify a URL without a trailing slash, for example: `https://webcrawlurl.com`, the web crawl will only crawl the login page. To workaround this issue, add a trailing slash to the URL, for example: `https://webcrawlurl.com/`.
  - The [Guided Tours](/docs/discovery-data?topic=discovery-data-tours) do not run on Firefox. For the list of other supported browsers, see [Browser support](/docs/discovery-data?topic=discovery-data-about#about-browser).
  - Ingesting documents into a collection that uses a custom [Advanced Rules model enrichment](/docs/discovery-data?topic=discovery-data-create-enrichments#advanced-rules) built in Watson Knowledge Studio may fail if multiple extractors in the model internally use the same names for one or more output views.
  - If you delete a large number of documents, then immediately ingest a large number of documents, it may take longer for all the documents to become available.
  - The [Classifier enrichment](/docs/discovery-data?topic=discovery-data-create-enrichments#classifier-enrichment) does not work when FIPS (Federal Information Processing Standards) is enabled.

 
Also see the issues identified in all previous releases. 

## Known issues identified in the IBM Cloud Premium General Availability (GA) release, 16 July 2020:
{: #16jul2020ki}
  
  - ![IBM Cloud only](images/cloudonly.png) When connecting to an {{site.data.keyword.blockstoragefull}} source with the {{site.data.keyword.discovery-data_short}} tooling, you will only see the first 75 COS buckets for a given credential. (This data source is only available in IBM Cloud.)


Also see the issues identified in all previous releases.

## Known issues identified in the Discovery for Cloud Pak for Data 2.1.3, 19 June 2020 release:
{: #19jun2020ki}

  - `Entity Subtypes` in {{site.data.keyword.knowledgestudiofull}} Machine Learning models are not supported in {{site.data.keyword.discovery-data_short}} 2.1.3 or later. For instructions on converting existing models, contact the [Support center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.
  - You cannot upload CSV files that include a space in the file name (for example: `file 1.csv`) to a Content Mining project. Rename the file to work around the issue.
  - When performing Project level relevancy training, if you have multiple collections, and two or more of those collections contains a duplicate `document_id`, then project level relevancy training will fail. Example of duplicate `document_ids`: `Collection A` contains a document with the id of `1234`, and `Collection B` also contains a document with the id of `1234`.
  - Only the first facet using a field with the prefix `extracted_metadata` is saved correctly after creation. Others with that prefix will appear but after a screen refresh will be gone. This only happens once per project, so the workaround is to refresh and add the facet again.
  - ![Cloud Pak for Data only](images/cpdonly.png) During installation on {{site.data.keyword.icp4dfull}} 2.5.0.0, some Kubernetes Jobs may incorrectly report their status as `OOMKilled`, causing the install to timeout. To resolve this, once a Job returns `OOMKilled` verify the logs of the Pod associated with that Job. There should be no obvious error messages in the logs and the resources are reported in the logs as created. Manually verify these resources exist in the namespace and then delete the Job. This will cause the install to continue.
  - Some documents may show two `html` fields when applying an enrichment. Both `html` fields shown are the same and operate as such.
  - When creating a data source in Firefox, you may not see the entire list of options, including the **More processing settings** settings. To work around the issue, zoom out, increase the browser height, or use another supported browser.
  - When customizing the display of search results, the changes made sometimes do not save after clicking the `Apply` button. To work around this issue, refresh the browser and try to make the changes again.
  - When setting up a data source or web crawler for your collection, if you enter an incorrect configuration, then try to update it on the **Processing settings** page, the data source update or crawl may not start when you click the `Apply changes and reprocess` button. You can confirm this issue by opening the **Activity** page for your collection to see if processing has started. If you see that processing has not started for your data source, click the `Recrawl` button, then the `Apply changes and reprocess` button. If you see that processing has not started for your web crawl, click the `Stop` button, then the `Recrawl` button.
  - ![Cloud Pak for Data only](images/cpdonly.png) When running Helm tests on the `core` deployment using `helm test core`, the `core-discovery-api-post-install-test` will return a `FAILED` status. This is due to a bug within the test pod's image. The test result can be ignored as the failure is not related to anything within the deployment.
  - By default, Optical Character Recognition (OCR) is set to `off` when you create any **Project type** with the tooling. However, if you create a Project using the API, OCR is set to `on`. To work around this issue, open the Tooling and change the **Project setting** to `off`.
  - When Optical Character Recognition (OCR) is set to `on` for a Collection AND no trained Smart Document Understanding (SDU) model is applied, PNG, TIFF, and JPG files will not be processed for text recognition. Images embedded in PDF, Word, PowerPoint, and Excel documents will not be processed - only the non-image portion of these documents will be processed for text recognition. To work around this issue, import or train an SDU model and reprocess the collection. This will allow text to be extracted from the images.
  - After you create a Search Skill in Watson Assistant and are directed to the Watson {{site.data.keyword.discoveryshort}} tooling, the screen is blank. This happens because the URL is missing the {{site.data.keyword.discoveryshort}} instance ID. To work around this issue:
    1. From the IBM Cloud Pak for Data web client menu, choose **My Instances**. For example: `https://mycluster.com/zen/#/myInstances`.
    1. Select the Discovery instance you are using and click **Launch Tool**.
    1. Once the tooling is loaded, the URL should have the following structure: `https://mycluster.com/discovery/core/instances/00000000-0000-0000-0001-597165341876/projects`
    1. Copy the entire path, excluding `/projects`. For example: `https://mycluster.com/discovery/core/instances/00000000-0000-0000-0001-597165341876`
    1. Go back to the browser tab that is displaying the blank Discovery screen. That URL structure will look like this: `https://mycluster.com/discovery/core/collections/new?redirect_uri=...`
    1. Replace `https://mycluster.com/discovery/core` with the URL you copied previously, so the new URL should look like this: `https://mycluster.com/discovery/core/instances/00000000-0000-0000-0001-597165341876/collections/new?redirect_uri=...`
    1. Press enter to open updated URL. You should now be on the Watson {{site.data.keyword.discoveryshort}} **Manage collections** page.

Also see the issues identified in all previous releases. 

## Known issues identified in the Discovery for Cloud Pak for Data 2.1.2, 31 Mar 2020 release:
{: #31mar2020ki}

  -  When using passage retrieval with Korean, Polish, Japanese, Slovak or Chinese you may encounter much slower response times in this version. To resolve this, either disable passage retrieval, or upload a custom stopword list with words that are common in your documents (for example, prepositions and pronouns).  See [Defining stopwords](https://cloud.ibm.com/docs/discovery-data?topic=discovery-data-search-settings#stopwords) for example stopword lists in several languages. Also see [Stopwords ISO](https://github.com/stopwords-iso/){: external}) on GitHub.
  -  [Update: fixed in version 2.1.3] In versions 2.1.2, 2.1.1, and 2.1.0, PNG, TIFF, and JPG individual image files are not scanned, and no text is extracted from those files. PNG, TIFF, and JPEG images embedded in PDF, Word, PowerPoint, and Excel files are also not scanned, and no text is extracted from those image files.
  -  Smart Document Understanding does not support `.doc`, `.docx`, `.odf`, `.xls`, `.xlsx`, `.ods`, `.ppt`, `.pptx`, and `.odp` conversion when FIPS (Federal Information Processing Standards) is enabled.
  -  In a Content Mining application, any document flags set will disappear if the index is rebuilt for that collection.
  -  Beginning with the 2.1.2 release, uploading and managing relevancy training data using the v1 APIs will not train a relevancy training model. The v1 APIs have been superseded by the [Projects relevancy training v2 APIs](https://{DomainName}/apidocs/discovery/discovery-data#createtrainingquery){: external}. If your training data needs to be preserved, it can be listed using the v1 API, then added to a project with the v2 API.
  -  Multiple [Regular expressions enrichments](/docs/services/discovery-data?topic=discovery-data-create-enrichments#characterpattern-enrichment) cannot be applied to a collection at the same time.
  -  ![Cloud Pak for Data only](images/cpdonly.png) There were two small changes to the installation instructions README included with the download of {{site.data.keyword.discovery-data_long}}. For the updated version of the README, see the [Discovery Helm chart README.md](https://github.com/ibm-cloud-docs/data-readmes/blob/master/discovery-README.md){: external}.
     -  A change to the description of the `--cluster-pull-prefix PREFIX` argument.
     -  The language extension pack name has been updated from `ibm-watson-discovery-pack1-2.1.2.tar.xz.` to `ibm-wat-dis-pack1-prod-2.1.2.tar.xz`.
  
Also see the issues identified in all previous releases.

## Known issues identified in the Discovery for Cloud Pak for Data 2.1.1, 24 Jan 2020 release:
{: #24jan2020ki}

  -  When creating a [dictionary](/docs/discovery-data?topic=discovery-data-facets#facetdict), suggested dictionary terms are normalized to lower case by default (for example, Watson Assistant will be normalized to watson assistant). To ensure matching on upper case terms, they should be explicitly included as part of the `Other terms` list or as the `Base term`.
  -  When backing up and restoring data, training data does not restore successfully. If the documents in your collection were added by crawl using a connector or web crawl, your training data can be separately retrieved for backup from an existing project and uploaded to a new restored project. For more information, see [List training queries](https://{DomainName}/apidocs/discovery/discovery-data#isttrainingqueries){: external} and [Create training queries](https://{DomainName}/apidocs/discovery/discovery-data#createtrainingquery){: external}) in the API reference.
  -  When crawling SharePoint Online or SharePoint OnPrem documents, JSON documents may not be indexed correctly and the `title` returned may be `errored`. This is because SharePoint web services use the `ows_FileRef` property to retrieve JSON files, which will return an error page. To fix this issue, contact your SharePoint Administrator and Microsoft Support.
  -  ![Cloud Pak for Data only](images/cpdonly.png) If you migrate a collection created in version 2.0.1 to either version 2.1.0 or 2.1.1, that collection will not have a **Project type** assigned and the collection will not be available to be queried. To assign a **Project type**, open the **Projects** page by selecting **My Projects**. Name your project and choose one of the Project types: `Document Retrieval`, `Conversational Search`, `Content Mining`, or `Custom`.
  - [Update: fixed in version 2.1.2] When installing {{site.data.keyword.discovery-data_short}} on OpenShift, the `ranker-rest` service might intermittently fail to startup, due to an incompatible jar in the `classpath`. To fix the issue:

     1. Open the `ranker-rest` editor with this command: `kubectl edit deployment {release-name}-{watson-discovery}-ranker-rest`
     2. In the editor, search for the `ranker-rest image` (for example: `{docker-registry}/{namespace}/discovery-ranker-rest-service:20200113-150050-2-d1527c2`) 
     3. Add the following command below `{docker-registry}/{namespace}/discovery-ranker-rest-service:20200113-150050-2-d1527c2`:

        ```bash
        command: ["/tini"]
        args: ["-s", "-v", "--", "java", "-Dkaryon.ssl=true", "-Dkaryon.port=9081", "-Dkaryon.ssl.port=9090", "-Dkaryon.ssl.certificate=/opt/bluegoat/karyon/ssl/karyon-cert.pem", "-Dkaryon.ssl.privatekey=/opt/bluegoat/karyon/ssl/karyon-private-key.pem", "-Djavax.net.ssl.trustStore=/opt/bluegoat/karyon/ssl/keystore.jks", "-Djavax.net.ssl.keyStore=/opt/bluegoat/karyon/ssl/keystore.jks", "-Dlog4j.debug=false", "-Dlitelinks.threadcontexts=log4j_mdc", "-Dwatson.ssl.truststore.path=/opt/bluegoat/karyon/ssl/litelinks-truststore.jks", "-Dwatson.ssl.truststore.password=watson15qa", "-Dlitelinks.delay_client_close=false", "-Drxnetty.http.maxcontentlength=314572800", "-cp", "lib/logback-classic-1.2.3.jar:*:lib/*", "com.ibm.watson.raas.rest.Runner"]
        ```
        {: pre}

Also see the issues identified in all previous releases.

## Known issues identified in the Discovery for Cloud Pak for Data 2.1.0, 27 Nov 2019 release:
{: #29nov2019ki}

  -  When you apply an enrichment to a collection, the enrichment language must match the collection language, or it will fail. The tooling displays all the collections, regardless of language.
  -  Discovery only supports .zip files from MacOS that are generated using a command such as: `zip -r my-folder.zip my-folder -x "*.DS_Store"`. Zips created by right-clicking on a folder name and selecting  `compress` are not supported. 
  -  On the Manage Fields tab, you can edit system-generated fields. The following fields should not be edited by changing the field type or turning off indexing: `document_id`, `extracted_metadata`, `metadata`.
  -  When you delete a Collection and select the option `Don't delete underlying data`, any incomplete document ingestion crawls will continue running in the background, which will impact the new crawl start times, until the existing crawls are completed.
  -  ![Cloud Pak for Data only](images/cpdonly.png) Discovery can fail to start up correctly due to components getting into a lock state. Manual database intervention may be needed to clear the lock. For more information on identifying and resolving this issue, see [Clearing a lock state](/docs/discovery-data?topic=discovery-data-troubleshoot#troubleshoot-ls).
  -  If you upload a document with the Upload Data function, delete that document, and then try to upload either the same document or another document with the same document ID,the upload will fail and the message `Error during creating a document` will be displayed.
  -  Documents that produce an `html` field when processed can not be used with relevancy training. html is produced for documents processed with Smart Document Understanding or Content Intelligence. The `html` field must be removed before relevancy training can complete successfully.
  -  If the Parts of Speech enrichment is not turned on: Dynamic facets will not be created, Dictionary suggestions cannot be used, Content Miner "extracted facets" will not generate.
  -  [Update: fixed in version 2.1.1] Discovery for Content Intelligence and Table Understanding enrichments are configured out of the box to be applied on a field named `html`. When a user uploads a JSON document without a top-level field named `html`, these enrichments will not yield results in the index. To run the enrichments on this kind of JSON documents, users must re-configure the enrichments to run on an existing field (or fields) in the JSON document.
  -  When viewing the Content Miner deploy page, sometimes the full application URL is not displayed for copying. To fix, refresh the page.
  -  [Update: fixed in version 2.1.2] Deprovisioning a {{site.data.keyword.discovery-data_long}} Instance will not delete the underlying data. Delete the collections and documents manually.
  -  [Update: fixed in version 2.1.3] On the Improvement tools panel, the enrichment `Sentiment of phrases` is listed, but is not currently available.
  -  In Content Mining projects, the `dates` fields may not be parsed properly for display in facets.
  -  The Dynamic facets toggle should not appear in Content Mining projects.
  -  A minimum of 50-100 documents should be ingested to see valid dynamic facets generated.
  -  If you click **Stop** to stop a crawler and the converter processes slowly or has errors, you might see a status of the crawler running.
  -  The total size limit of all non-HTML fields in uploaded and crawled documents is 1MB, which is equivalent to 1,048,676 bytes, and the total size limit of all HTML fields in these documents is 5MB. If you exceed either limit, you receive an error message stating `The document has fields/HTML fields that exceed the 1 MB/5 MB limit.`, and the document is not ingested. For assistance on increasing either size limit, contact the [IBM Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.

Also see the issues identified in all previous releases.

## Known issues identified in the Discovery for Cloud Pak for Data 2.0.1, 30 August 2019 release:
{: #30aug2019ki}

  -  After you create a Machine Learning enrichment using a {{site.data.keyword.knowledgestudiofull}} model, two identically named enrichments may display on the **Enrich fields** page. This will not affect the enrichments, but it is best to use only one of them to select and apply the enrichment to one or more fields.
  -  [Update: fixed in version 2.1.2] When you upload documents to a collection with existing documents, a `Documents uploaded!` message displays on the **Activity** page, but no further processing status displays until the number of documents increases.
  -  If a web crawl appears to be stuck processing at a fixed number of documents, and the message displayed on the **Logs** page is `The ingestion job <jobid> is terminated incorrectly`, contact IBM support for assistance restarting the crawl.
  -  If one or more of your collections is trained, the training data from one of those collection may display on the **Train** page of an untrained collection. Refresh the page to clear that training data.
  -  The following types of documents will not be processed if they do not have the proper file extension: .docx, .pptx, .xlsx.

Also see the issues identified in the previous release.

## Known issues identified in the Discovery for Cloud Pak for Data General Availability (GA) release, 28 June 2019:
{: #known-issues-ga}

  -  If you are working in the {{site.data.keyword.discovery-data_short}} tooling, and your {{site.data.keyword.icp4dfull}} session expires, you will receive a blank page. To return to the tooling, refresh the browser and log back in.
  -  All JSON files ingested into {{site.data.keyword.discoveryshort}} should include the .json file extension.
  -  When querying  on the `collection_id` of a trained collection, the `training_status.notices` value may occasionally display as `0` instead of the correct value.
  -  Not all query limitations are enforced in this release. See [query limitations](/docs/discovery-data?topic=discovery-data-query-reference#query-limitations) for the complete list of banned fields.
  -  In JSON source documents, you should not duplicate the following system-generated fields: `document_id`, `parent_document_id`, `filename`, and `title`. This will cause the duplicate fields to nest within arrays and break certain features, such as ranker training.
  -  Do not include a top-level `metadata` property in your JSON documents. If you upload a JSON document that already contains a top-level `metadata` property, then the `metadata` property of the indexed document will be converted to an array in the index.
  -  CSV files must use commas (`,`) or semicolons (`;`) as delimiters; other delimiters are not supported. If your CSV file includes values containing either commas or semicolons, you should surround those values in double quotation marks so they are not separated. If header rows are present, the values within them are processed in the same manner as values in all other rows. The last row of CSV files will not be processed if not followed by a CRLF (carriage return).
  -  Currently, unique collection names are not enforced. Using duplicate collection names is not recommended and should be avoided.
