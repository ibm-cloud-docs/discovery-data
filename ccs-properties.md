---

copyright:
  years: 2019
lastupdated: "2019-11-26"

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
{:xml: .ph data-hd-programlang='xml'}
{:properties: .ph data-hd-programlang='properties'}

# Understanding and customizing the properties file
{: #ccs-properties}

The example custom connector uses a properties file named `message.properties`.
{: shortdesc}

## The default `message.properties` file
{: #default-props}

```properties
CUSTOM-SFTP_DATASOURCE_SETTINGS_KEY_DESCRIPTION=
CUSTOM-SFTP_DATASOURCE_SETTINGS_KEY_LABEL=Key file location
CUSTOM-SFTP_DATASOURCE_SETTINGS_PASSPHRASE_DESCRIPTION=
CUSTOM-SFTP_DATASOURCE_SETTINGS_PASSPHRASE_LABEL=passphrase
CUSTOM-SFTP_DATASOURCE_SETTINGS_SECRET_KEY_DESCRIPTION=
CUSTOM-SFTP_DATASOURCE_SETTINGS_SECRET_KEY_LABEL=Password
CUSTOM-SFTP_DATASOURCE_SETTINGS_USE_KEY_DESCRIPTION=
CUSTOM-SFTP_DATASOURCE_SETTINGS_USE_KEY_LABEL=Use key file ( or input password )
CUSTOM-SFTP_DESCRIPTION=
CUSTOM-SFTP_LABEL=Sftp
CUSTOM-SFTP_SPACE_FILTERS_DESCRIPTION=
CUSTOM-SFTP_SPACE_FILTERS_LABEL=Space filter
CUSTOM-SFTP_SPACE_FILTERS_LEVEL_DESCRIPTION=
CUSTOM-SFTP_SPACE_FILTERS_LEVEL_LABEL=Level
CUSTOM-SFTP_SPACE_FILTERS_ROOT_FILTER_DESCRIPTION=
CUSTOM-SFTP_SPACE_FILTERS_ROOT_FILTER_LABEL=Path filter

#CUSTOM-SFTP_CRAWLSPACE_SETTINGS_DESCRIPTION=Specify how you want the content of this data source to be made available for searching. To apply changes, restart the crawler. The crawler automatically does a full crawl to apply changes to indexed documents.
#CUSTOM-SFTP_CRAWLSPACE_SETTINGS_LABEL=Crawl space Properties
#CUSTOM-SFTP_CRAWLSPACE_SETTINGS_PATH_DESCRIPTION=
#CUSTOM-SFTP_CRAWLSPACE_SETTINGS_PATH_LABEL=Crawl space path
#CUSTOM-SFTP_DATASOURCE_SETTINGS_DESCRIPTION=Specify the data source information.
#CUSTOM-SFTP_DATASOURCE_SETTINGS_HOST_DESCRIPTION=Specify the host name of the data source.
#CUSTOM-SFTP_DATASOURCE_SETTINGS_HOST_LABEL=Host name
#CUSTOM-SFTP_DATASOURCE_SETTINGS_LABEL=Data Source Properties
#CUSTOM-SFTP_DATASOURCE_SETTINGS_PORT_DESCRIPTION=Specify the port of the data source.
#CUSTOM-SFTP_DATASOURCE_SETTINGS_PORT_LABEL=Port
#CUSTOM-SFTP_DATASOURCE_SETTINGS_USER_DESCRIPTION=Specify the user name to crawl the data source.
#CUSTOM-SFTP_DATASOURCE_SETTINGS_USER_LABEL=User name
#CUSTOM-SFTP_GENERAL_SETTINGS_CRAWLER_NAME_DESCRIPTION=Spaces and the characters a-z, A-Z, 0-9, underscore, and hyphen are allowed.
#CUSTOM-SFTP_GENERAL_SETTINGS_CRAWLER_NAME_LABEL=Crawler name
#CUSTOM-SFTP_GENERAL_SETTINGS_DESCRIPTION=Specify the general settings for the crawler.
#CUSTOM-SFTP_GENERAL_SETTINGS_DESCRIPTION_DESCRIPTION=You can change the description without restarting the crawler.
#CUSTOM-SFTP_GENERAL_SETTINGS_DESCRIPTION_LABEL=Crawler description
#CUSTOM-SFTP_GENERAL_SETTINGS_FETCH_INTERVAL_DESCRIPTION=The time is millisecond.
#CUSTOM-SFTP_GENERAL_SETTINGS_FETCH_INTERVAL_LABEL=Time to wait between retrieval requests (milliseconds)
#CUSTOM-SFTP_GENERAL_SETTINGS_LABEL=Crawler Properties
#CUSTOM-SFTP_GENERAL_SETTINGS_MAX_PAGE_LENGTH_DESCRIPTION=Maximum value is 131071 KB. A change to this field requires a full recrawl.
#CUSTOM-SFTP_GENERAL_SETTINGS_MAX_PAGE_LENGTH_LABEL=Maximum document size (KB)
#CUSTOM-SFTP_GENERAL_SETTINGS_NUMBER_OF_MAX_DOCUMENTS_DESCRIPTION=Specify the maximum number of documents to crawl.
#CUSTOM-SFTP_GENERAL_SETTINGS_NUMBER_OF_MAX_DOCUMENTS_LABEL=Maximum number of documents to crawl
#CUSTOM-SFTP_GENERAL_SETTINGS_NUMBER_OF_MAX_THREADS_DESCRIPTION=Specify the maximum number of active crawler threads.
#CUSTOM-SFTP_GENERAL_SETTINGS_NUMBER_OF_MAX_THREADS_LABEL=Maximum number of active crawler threads
#CUSTOM-SFTP_GENERAL_SETTINGS_START_MODE_DESCRIPTION=Specify the crawling mode when the crawler session is started.
#CUSTOM-SFTP_GENERAL_SETTINGS_START_MODE_FULL=Start a full crawl
#CUSTOM-SFTP_GENERAL_SETTINGS_START_MODE_LABEL=When the crawler session is started
#CUSTOM-SFTP_GENERAL_SETTINGS_START_MODE_NORMAL=Start crawling updates (look for new, modified, and deleted content)
#CUSTOM-SFTP_GENERAL_SETTINGS_START_MODE_QUICK=Start crawling new and modified content
#CUSTOM-SFTP_PLUGIN_SETTINGS_CLASSNAME_DESCRIPTION=Specify the class name for the crawler plug-in.
#CUSTOM-SFTP_PLUGIN_SETTINGS_CLASSNAME_LABEL=Plug-in class name
#CUSTOM-SFTP_PLUGIN_SETTINGS_CLASSPATH_DESCRIPTION=Specify the JAR file location of the crawler plug-in.
#CUSTOM-SFTP_PLUGIN_SETTINGS_CLASSPATH_LABEL=Plug-in class path
#CUSTOM-SFTP_PLUGIN_SETTINGS_DESCRIPTION=Specify the crawler plug-in configurations.
#CUSTOM-SFTP_PLUGIN_SETTINGS_ENABLED_DESCRIPTION=Enable this option when you use the crawler plug-in.
#CUSTOM-SFTP_PLUGIN_SETTINGS_ENABLED_LABEL=Enable the crawler plug-in
#CUSTOM-SFTP_PLUGIN_SETTINGS_ENABLING_FOR_EXCLUDED_CONTENTS_DESCRIPTION=Enable this option when making the crawler plug-in handle the excluded document content.
#CUSTOM-SFTP_PLUGIN_SETTINGS_ENABLING_FOR_EXCLUDED_CONTENTS_LABEL=Excluded document content
#CUSTOM-SFTP_PLUGIN_SETTINGS_FENCED_DESCRIPTION=When the plug-in runs in unfenced mode, it runs inside the crawler process. In this mode, plug-in performance is enhanced. Critical\: If the plug-in encounters a problem and cannot recover, the crawler process might be terminated.
#CUSTOM-SFTP_PLUGIN_SETTINGS_FENCED_LABEL=Run the plug-in in unfenced mode
#CUSTOM-SFTP_PLUGIN_SETTINGS_LABEL=Crawler plug-in
```

## Customizing the properties file
{: #customize-properties}

You can customize the properties file by hand, or you can specify required and optional properties in the {{site.data.keyword.discovery-data_short}} tooling when you configure the custom connector to crawl a data source to create a collection.

### Required customizations
{: #ccs-props-req-customizations}

You must provide, at a minimum, valid values for the following properties:

  - The key file, passphrase, or password for the user specified in the `template.xml` file, as described in [Understanding and customizing the XML definitions file](/docs/discovery-data?topic=discovery-data-ccs.xml#ccs-xml-req-customizations):
    ```properties
    CUSTOM-SFTP_DATASOURCE_SETTINGS_KEY_LABEL={key_file_location}
    CUSTOM-SFTP_DATASOURCE_SETTINGS_PASSPHRASE_LABEL={passphrase}
    CUSTOM-SFTP_DATASOURCE_SETTINGS_SECRET_KEY_LABEL={password}
    CUSTOM-SFTP_DATASOURCE_SETTINGS_USE_KEY_LABEL={true | false}
    ```
    For `CUSTOM-SFTP_DATASOURCE_SETTINGS_USE_KEY_LABEL`, specify a value of `true` to use a key file or a value of `false` to use a password.

**DRAFT ONLY: TODO**: List optional and advanced customizations.

<!--
### Optional customizations
{: #ccs-props-optional-customizations}

```properties
CUSTOM-SFTP_DATASOURCE_SETTINGS_PASSPHRASE_DESCRIPTION=
CUSTOM-SFTP_DATASOURCE_SETTINGS_SECRET_KEY_DESCRIPTION=
CUSTOM-SFTP_DATASOURCE_SETTINGS_USE_KEY_DESCRIPTION=
```

### Advanced customizations
{: #ccs-props-adv-customizations}

-->
