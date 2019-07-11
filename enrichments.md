---

copyright:
  years: 2019
lastupdated: "2019-07-10"

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


# Creating enrichments
{: #create-enrichments}

<!-- Help for the Enrichments screen in WD ICP4D -->

You can create enrichments that will add related terms (**Dictionary**), identify and extract values (**Character Pattern**), or extract entities and relationships/apply rules (**Machine Learning**) to fields in your collection.
{: shortdesc}


To create a new enrichment:

1. Click the **Enrichments** ![Enrichments](images/enrichments_icon.png) icon on the left.
1. Click **Add new**
1. Enter a **Name** and choose the enrichment **Type**.
1. Configure the enrichment:
    - [**Dictionary**](/docs/services/discovery-data?topic=discovery-data-dictionary-enrichment#dictionary-enrichment) 
    - [**Character Pattern**](/docs/services/discovery-data?topic=discovery-data-characterpattern-enrichment#characterpattern-enrichment)
    - [**Machine Learning**](/docs/services/discovery-data?topic=discovery-data-machinelearning-enrichment#machinelearning-enrichment) 
1. Click the **Create** button.

After you create an enrichment, you must apply it to a field (or fields) in your collection. See [Enriching fields](/docs/services/discovery-data?topic=discovery-data-enrich-fields#enrich-fields) for instructions.
{: important}

Once you create an enrichment, it is not possible to edit or delete it. If you need to update an existing enrichment, create a new one.
{: note}

## Dictionary enrichments
{: #dictionary-enrichment}

The Dictionary enrichment allows you to enrich document fields in your collection. The enrichment terms can be synonyms (car, automotive, auto), or words in the same category (carburetor, piston, valves). 

You must create and upload a dictionary csv file to apply this enrichment. The enrichment will be applied only to the field(s) you specify on the [Enrich fields](/docs/services/discovery-data?topic=discovery-data-enrich-fields#enrich-fields) screen.

Enrichment-specific fields:

-  **Collection language** - Select the language of your dictionary `.csv` file.
-  **Facet Path** - Used as a field value in the index. To specify hierarchy, use a period `.` to separate values, for example `automobiles.motorsports`.

Dictionary files must be .csv files using UTF-8 encoding in the following format. For example:

```
engine,gasket,carburetor,piston,valves
racing,stock,open,indy,drag
flag,checkered,green,caution,yellow,red
```

Each line of the csv file is a separate enrichment. For example, this line: `engine,gasket,carburetor,piston,valves` will apply the enrichment `engine` to the specified field(s) in your collection that contain the terms `engine`,`gasket`,`carburetor`,`piston`, or `valves`.

In the output, the dictionary enrichment can be found under `enriched_text`, within the `entities` array.

In this example, the **Facet Path** specified was `automobiles.motorsports`, and the field selected for enrichment was `text`.

 In the JSON output
 -  `path` = entire **Facet Path**
 -  `type` = final level of the **Facet Path** 
 -  `text` = enrichment (in this example, `engine`) 

```JSON
"enriched_text": [
  {
    "entities": [
	  {
	    "path": ".automobiles.motorsports",
		"text": "engine",
		"type": "motorsports"
	  }
	]
  }
],
. . .
"text": [
  "I prefer a carburetor to fuel-injection."
]  
```

Result: The query `enriched_text.entities.text:engine` will also return results that include `carburetor`. 

## Character Pattern enrichments
{: #characterpattern-enrichment}

The Character Pattern enrichment uses regular expressions to identify and extract information from fields in your collection.

The enrichment will be applied only to the field(s) you specify on the [Enrich fields](/docs/services/discovery-data?topic=discovery-data-enrich-fields#enrich-fields) screen.

Enrichment-specific fields:

-  **Facet Path** - The text matched to this regular expression will be included in this facet. To specify hierarchy, use a period `.` to separate values, for example `regex.cccardnumber`.
-  **Character Pattern** - Your regular expression string. 

Notes about writing regular expressions:

-  Use a Java&trade; regular expression. See the [Java documentation](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html){: external} for more information. 
-  Your regular expression should be short and understandable.
-  The optimal regular expression would lead to a match or a non-match quickly.
-  It is best to extract common patterns. For example, use `a(b|c|d)` instead of `(ab|ac|ad)`.
-  The regular expression engine may fail if it backtracks because it can't make a negative match towards the end of the string and then attempts too many permutations. To avoid this, consider using a possessive quantifier, for example, `(a+b*)++c`.

Example:

This regular expression will find credit card numbers of a specific format and length in your collection. 

```
4[0-9]{15}
```

In the output, the information extracted by the Character Pattern enrichment can be found under `enriched_text`, within the `entities` array.

In this example, the **Facet Path** specified was `regex.cccardnumber`, and the field selected for enrichment was `text`.

In the JSON output:
 -  `type` = final level of the **Facet Path** 
 -  `path` = entire **Facet Path**
 -  `text` = the information extracted with the regular expression (in this example, `4000000000000000`) 

```JSON
"enriched_text": [
  {
    "entities": [
      {
        "type": "cccardnumber",
        "path": ".regex.cccardnumber",
        "text": "4000000000000000"
      }
	]
  }
],
. . .
"text": [
  "He has 2 phones, 090-1234-5678 and 080-1234-5678. His credit card number is 4000000000000000."
]
```	

Result: The query `enriched_text.entities.type: cccardnumber` will return all results that include a credit card number of the specified type.


## Machine Learning enrichments
{: #machinelearning-enrichment}

This enrichment uses models created in {{site.data.keyword.knowledgestudiofull}} for {{site.data.keyword.icp4dfull}} to enrich your collection. There are two types of models:

-  Rule-based models that find entities in documents based on rules that you define. (File format: `.pear`)
-  Machine learning models that understand the linguistic nuances, meaning, and relationships specific to your industry (file format: `.zip`)

Create your `.pear` or `.zip` file before adding this enrichment. See the documentation for [{{site.data.keyword.knowledgestudiofull}} for {{site.data.keyword.icp4dfull}}](https://cloud.ibm.com/docs/services/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-wks_overview_full
){: external} for more information.

The enrichment will be applied only to the field(s) you specify on the [Enrich fields](/docs/services/discovery-data?topic=discovery-data-enrich-fields#enrich-fields) screen.

Enrichment-specific fields:

-  **Select a .pear or .zip file** - Select the model and upload it.

**Example - Rule-based model:**

The example model extracts several entity types, including `person`, `surname`, and `position`. When this model is applied as an enrichment to a field, it extracts all entity types in that field that were specified in the {{site.data.keyword.knowledgestudiofull}} rule-based model.  

```
rules.pear (not available for download)
```

In the output, the information extracted by the Machine Learning enrichment (rule-based model) can be found under `enriched_text`, within the `entities` array.

In this example snippet, the field selected for enrichment was `text`.

In the JSON output:
 -  `path` = the facet path of the entity
 -  `text` = the text in the document that the rule has matched to the `type`
 -  `type` = entity type 
 

```JSON
"enriched_text": [
  {
    "entities": [
      {
        "path": ".wksrule.entities.PERSON",
        "text": "George Washington",
        "type": "PERSON"
      },
      {
         "path": ".wksrule.entities.GIVENNAME",
         "text": "George",
         "type": "GIVENNAME"
      },
      {
         "path": ".wksrule.entities.SURNAME",
         "text": "Washington",
         "type": "SURNAME"
      },                    
      {
         "path": ".wksrule.entities.POSITION",
         "text": "politician",
         "type": "POSITION"
      },
      {
         "path": ".wksrule.entities.POSITION",
         "text": "soldier",
         "type": "POSITION"
      },
      {
        "path": ".wksrule.entities.JOBTITLE",
        "text": "President of the United States",
        "type": "JOBTITLE"
      },
      . . .  
],
. . .
"text": [
  "George Washington (February 22, 1732‚ December 14, 1799) was an American politician and soldier who served as the first President of the United States from 1789 to 1797 and was one of the Founding Fathers of the United States."
] 
```	

Result: The query `enriched_text.entities.type:position` will return all documents that include a `type` of `position`.

**Example - Machine learning model:**

Machine learning models will extract entity types (including `person`, `oranization`, and `date`) as well as relations. When this model is applied as an enrichment to a field, it uses machine learning to understand the linguistic nuances, meaning, and relationships.

```
ml.zip (not available for download)
```

In the output, the information extracted by the Machine Learning enrichment (machine learning model) can be found under `enriched_text`, within the `entities` and the `relations` arrays.

In this example snippet, the field selected for enrichment was `text`.

In the JSON output:
 -  `count` = number of times the `text` occurs
 -  `text` = the text in the document that validates the `type`
 -  `type` = entity type 
 

```JSON
"enriched_text": [
  {
    "entities": [
      {
        "count": 1,
        "text": "Democratic Party",
        "type": "ORGANIZATION"
      },
      {
        "count": 1,
        "text": "March 15, 1767",
        "type": "DATE"
      },
      {
        "count": 1,
        "text": "President",
        "type": "POSITION"
      },
      {
        "count": 1,
        "text": "Andrew Jackson",
        "type": "PERSON"
       },
           . . . 
    "relations": [
			{
			  "sentence": "Andrew Jackson (March 15, 1767‚ June 8, 1845) was an American soldier and statesman who served as the seventh President of the United States from 1829 to 1837 and was the founder of the Democratic Party.",         
           . . .              
] 
```	