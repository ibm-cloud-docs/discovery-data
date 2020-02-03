---

copyright:
  years: 2019
lastupdated: "2019-12-18"

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


# Creating enrichments
{: #create-enrichments}

You can create enrichments that will add related terms (**Dictionary**), identify and extract values (**Character Pattern**), extract entities and relationships/apply rules to fields in your collection (**Machine Learning and Watson Explorer Content Analytics Studio models**), classify your documents into categories (**Classifier**), or use an **Advanced rule model**.
{: shortdesc}

The enrichments available will vary based on the **Project type**.

To create a new enrichment: 

1. Open your project and select the **Improve and customize** icon on the navigation panel. On the **Improvement tools** panel, select **Teach domain concepts** and choose the enrichment.
1. Click **Upload** or **New**.
1. Configure the enrichment:
    - [**Dictionary**](/docs/discovery-data?topic=discovery-data-create-enrichments#dictionary-enrichment) 
    - [**Character Pattern**](/docs/discovery-data?topic=discovery-data-create-enrichments#characterpattern-enrichment)
    - [**Machine Learning and Watson Explorer Content Analytics Studio models**](/docs/discovery-data?topic=discovery-data-create-enrichments#machinelearning-enrichment) 
    - [**Classifier**](/docs/discovery-data?topic=discovery-data-create-enrichments#classifier-enrichment)
    - [**Advanced rule models** (beta)](/docs/discovery-data?topic=discovery-data-create-enrichments#advanced-rules)

Other available enrichments: [Extracting meaning](/docs/discovery-data?topic=discovery-data-create-enrichments#extract-meaning) and [Discovery for Content Intelligence](/docs/discovery-data?topic=discovery-data-create-enrichments#content-intelligence).


The enrichment will be applied only to the collection(s) and field(s) you specify, or you can do so later on the [Enrichments](/docs/discovery-data?topic=discovery-data-configuring-fields#enrich-fields) page. The enrichment **Status** should be **Ready** before you apply it.
{: important}


## Dictionary enrichments
{: #dictionary-enrichment}

The Dictionary enrichment allows you to enrich document fields in your collection. The enrichment terms can be synonyms (car, automotive, auto), or words in the same category (carburetor, piston, valves). 

You can create a new dictionary using the tooling, or you can upload a dictionary csv file. The enrichment will be applied only to the collection(s) and field(s) you specify after you create your dictionary, or you can do so later on the [Enrichments](/docs/discovery-data?topic=discovery-data-configuring-fields#enrich-fields) page.

To create a new dictionary:

1. Select the **New** button.
1. Name your dictionary and choose the language.
1. Enter a term and select the **+** button. Continue adding terms. When enough terms have been added, addtional terms will be suggested.
1. Click **Save dictionary**.
1. Choose the collections(s) and fields(s) you want to apply the dictionary to and click **Apply**. 

Dictionary suggestions will not generate unless the **Parts of Speech** enrichment is turned on.
{: tip}

To upload a dictionary:

1. Select the **Upload** button.
1. Name your dictionary and choose the language.
1. Enter the **Facet Path**, which is used as a field value in the index. To specify hierarchy, use a period `.` to separate values, for example `automobiles.motorsports`.
1. Choose the .csv file to upload and click the **Create** button.

Dictionary files must be .csv files using UTF-8 encoding in the following format. For example:

```
engine,gasket,carburetor,piston,valves
racing,stock,open,indy,drag
flag,checkered,green,caution,yellow,red
```

Each line of the csv file is a separate enrichment. For example, this line: `engine,gasket,carburetor,piston,valves` will apply the enrichment `engine` to the specified field(s) in your collection that contain the terms `engine`,`gasket`,`carburetor`,`piston`, or `valves`.

In this example, the **Facet Path** specified was `automobiles.motorsports`, and the field selected for enrichment was `text`. The dictionary enrichment can be found under `enriched_text`, within the `entities` array.

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

The enrichment will be applied only to the collection(s) and field(s) you specify after you create the enrichment, or you can do so later on the [Enrichments](/docs/discovery-data?topic=discovery-data-configuring-fields#enrich-fields) page.  

Enrichment-specific fields:

-  **Facet Path** - The text matched to this regular expression will be included in this facet. To specify hierarchy, use a period `.` to separate values, for example `regex.cccardnumber`.
-  **Character Pattern** - Your regular expression string. 

Notes about writing regular expressions:

-  Use a Java&trade; regular expression. See the [Java documentation](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html){: external} for more information. 
-  Your regular expression should be short and understandable.
-  The optimal regular expression would lead to a match or a non-match quickly.
-  It is best to extract common patterns. For example, use `a(b|c|d)` instead of `(ab|ac|ad)`.
-  The regular expression engine may fail if it backtracks because it can't make a negative match towards the end of the string and then attempts too many permutations. To avoid this, consider using a possessive quantifier, for example, `(a+b*)++c`.

**Example:**

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


## Machine Learning enrichments and Watson Explorer Content Analytics Studio models
{: #machinelearning-enrichment}

This enrichment uses models created in {{site.data.keyword.knowledgestudiofull}} for {{site.data.keyword.icp4dfull}} or Watson Explorer Content Analytics Studio to enrich your collection. There are three types of models:

-  Rule-based models created in {{site.data.keyword.knowledgestudiofull}} for {{site.data.keyword.icp4dfull}}  that find entities in documents based on rules that you define. (File format: `.pear`)
-  Machine learning models created in {{site.data.keyword.knowledgestudiofull}} for {{site.data.keyword.icp4dfull}} that understand the linguistic nuances, meaning, and relationships specific to your industry (file format: `.zip`)
-  Custom UIMA text analysis models created in Watson Explorer Content Analytics Studio. (File format: `.pear`)

Create your `.pear` or `.zip` file before adding this enrichment. See the following documentation for more information:
  -  [{{site.data.keyword.knowledgestudiofull}} for {{site.data.keyword.icp4dfull}}](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-wks_overview_full
)
  -  [Watson Explorer Content Analytics Studio](https://www.ibm.com/support/knowledgecenter/en/SS8NLW_11.0.2/com.ibm.discovery.es.ta.doc/iiystacastudio.html){: external}

The enrichment will be applied only to the collection(s) and field(s) you specify after you create the enrichment, or you can do so later on the [Enrichments](/docs/discovery-data?topic=discovery-data-configuring-fields#enrich-fields) page. 

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

## Advanced rule models enrichment (beta)
{: #advanced-rules}

This beta enrichment uses a text extraction model created and exported from the Advanced Rule Editor of {{site.data.keyword.knowledgestudiofull}} for {{site.data.keyword.icp4dfull}} (file format: `.zip`). 

The Advanced rule models enrichment is currently supported only as a beta capability. See [Beta features](/docs/discovery-data?topic=discovery-data-release-notes#beta-features) in the Release notes for more information.  
{: note}

The enrichment will be applied only to the collection(s) and field(s) you specify after you create the enrichment, or you can do so later on the [Enrichments](/docs/discovery-data?topic=discovery-data-configuring-fields#enrich-fields) page. 

Enrichment-specific fields:

-  **Result field** - Field in the index that will contain the output of this enrichment.
-  **Collection language** - Select the language of your `.zip` file.
-  **Select a .zip file** - Select the file and upload it.

For more information, see the documentation for [{{site.data.keyword.knowledgestudiofull}} for {{site.data.keyword.icp4dfull}}](/docs/watson-knowledge-studio-data?topic=watson-knowledge-studio-data-create-advanced-rules-model).

## Classifier enrichments
{: #classifier-enrichment}

The Classifier enrichment allows you to classify the documents in your collection into categories. {{site.data.keyword.discovery-data_short}} uses the labels and text examples you have specified to predict the categories of the documents in your collection. 

You must create and upload a classifier csv file to apply this enrichment. The enrichment will be applied only to the collection(s) and field(s) you specify after you create the enrichment, or you can do so later on the [Enrichments](/docs/discovery-data?topic=discovery-data-configuring-fields#enrich-fields) page. 

Enrichment-specific fields:

-  **Collection language** - Select the language of your classifier `.csv` file.
-  **Select a .csv file** - Select the file and upload it.

After you upload the csv file, the Classifier enrichment is not ready to use until the **Status** changes from `Training` to `Ready` on the **Enrichments** page. You may need to refresh the page to view the updated status.
{: important}

Classifier .csv file requirements:

-  The .csv file must use UTF-8 encoding.
-  The format is `text`,`label`. The `text` is the example text, and the `label` is the category.
-  The .csv must have at least two columns, with no header. The first column contains the `text` and the second column contains the `label`. You can add additional `label` columns if you need to apply more than one label to the `text` column. (`text`,`label`,`label`)
-  There should be at least ten examples (10 `text`,`label` pairs) for each `label`. The minimum is 3 examples. The more examples you provide per label, the more accurately the classifier will predict the categories of the documents in your collection. 

**Example:**

This .csv file could be used to classify conference attendee feedback.

```
The rooms were too cold.,facility_temperature
Breakfast did not include gluten-free options.,catering
The rooms were too warm.,facility_temperature
I was very comfortable in the session rooms.,facility_temperature
The awards dinner was delicious.,catering
Coffee ran out during one of the breaks.,catering
The temperature was not comfortable.,facility_temperature
I was very happy with the selection at lunch.,catering
It was nice that you provided tea and coffee. Tea drinkers are often ignored.,catering
Can you turn up the air conditioning? I was very warm.,facility_temperature
My teeth were chattering because I was so cold.,facility_temperature
The speaker left the room to find someone to adjust the temperature.,facility_temperature
Would you consider an all-vegan menu next year?,catering
I would like lemonade and iced tea to be served during the breaks.,catering
The lunch staff was excellent.,catering
Appreciated the fresh blueberry muffins at breakfast.,catering
The hotel staff adjusted the temperature in my session room as soon as I asked. Excellent service!,facility_temperature
Every meal was delicious and there was something for everyone.,catering
The seats under the skylights were not comfortable. Too hot.,facility_temperature
I was comfortable everywhere in the conference center. I never needed my emergency sweater.,facility_temperature
```

In the output, the classifier enrichment applied the `facility_temperature` label to this document in the collection. The `label` can be found under `enriched_text`, within the `classes` array.

In this example snippet, the field selected for enrichment was `text`.

```JSON
"enriched_text": [
  {
    "classes": [
	  {
	    "score": 0.999692440032959,
		  "label": "facility_temperature"
	  }
	]
  }
],
. . .
"text": [
  "I think more attendees would stay awake in the sessions if the rooms were colder."
]  
```

## Extracting meaning
{: #extract-meaning}

The **Entities**, **Keywords**, and **Sentiment of documents** enrichments are supported in English only, unless you download and install `ibm-watson-discovery-pack1-prod` from Passport Advantage.
{: note}

### Entities
{: #entities}

Identifies people, cities, organizations, and other entities in the content. 

For example:

**Input**
> text: "IBM is an American multinational technology company headquartered in Armonk, New York, United States, with operations in over 170 countries."

**Response**
> IBM: Company </br>
> Armonk: Location </br>
> New York: Location </br>
> United States: Location

### Parts of speech
{: #pos}

Extracts parts of speech, such as nouns, verbs, adjectives, adverbs, conjunctions, interjections, and numerals.

### Keywords
{: #keywords}

Returns important keywords in the content. For example:

**Input**
>url: "[http://www.ibm.com/press/us/en/pressrelease/51493.wss](http://www.ibm.com/press/us/en/pressrelease/51493.wss)"

**Response**
>Australian Open </br>
>Tennis Australia </br>
>IBM SlamTracker analytics

### Sentiment of documents
{: #sentiment}

Extracts the positive, neutral, and negative sentiments of the overall document. For example:

**Input**
>text: "Thank you and have a nice day!"

**Response**
>Positive sentiment (score: 0.91)


## Discovery for Content Intelligence
{: #content-intelligence}

The `Contracts`, `Invoices`, and `Purchase orders` enrichments are available if you have purchased and installed {{site.data.keyword.discovery-data_short}} for Content Intelligence and chosen the **Project type** of **Document retrieval**.
{: note}

For more information, see [Understanding Discovery for Content Intelligence](/docs/discovery-data?topic=discovery-data-output_schema).
