---

copyright:
  years: 2018, 2021
lastupdated: "2021-02-26"

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

# Understanding the Contracts enrichment
{: #contracts-schema}

The `Contracts` enrichment is available with Document Retrieval for Contract project types.
{: shortdesc}

After a document is processed by the `Contracts` enrichments, the service provides JSON output in the following schema. For definitions of each element, see [Understanding contract analysis](/docs/discovery-data?topic=discovery-data-contract_parsing).

```json
{
  "elements": [
    {
      "location": { 
        "begin": int,
        "end": int
      },
      "text": string,
      "types": [
        {
          "label": { "nature": string, "party": string },
          "provenance_ids": [string, string, ...]
            ...
          ]
        }
        ...
      ],
      "categories": [
        {
          "label": string,
          "provenance_ids": [string, string, ...]
        }
        ...
      ],
      "attributes": [
        {
          "type": string,
          "text": string,
          "location": { "begin": int, "end": int }
         }
      ]
    }
    ...
  ],
  "effective_dates": [
    {
      "confidence_level": string,
      "text": string,
      "text_normalized": string,
      "provenance_ids": [ string, string, ... ],
      "location": { "begin": int, "end": int }
     },
     ...
  ],
  "contract_amounts": [
    {
      "confidence_level": string,
      "text": string,
      "text_normalized": string,
      "interpretation": {
        "value": string,
        "numeric_value": number,
        "unit": string,
      },
      "provenance_ids": [ string, string, ... ],
      "location": { "begin": int, "end": int }
    },
    ...
  ],
  "termination_dates": [
    {
      "confidence_level": string,
      "text": string,
      "text_normalized": string,
      "provenance_ids": [ string, string, ... ],
      "location": { "begin": int, "end": int }
    },
    ...
  ],
  "contract_types": [
    {
      "confidence_level": string,
      "text": string,
      "provenance_ids": [ string, string, ... ],
      "location": { "begin": int, "end": int }
    },
    ...
  ],
  "contract_terms": [
    {
      "confidence_level": string,
      "text": string,
      "text_normalized": string,
      "interpretation": {
        "value": string,
        "numeric_value": number,
        "unit": string,
      },
      "provenance_ids": [ string, string, ... ],
      "location": { "begin": int, "end": int }
    },
    ...
  ],
  "payment_terms": [
    {
      "confidence_level": string,
      "text": string,
      "text_normalized": string,
      "interpretation": {
        "value": string,
        "numeric_value": number,
        "unit": string,
      },
      "provenance_ids": [ string, string, ... ],
      "location": { "begin": int, "end": int }
    },
    ...
  ],
  "contract_currencies": [
    { 
      "confidence_level" : string,
      "text" : string,
      "text_normalized" : string, 
      "provenance_ids": [string, string ..],
      "location": { "begin": int, "end": int }
    },
  ...
],
  "tables": [],
  "document_structure": {
    "section_titles": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "level": int,
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ],
    "leading_sentences": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ],
    "paragraphs": [
      {
        "location": {
           "begin": int,
           "end": int
         }
      },
      ...
    ]
      },
      ...
    ]
  },
  "parties": [
    {
      "party": string,
      "role": string,
      "importance": string,
      "addresses": [
        {
          "text": string,
          "location": {
            "begin": int,
            "end": int
          }
        },
        ...
      ],
      "contacts": [
        {
          "name": string,
          "role": string 
        },
        ...
      ],
      "mentions": [
        {
          "text": string,
          "location": {
            "begin": int,
            "end": int
          }
        },
        ...
      ]
    },
    ...
  ]
}
```

## Schema arrangement
{: #schema-arrangement}

The `contracts` schema is arranged as follows.

  - `elements`: An array of the document elements detected by the service.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: The text of the element.
    - `types`: An array that describes what the element is and whom it affects.
      - `label`: An object that defines the type by using a pair of the following elements:
        - `nature`: The type of action the sentence requires. Current values are `Definition`, `Disclaimer`, `Exclusion`, `Obligation`, and `Right`.
        - `party`: A string that identifies the party to whom the sentence applies.
      - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
    - `categories`: An array that lists the functional categories into which the element falls; in other words, the subject matter of the element.
      - `label`: A string that lists the identified category. You can find a list of [categories](/docs/discovery-data?topic=discovery-data-contract_parsing#contract_categories) in [Understanding contract anaysis](/docs/discovery-data?topic=discovery-data-contract_parsing).
      - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
    - `attributes`: An array that identifies document attributes. Each object in the array consists of three elements:
      - `type`: The type of attribute. Possible values are `Currency`, `DateTime`, `Duration`, `Location`, `Number`, `Organization`, `Percentage`, and `Person` as described at [Attributes](/docs/discovery-data?topic=discovery-data-contract_parsing#attributes).
      - `text`: The text that is associated with the attribute.
      - `location`: The location of the attribute as defined by its `begin` and `end` indexes.
  - `effective_dates`: An array that identifies the date or dates on which the document becomes effective.
    - `confidence_level`: The confidence level of the identification of the effective date. Possible values include `High`, `Medium`, and `Low`.
    - `text`: An effective date, which is listed as a string.
    - `text_normalized`: The normalized form of the effective date, which is listed as a string. This element is optional; that is, the service output lists it only if normalized text exists.
    - `location`: The location of the date as defined by its `begin` and `end` indexes.
    - `provenance_ids`: An array that contains zero or more keys. Each key is a hashed value that you can send to IBM to provide feedback or receive support.
  - `contract_amounts`: An array that monetary amounts that identify the total amount of the contract that needs to be paid from one party to another.
    - `confidence_level`: The confidence level of the identification of the contract amount. Possible values include `High`, `Medium`, and `Low`.    
    - `text`: A contract amount, which is listed as a string.
    - `location`: The location of the amount or amounts as defined by its `begin` and `end` indexes.
    - `provenance_ids`: An array that contains zero or more keys. Each key is a hashed value that you can send to IBM to provide feedback or receive support.
  - `termination_dates`: An array that identifies the date or dates on which the document is to be terminated.
    - `confidence_level`: The confidence level of the identification of the termination date. Possible values include `High`, `Medium`, and `Low`.    
    - `text`: A termination date, which is listed as a string.
    - `text_normalized`: The normalized form of the termination date, which is listed as a string. This element is optional; that is, the service output lists it only if normalized text exists.
    - `location`: The location of the date as defined by its `begin` and `end` indexes.
    - `provenance_ids`: An array that contains zero or more keys. Each key is a hashed value that you can send to IBM to provide feedback or receive support.
  - `contract_types`: An array that identifies the document's contract type or types.
    - `confidence_level`: The confidence level of the identification of the contract type. Possible values include `High`, `Medium`, and `Low`.
    - `text`: A contract type, which is listed as a string.
    - `provenance_ids`: An array that contains zero or more keys. Each key is a hashed value that you can send to IBM to provide feedback or receive support.
    - `location`: The location of the contract type as defined by its `begin` and `end` indexes.
  - `contract_terms`: An array that identifies the duration or durations of the contract.
    - `confidence_level`: The confidence level of the identification of the contract terms. Possible values include `High`, `Medium`, and `Low`.
    -  `text`: A contract term, which is listed as a string.
    - `provenance_ids`: An array that contains zero or more keys. Each key is a hashed value that you can send to IBM to provide feedback or receive support.
    - `location`: The location of the contract term as defined by its `begin` and `end` indexes.
  - `payment_terms`: An array that identifies the document's payment duration or durations.
    - `confidence_level`: The confidence level of the identification of the payment term. Possible values include `High`, `Medium`, and `Low`.
    - `text`: A payment term, which is listed as a string.
    - `text_normalized`: The normalized text, if applicable.
    - `interpretation`: The details of the normalized text, if applicable.
      - `value`: A string listing the value that was found in the normalized text.
      - `numeric_value`: An integer or double expressing the numeric value of the `value` key.
      - `unit`\*\*: A string listing the unit of the value that was found in the normalized text.
    - `provenance_ids`: An array that contains zero or more keys. Each key is a hashed value that you can send to IBM to provide feedback or receive support.
    - `location`: The location of the contract term as defined by its `begin` and `end` indexes.
  - `contract_currencies`: An array that identifiea the document's contract currency or currencies.
    - `confidence_level`: The confidence level of the identification of the contract currency. Possible values include `High`, `Medium`, and `Low`.
    - `text`: A contract currency, which is listed as a string.
    - `text_normalized`: The normalized text, if applicable. It is listed as a string in [ISO-4217](https://www.iso.org/iso-4217-currency-codes.html){: external} format
    - `provenance_ids`: An array that contains zero or more keys. Each key is a hashed value that you can send to IBM to provide feedback or receive support.
    - `location`: The location of the contract currency as defined by its `begin` and `end` indexes.
  - `document_structure`: An object that describes the structure of the input document.
    - `section_titles`: An array that contains one object per section or subsection that is detected in the input document. Sections and subsections are not nested. Instead, they are flattened out and can be placed back in order by using the `begin` and `end` values of the element and the `level` value of the section.
      - `text`: A string that lists the section title, if detected.
      - `location`: The location of the title in the input document as defined by its `begin` and `end` indexes.
      - `level`: An integer that indicates the level at which the section is located in the input document. For example,  represents a top-level section,  represents a subsection within the level  section.
      - `element_locations`: An array that specifies the `begin` and `end` values of the sentences in the section.
    - `leading_sentences`: An array that contains one object per leading sentence of a list or subsection, in parallel with the `section_titles` and `paragraph` arrays. The object details the leading sentences in the matching section or subsection. As in the `section_titles` array, the objects are not nested; instead, they are flattened out and can be placed back in order by using the `begin` and `end` values of the element or any level markers in the input document.
      - `text`: A string that lists the leading sentence, if detected.
      - `location`: The location of the leading sentence in the input document as defined by its `begin` and `end` indexes.
      - `element_locations`: An array that specifies the `begin` and `end` values of the leading sentences in the section.
    - `paragraphs`: An array containing one object per paragraph, in parallel with the `section_titles` and `leading_sentences` arrays. Each object lists the span (beginning and end location) of the corresponding paragraph.
      - `location`: The location of the paragraph in the input document as defined by its `begin` and `end` indexes.
  - `parties`: An array that defines the parties that are identified by the service.
    - `party`: A string that provides the normalized form of the party's name.
    - `role`: A string that identifies the role of the party.
    - `importance`: A string that identifies the importance of the party. Possible values include `Primary` for a primary party and `Unknown` for a non-primary party.
    - `addresses`: An array of objects that identify addresses.
      - `text`: A string that contains the address.
      - `location`: The location of the address as defined by its `begin` and `end` indexes.
    - `contacts`: An array that defines the name and role of contacts that are identified in the input document.
      - `name`: A string that lists the name of an identified contact.
      - `role`: A string that lists the role of the identified contact.
    - `mentions`: An array of objects that identify mentions of the party.
      - `text`: A string that lists the name of the party.
      - `location`: The location of the mention as defined by its `begin` and `end` indexes.
  
### \*\*Note on `unit` values
{: #unit-value-note}

The value of `unit` is the [ISO-4217 currency code](https://www.iso.org/iso-4217-currency-codes.html){: external} identified for the currency amount (for example, `USD` or `EUR`). If the service cannot disambiguate a currency symbol (for example, `$` or `£`), the value of `unit` contains the ambiguous symbol as-is.
  
### Note on `location` objects
{: #location-note}

The `location` object is included with the majority of element definitions. The object identifies the location of an element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
  
For example, a `text` string with the value `Amount due` might have a corresponding `location` object such as
```json
{
  ...
  "location": {
    "begin": 2510,
    "end": 2519
  }
  ...
}
  ```
The `begin` index indicates that the string begins at character position `2510` in the transformed HTML; this is the location of the letter `A` in `Amount`. The `end` index indicates that the string ends at character position `2519`; this is the location of the letter `e` in `due`.

## Understanding contract document structure
{: #doc_struct}

The output of the `Contracts` enrichment includes a `document_structure` object that details the structural composition of the input document. 

### Document structure output
{: #struct_output}

Document structure information is represented in the output as follows. The object is located immediately after the top-level `tables` array.

```json
  "document_structure": {
    "section_titles": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "level": int
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ],
    "leading_sentences": [
      {
        "text": string,
        "location": {
          "begin": int,
          "end": int
        },
        "element_locations": [
          {
            "begin": int,
            "end": int
          },
          ...
        ]
      },
      ...
    ],
    "paragraphs": [
       {
         "location": {
           "begin": int,
           "end": int
         }
       },
       ...
    ]
  }
```

### Document structure elements
{: #struct_elements}

The elements of the `document_structure` object contain the following information:

  - `document_structure`: An object describing the structure of the input document.
    - `section_titles`: An array containing one object per section or subsection detected in the input document. Sections and subsections are not nested; instead, they are flattened out and can be placed back in order by using the `begin` and `end` values of the element and the `level` value of the section.
      - `text`: A string listing the section title, if detected.
      - `location`: The location of the title in the input document as defined by its `begin` and `end` indexes.
      - `level`: An integer indicating the level at which the section is located in the input document. For example, `1` represents a top-level section, `2` represents a subsection within the level `1` section, and so forth.
      - `element_locations`: An array containing objects that specify the `begin` and `end` values of the sentences in the section.
    - `leading_sentences`: An array that contains one object per leading sentence of a list or subsection, in parallel with the `section_titles` and `paragraph` arrays. The object details the leading sentences in the matching section or subsection. As in the `section_titles` array, the objects are not nested; instead, they are flattened out and can be placed back in order by using the `begin` and `end` values of the element or any level markers in the input document.
      - `text`: A string listing the leading sentence, if detected.
      - `location`: The location of the leading sentence in the input document as defined by its `begin` and `end` indexes.
      - `element_locations`: An array containing objects that specify the `begin` and `end` values of the leading sentences in the section.
    - `paragraphs`: An array containing one object per paragraph, in parallel with the `section_titles` and `leading_sentences` arrays. Each object lists the span (beginning and end location) of the corresponding paragraph.
      - `location`: The location of the paragraph in the input document as defined by its `begin` and `end` indexes.
