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

# Understanding and customizing the Java source file
{: #ccs-java}

The example custom connector uses a source file named `SftpCrawler.java`.
{: shortdesc}

## The default `SftpCrawler.java` file
{: #default-java}

```java
package com.ibm.es.ama.custom.crawler.sample.sftp;

import com.ibm.es.ama.custom.crawler.CustomCrawler;
import com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration;
import com.ibm.es.ama.datamodel.Field.FieldType;
import com.jcraft.jsch.*;
import com.jcraft.jsch.ChannelSftp.LsEntry;
import java.io.InputStream;
import java.util.*;

/**
 * Custom crawler sample for sftp using jsch.
 */
public class SftpCrawler implements CustomCrawler, CustomCrawlerConfiguration {

   private JSch jsch;

   private String username;

   private int port;

   private String host;

   private Session session;

   private String rootURL;

   /*
    * Initialize custom crawler plugin.
    *
    * @see com.ibm.es.ama.custom.crawler.CustomCrawler#init(com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration.ConfigProvider)
    */
   @Override
   public void init(ConfigProvider config) throws Exception {
      // Get data source section
      Map<String, Object> ds = config.get(ConfigSection.datasource);
      // Get string setting
      this.username = (String) ds.get("user");
      this.host = (String) ds.get("host");
      // Get numeric setting
      this.port = ((Number) ds.get("port")).intValue();
      this.rootURL = "sftp://" + this.host + ":" + this.port;
      // Get boolean setting
      Boolean use = (Boolean) ds.get("use_key");
      this.jsch = new JSch();

      String password = null;
      if (!use) {
         password = (String) ds.get("secret_key");
      } else {
         String key = (String) ds.get("key");
         String passphrase = (String) ds.get("passphrase");
         this.jsch.addIdentity(key, passphrase);
      }
      // Initialize sftp and connect to the specified server
      this.session = this.jsch.getSession(this.username, this.host, this.port);
      Properties setting = new Properties();
      setting.setProperty("StrictHostKeyChecking", "no");
      this.session.setConfig(setting);
      this.session.setDaemonThread(true);

      if (password != null) {
         // Use password
         this.session.setPassword(password);
      }

      this.session.connect();
   }

   /*
    * Terminate crawler session
    * @see com.ibm.es.ama.custom.crawler.CustomCrawler#term()
    */
   @Override
   public void term() throws Exception {
      if (this.session != null) {
         this.session.disconnect();
      }
   }

   /*
    * Crawl server in path
    * @see com.ibm.es.ama.custom.crawler.CustomCrawler#crawl(java.lang.String, com.ibm.es.ama.custom.crawler.CustomCrawler.RecordKeeper)
    */
   @Override
   public void crawl(String path, RecordKeeper keeper) throws Exception {
      ChannelSftp sftp = null;
      try {
         sftp = openChannel();
         Stack<String> stack = new Stack<>();
         stack.push(path);
         // Crawler should stop crawling if user stopped it.
         while (keeper.canContinue() && stack.size() > 0) {
            path = stack.pop();
            // list files under the path
            Vector<Object> ls = ls(path, sftp);
            for (Object object : ls) {
               LsEntry le = (LsEntry) object;
               SftpATTRS attrs = le.getAttrs();

               // ignore hidden files
               String name = le.getFilename();
               if (name.startsWith(".")) {
                  continue;
               }

               // put directory for scanning
               String currentPath = path + "/" + name;
               if (attrs.isDir()) {
                  stack.push(currentPath);
                  continue;
               }

               //if the path is already an absolute path
               if (ls.size() == 1) {
                  currentPath = path;
               }

               // Create a URL for this document.
               String uri = this.rootURL + currentPath;

               // Check if the file is already crawled or changed from last crawl.
               // Based on the modified time as key
               int mTime = attrs.getMTime();
               boolean doCrawl = keeper.check(uri, Arrays.asList(String.valueOf(mTime)));
               if (!doCrawl) {
                  // This document is not changed and do not send.
                  continue;
               }

               // Set fields can be a  string, number or date
               HashMap<String, Object> map = new HashMap<>();
               map.put("modifiedTime", new Date(mTime * 1000L));
               map.put("uid", attrs.getUId());
               map.put("gid", attrs.getGId());
               List<String> docACL = getDocACL(attrs, le.getLongname());

               //Send uri as documents ID, fields and content downloaded from the server.
               keeper.upsert(uri, map, getContent(sftp, currentPath), null, null, docACL);
            }
         }
      } catch (SftpException e) {
         throw e;
      } finally {
         if (sftp != null) {
            try {
               sftp.disconnect();
            } catch (Exception ignored) {
               // ignored
            }
         }
         this.session.disconnect();
      }
   }

   private InputStream getContent(ChannelSftp sftp, String path) {
      InputStream content = null;
         try {
            content = sftp.get(path);
         } catch (SftpException ex) {
            //ignored
            //Something wrong when retrieving the documents e.g. Permission denied
         }
      return content;
   }

   private List<String> getDocACL(SftpATTRS attrs, String entryName) {
      Map<String, String> permissionMap = parseLsEntry(entryName);
      String ownername = permissionMap.get("ownername");
      String groupname = permissionMap.get("groupname");

      List<String> docACL = new ArrayList<>();
      String permissions = attrs.getPermissionsString();
      //owner read access
      char ownerReadAccess = permissions.charAt(1);
      if (ownerReadAccess == 'r') {
         docACL.add(ownername);
      }
      //group read access
      char groupReadAccess = permissions.charAt(4);
      if (groupReadAccess == 'r') {
         docACL.add(String.valueOf(groupname));
      }
      return docACL;
   }

   private Map<String, String> parseLsEntry(String longname) {
      Map<String, String> map = new HashMap<>();
      String[] split = longname.split("\\s+");
      map.put("ownername", split[2]);
      map.put("groupname", split[3]);
      return  map;
   }

   /*
    * Discover crawl space.
    * @see com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration#discoverySubspaces(com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration.ConfigProvider, com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration.SubspaceConsumer, java.util.List, java.util.Map)
    */
   @Override
   public void discoverySubspaces(ConfigProvider config, SubspaceConsumer consumer, List<String> paths, Map<String, Object> filter) throws Exception {
      try {
         init(config);
         String root = (String) filter.get("root_filter");
         int level = ((Number) filter.get("level")).intValue();
         ChannelSftp sftp = openChannel();
         // Add root directory
         consumer.add(root);
         discoverDir(consumer, root, sftp, level - 1);
      } catch (SftpException e) {
         throw e;
      } finally {
         term();
      }
   }

   private void discoverDir(SubspaceConsumer consumer, String path, ChannelSftp sftp, int levelRemains) throws SftpException {
      Vector<Object> ls = ls(path, sftp);
      for (Object object : ls) {
         LsEntry le = (LsEntry) object;
         SftpATTRS attr = le.getAttrs();
         String name = le.getFilename();
         if (name.startsWith(".")) {
            continue;
         }
         String fullPath = path + (path.endsWith("/") ? "" : "/") + name;
         boolean dir = attr.isDir();
         // Add sub space for end user
         consumer.add(fullPath);
         if (levelRemains > 0 && dir) {
            discoverDir(consumer, fullPath, sftp, levelRemains - 1);
         }
      }
   }

   /*
    * Validate configuration
    * @see com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration#validate(com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration.ConfigProvider)
    */
   @Override
   public void validate(ConfigProvider config) throws Exception {
      try {
         init(config);
      } finally {
         term();
      }
   }

   /*
    * Add known type of fields
    * @see com.ibm.es.ama.custom.crawler.CustomCrawlerConfiguration#getFieldsFor(java.lang.String)
    */
   @Override
   public Map<String, FieldType> getFieldsFor(String path) throws Exception {
      Map<String, FieldType> map = new HashMap<>();
      map.put("modifiedTime", FieldType.Date);
      map.put("uid", FieldType.Long);
      map.put("gid", FieldType.Long);
      return map;
   }

   private ChannelSftp openChannel() throws JSchException {
      ChannelSftp sftp;
      sftp = (ChannelSftp) this.session.openChannel("sftp");
      sftp.connect();
      return sftp;
   }

   Vector<Object> ls(String root, ChannelSftp sftp) throws SftpException {
      Vector<Object> ls;
      try {
         ls = sftp.ls(root);
      } catch (SftpException e) {
         if (e.id == 3) {
            return new Vector<>();
         }
         throw e;
      }
      return ls;
   }
}
```
