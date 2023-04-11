---

copyright:
  years: 2019, 2023
lastupdated: "2023-04-11"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Migrating {{site.data.keyword.knowledgestudioshort}} models
{: #migrate-wks}

Use custom models that you created in {{site.data.keyword.knowledgestudioshort}} by migrating them to {{site.data.keyword.discoveryshort}}.
{: shortdesc}

## Using a model as is
{: #migrate-wks-output}

To start using your {{site.data.keyword.knowledgestudioshort}} model immediately, export the model from {{site.data.keyword.knowledgestudioshort}} and import it to {{site.data.keyword.discoveryshort}} as a machine learning enrichment.

When you import a {{site.data.keyword.knowledgestudioshort}} model to use as is in {{site.data.keyword.discoveryshort}}, root-level entity types that were defined in the model can be recognized when they occur in your documents. Any mentions of entity subtypes that occur are identified as mentions of the parent entity type. The subtype entities themselves are not preserved. If you want the model to continue to distinguish between different subtypes of an entity, you must take extra steps. For more information, see [Retaining subtype information](#migrate-wks-subtypes).

Relations and coreferences from the {{site.data.keyword.knowledgestudioshort}} machine learning model are not represented, neither are any custom dictionaries that are associated with the model.

You cannot continue to update a model that you import as an ML enrichment.
{: note}

The following types of models can be imported and used as is:

-  Rule-based models created in {{site.data.keyword.knowledgestudioshort}} that find entities in documents based on rules that you define. (File format: .pear)
-  Machine learning models created in {{site.data.keyword.knowledgestudioshort}} that understand the linguistic nuances, meaning, and relationships specific to your industry (file format: .zip)

The models that you can add depend on your deployment type:

-   [IBM Cloud]{: tag-ibm-cloud} You can add models that were created with a {{site.data.keyword.knowledgestudiofull}} instance that is hosted in {{site.data.keyword.cloud_notm}} only.
-   [IBM Cloud Pak for Data]{: tag-cp4d} You can add models that were created with an instance of {{site.data.keyword.knowledgestudiofull}} that is hosted on {{site.data.keyword.icp4dfull}} or {{site.data.keyword.cloud_notm}}.

For more information, see [Using imported ML models to find custom terms](/docs/discovery-data?topic=discovery-data-domain-ml).

## Using a corpus as training data
{: #migrate-wks-corpus}

{{site.data.keyword.discoveryshort}} has an entity extractor tool that you can use to define a type system. The entity extractor user interface is similar to the {{site.data.keyword.knowledgestudioshort}} user interface that is used to annotate documents that you add to corpus for a machine learning model. However, in {{site.data.keyword.knowledgestudioshort}}, you define root-level entities only, not subtypes or relationships.

As an alternative to importing a {{site.data.keyword.knowledgestudioshort}} model as is and applying it as an enrichment, you can also import a {{site.data.keyword.knowledgestudioshort}} corpus. When you add a {{site.data.keyword.knowledgestudioshort}} corpus to the {{site.data.keyword.discoveryshort}} entity extractor tool, any root-level entities from the corpus are represented as new entities in the {{site.data.keyword.discoveryshort}} entity extractor workspace. Entity subtypes and relations are not recognized.

For more information, see [Importing a {{site.data.keyword.knowledgestudioshort}} corpus](/docs/discovery-data?topic=discovery-data-entity-extractor#entity-extractor-import-wks).

Things to consider when choosing whether to import a model or import a corpus:

-  You can continue to edit the type system when you import the corpus. When you import a trained model, you cannot subsequently edit it in {{site.data.keyword.discoveryshort}}.
-  An imported model that you apply to a collection as an enrichment can find and tag entity subtype and relation information in addition to root-level entities. An entity extractor enrichment can find and tag root-level entities only.

## Retaining subtype information
{: #migrate-wks-subtypes}

When you import a {{site.data.keyword.knowledgestudioshort}} model to {{site.data.keyword.discoveryshort}}, any subtypes that were defined in the model are identified as mentions of the parent entity type. The subtype entities themselves are not preserved. To retain the subtype information, you must *flatten* your type system by converting entity subtypes into new root-level entity types.

Follow these steps only if you are sure that the subtype distinctions add significant value to the model. In many use cases, using the root-level entity types is sufficient.

You cannot use this procedure to retain subtypes if any of the documents in your corpus were pre-annotated with the Natural Language Understanding service. Make sure that your flattened type system doesn't surpass the allowed number of entity types for your plan. For more information, see [Entity extractor limits](/docs/discovery-data?topic=discovery-data-entity-extractor#entity-extractor-limits).
{: important}

For example, your model might have entity types with the following hierarchy:

```text
APPLIANCES
FURNITURE
  PATIO
  LIVING
  DINING
```
{: codeblock}

A flattened version of the type sytem looks like this:

```text
APPLIANCES
FURNITURE_NONE
FURNITURE_PATIO
FURNITURE_LIVING
FURNITURE_DINING
```
{: codeblock}

A useful approach for flattening the type system involves the following changes:

-  Add the parent entity type label (`FURNITURE`) as a prefix to the label of each child subtype to produce a new root-level entity that preserves the hierarchical relationship in its label. For example, `FURNITURE_PATIO`, `FURNITURE_LIVING`, and `FURNITURE_DINING`.
-  Append the word *NONE* to the parent root-level entity label to identify it as the parent. For example, `FURNITURE_NONE`.
-  Leave the labels of entity types that don't have subtypes unchanged. For example, the label `APPLIANCES` doesn't change. 

To retain entity subtype information, complete the following steps:

1.  Ensure that the annotation and training of the {{site.data.keyword.knowledgestudioshort}} model is completed and the model is ready to be deployed.

1.  Export the type system that was used to annotate the documents in your corpus from {{site.data.keyword.knowledgestudioshort}} as a .json file.

    Follow the appropriate steps for exporting based on your {{site.data.keyword.knowledgestudioshort}} deployment type:

    -   [IBM Cloud]{: tag-ibm-cloud} [Uploading resources from another workspace](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-exportimport#wks_exportimport_expimp_type){: external}
    -   [IBM Cloud Pak for Data]{: tag-cp4d} [Uploading resources from another workspace](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-exportimport#wks_exportimport_expimp_type){: external}

1.  Modify the type system JSON file. For each subtype, add a new root-level entity type.

    For example, the original type system might contain the following types:

    ```json
    {
      "id":"b9d6caa2-90ac-47ff-91f6-2149b8ffcf20",
      "label":"FURNITURE",
      "sireProp":{
        "mentionType":null,
        "subtypes":["PATIO","LIVING","DINING"],
        "roles":["b9d6caa2-90ac-47ff-91f6-2149b8ffcf20","93ba1f27-173f-4714-b31e-77bdd8cb9932"],
        "clazz":null,
        "color":"black",
        "hotkey":"m",
        "backGroundColor":"#00FFFF",
        "active":true,
        "roleOnly":false},
        "creationDate":1610611788484,
        "source":null,
        "modifiedDate":0,
        "typeType":null,
        "typeClass":null,
        "typeVersion":null,
        "typeDesc":null,
        "typeSuperType":null,
        "typeSuperTypeId":null,
        "typeCreateDate":null,
        "typeUpdateDate":null,
        "typeProvenance":null,
        "alchemyAPITypes":null,
        "nluAPITypes":null},
    ```
    {: codeblock}

    To convert the subtypes to new root-level types, make the following change:

    ```json
    {
      "id":"b9d6caa2-90ac-47ff-91f6-2149b8ffcf20",
      "label":"FURNITURE_NONE",
      "sireProp":{
        "mentionType":null,
        "subtypes":null,
        "roles":["b9d6caa2-90ac-47ff-91f6-2149b8ffcf20","93ba1f27-173f-4714-b31e-77bdd8cb9932"],
        "clazz":null,
        "and so on"
        }
    },
    {
      "id":"b9d6caa2-90ac-47ff-91f6-2149b8ffcf20",
      "label":"FURNITURE_PATIO",
      "sireProp":{
        "mentionType":null,
        "subtypes":null,
        "roles":["b9d6caa2-90ac-47ff-91f6-2149b8ffcf20","93ba1f27-173f-4714-b31e-77bdd8cb9932"],
        "clazz":null,
        "and so on"
        }
    },
    {
      "id":"b9d6caa2-90ac-47ff-91f6-2149b8ffcf20",
      "label":"FURNITURE_LIVING",
      "sireProp":{
        "mentionType":null,
        "subtypes":null,
        "roles":["b9d6caa2-90ac-47ff-91f6-2149b8ffcf20","93ba1f27-173f-4714-b31e-77bdd8cb9932"],
        "clazz":null,
        "and so on"
        }
    },
    {
      "id":"b9d6caa2-90ac-47ff-91f6-2149b8ffcf20",
      "label":"FURNITURE_DINING",
      "sireProp":{
        "mentionType":null,
        "subtypes":null,
        "roles":["b9d6caa2-90ac-47ff-91f6-2149b8ffcf20","93ba1f27-173f-4714-b31e-77bdd8cb9932"],
        "clazz":null,
        "and so on"
        }
    },
    ```
    {: codeblock}
    
1.  Assign a unique ID to each new root-level entity type.

1.  Export the corpus for your machine learning model from {{site.data.keyword.knowledgestudioshort}} as a compressed file.

    Follow the appropriate steps for exporting based on your {{site.data.keyword.knowledgestudioshort}} deployment type:

    -   [IBM Cloud]{: tag-ibm-cloud} [Uploading resources from another workspace](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-exportimport#wks_exportimport_expimp_doc){: external}
    -   [IBM Cloud Pak for Data]{: tag-cp4d} [Uploading resources from another workspace](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-exportimport#wks_exportimport_expimp_doc){: external}

1.  In the downloaded corpus, for all mentions with a subtype defined, update the type information for the mention to specify the new root-level entity type.

    For example, the original type system might include the `PATIO` subtype mention:

    ```json
    {
      "id" : "Blogs_shopper.com_dc5cf4764d91f87575b17ac8a5268462.en-M92",
      "source" : "IMPORT",
      "properties" : {
        "SIRE_ENTITY_CLASS" : "SPC",
        "SIRE_MENTION_CLASS" : "SPC",
        "SIRE_ENTITY_LEVEL" : "NONE",
        "SIRE_ENTITY_SUBTYPE" : "PATIO",
        "SIRE_MENTION_ROLE" : "FURNITURE",
        "SIRE_MENTION_TYPE" : "NONE"
      },
      "type" : "FURNITURE",
      "begin" : 3221,
      "end" : 3234,
      "inCoref" : false
    },
    ```
    {: codeblock}

    Replace the value of the `SIRE_MENTION_ROLE` and `type` for the mention with the new root-level entity label, such as `FURNITURE_PATIO`. Specify `NONE` as the `SIRE_ENTITY_SUBTYPE` value.

    ```json 
    {
      "id" : "Blogs_shopper.com_dc5cf4764d91f87575b17ac8a5268462.en-M92",
      "source" : "IMPORT",
      "properties" : {
        "SIRE_ENTITY_CLASS" : "SPC",
        "SIRE_MENTION_CLASS" : "SPC",
        "SIRE_ENTITY_LEVEL" : "NONE",
        "SIRE_ENTITY_SUBTYPE" : "NONE",
        "SIRE_MENTION_ROLE" : "FURNITURE_PATIO",
        "SIRE_MENTION_TYPE" : "NONE"
      },
      "type" : "FURNITURE_PATIO", 
      "begin" : 3221,
      "end" : 3234,
      "inCoref" : false
    },
    ```
    {: codeblock}

    Don't forget to rename the parent mention labels. 
    
    For example, find mentions that specify `"SIRE_ENTITY_SUBTYPE" : "OTHER"`, and then change the value from `OTHER` to `NONE`.

    Change the value of the `SIRE_MENTION_ROLE` and `type` for the mention to the new parent entity type label.
    
    For example, change the `SIRE_MENTION_ROLE` and `type` values for these mentions from `FURNITURE` to `FURNITURE_NONE`, and the `SIRE_ENTITY_SUBTYPE` to `NONE`.

    ```json
    {
      "id" : "Sports_herald.com_be99aca94a7cff5abb74476b844a11b6.en-M75",
      "source" : "IMPORT",
      "properties" : {
        "SIRE_MENTION_CLASS" : "SPC",
        "SIRE_ENTITY_LEVEL" : "NONE",
        "SIRE_ENTITY_SUBTYPE" : "NONE",
        "SIRE_ENTITY_CLASS" : "SPC",
        "SIRE_MENTION_TYPE" : "NONE",
        "SIRE_MENTION_ROLE" : "FURNITURE_NONE"
      },
      "type" : "FURNITURE_NONE",
      "begin" : 2063,
      "end" : 2071,
      "inCoref" : false
    },
    ```
    {: codeblock}

1.  Create a {{site.data.keyword.knowledgestudioshort}} workspace, and then upload the converted type system and annotated data.

    Follow the appropriate steps for uploading documents based on your {{site.data.keyword.knowledgestudioshort}} deployment type:

    -   [IBM Cloud]{: tag-ibm-cloud} [Adding documents to a workspace](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-documents-for-annotation#wks_projadd){: external}
    -   [IBM Cloud Pak for Data]{: tag-cp4d} [Adding documents to a workspace](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-documents-for-annotation#wks_projadd){: external}

    Follow the appropriate steps for uploading a type system based on your {{site.data.keyword.knowledgestudioshort}} deployment type:

    -   [IBM Cloud]{: tag-ibm-cloud} [Adding a type system to the workspace](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-typesystem#wks_projtypesys){: external}
    -   [IBM Cloud Pak for Data]{: tag-cp4d} [Adding a type system to the workspace](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-typesystem#wks_projtypesys){: external}

1.  From {{site.data.keyword.knowledgestudioshort}}, click **Train** to retrain the model.

    For more information, see the appropriate topic for your deployment type:
    
    -   [IBM Cloud]{: tag-ibm-cloud} [Training the machine learning model](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-train-ml){: external}
    -   [IBM Cloud Pak for Data]{: tag-cp4d} [Training the machine learning model](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-train-ml){: external}

1.  Now, you're ready to export the model from {{site.data.keyword.knowledgestudioshort}} and import it to {{site.data.keyword.discoveryshort}} to use the model as a machine learning enrichment.

    For more information, see [Using imported ML models to find custom terms](/docs/discovery-data?topic=discovery-data-domain-ml).
