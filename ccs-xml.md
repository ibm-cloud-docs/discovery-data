---

copyright:
  years: 2019
lastupdated: "2019-11-26"

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
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}
{:xml: .ph data-hd-programlang='xml'}
{:properties: .ph data-hd-programlang='properties'}

# Understanding and customizing the XML definitions file
{: #ccs-xml}

The example custom connector uses a definition file named `template.xml`.
{: shortdesc}

## The default `template.xml` file
{: #default-xml}

```xml
<!-- Do not change the name of the file. The file must not contains blank spaces or non-ASCII characters. -->
<function name="custom-sftp">
    <prototype>
    	<!-- General settings -->
        <proto-section section="general_settings">
        	<!-- Common settings might not need to be modified -->
            <declare type="string" name="crawler_name" />
            <declare type="string" name="description" />
            <declare type="long" name="fetch_interval" initial-value="0" />
            <declare type="long" name="number_of_max_threads" initial-value="10" />
            <declare type="long" name="number_of_max_documents" initial-value="2000000000" />
            <declare type="long" name="max_page_length" initial-value="32768" />
            <declare type="enum" name="start_mode" enum-values="NORMAL|QUICK|FULL" initial-value="NORMAL" />
	
	    	<!-- Configuration class -->        
            <declare type="string" name="custom_config_class" hidden="true" initial-value="com.ibm.es.ama.custom.crwler.sample.sftp.SftpCrawler" />
	    	<!-- Crawler class -->        
            <declare type="string" name="custom_crawler_class" hidden="true" initial-value="com.ibm.es.ama.custom.crwler.sample.sftp.SftpCrawler" />
	    	<!-- Document level security class -->        
            <declare type="string" name="custom_security_class" hidden="true" initial-value="com.ibm.es.ama.custom.crwler.sample.sftp.SftpCrawler" />
            <!-- Document level security is enabled or not -->
            <declare type="boolean" name="document_level_security_supported" initial-value="true" hidden="true"/>
            <!-- Must be false. -->
            <declare type="boolean" name="document_level_security_sso_enabled" initial-value="false" hidden="true"/>
            <!-- Construct scope from variables in datasource setting. -->
            <declare type="string" name="document_level_security_scope" initial-value="{host}:{port}" hidden="true"/>
        </proto-section>
		<!-- Data source settings change on each server -->
        <proto-section section="datasource_settings">
			<!-- Sample: SFTP server settings -->
            <declare type="string" name="host" required="required" initial-value="localhost"/>
            <declare type="long" name="port" required="required" initial-value="22"/>
            <declare type="string" name="user" required="required" />

			<!-- Sample: Use key file or password -->
            <declare type="boolean" name="use_key" initial-value="true" />
			<!-- Sample: If use key, input key and passphrase -->
            <condition name="use_key" enabled="true">
                <declare type="string" name="key" hidden="false" />
                <declare type="password" name="passphrase" hidden="false" />
            </condition>
            <!-- Sample: If use password, input password -->           
            <condition name="use_key" enabled="false">
                <declare type="password" name="secret_key" hidden="false" />
            </condition>
        </proto-section>
		<!-- Sample: Filter crawl space by root path and level to be recursively check -->    
        <proto-section section="space_filters" hidden="true">
            <declare type="string" name="root_filter" required="required"  initial-value="/" />
            <declare type="long" name="level" required="required" initial-value="1" />
        </proto-section>

		<!-- Do not modify, must be here -->    
        <proto-section section="crawlspace_settings" cardinality="multiple">
            <declare type="string" name="path" hidden="true" />
        </proto-section>

		<!-- Crawler Plugin is not supported.
        <proto-section section="plugin_settings">
            <declare type="boolean" name="enabled" initial-value="false" />
            <condition name="enabled" enabled="true">
                <declare type="boolean" name="fenced" initial-value="false" hidden="true" />
                <declare type="boolean" name="enabling_for_excluded_contents" initial-value="true" hidden="true" />
                <declare type="string" name="classname" />
                <declare type="string" name="classpath" />
            </condition>
        </proto-section>
        -->
    </prototype>
</function>
```
