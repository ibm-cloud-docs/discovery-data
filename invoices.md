---

copyright:
  years: 2018, 2020
lastupdated: "2020-12-04"

keywords: invoice,invoices,invoice parsing,parsing,invoice understanding

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:note: .note}
{:important: .important}
{:preview: .preview}

# Understanding the Invoices enrichment
{: #invoices}

![Cloud Pak for Data only](images/cpdonly.png)</br>

The `Invoices` enrichment is included with {{site.data.keyword.discoveryshort}} for Content Intelligence for Cloud Pak for Data. For more information, see [Understanding {{site.data.keyword.discoveryshort}} for Content Intelligence](/docs/discovery-data?topic=discovery-data-output_schema).
{: shortdesc}

You can analyze invoice documents by using the `Invoices` enrichment.

The `Invoices` enrichment returns the following schema.

```json
{
    "buyers": [
        {
            "location": {
                "begin": int,
                "end": int
            },
            "text": string,
            "provenance_ids": [ string, string, ... ]
        }
    ],
    "suppliers": [
        {
            "location": {
                "begin": int,
                "end": int
            },
            "text": string,
            "provenance_ids": [ string, string, ... ]
        }
    ],
    "totals_due": [
        {
            "amount": {
                "location": {
                    "begin": int,
                    "end": int
                },
                "text": string,
                "provenance_ids": [ string, string, ... ]
            },
            "currency": {
                "location": {
                    "begin": int,
                    "end": int
                },
                "text": string,
                "text_normalized": string,
                "provenance_ids": [ string, string, ... ]
            }
        }
    ],
    "currencies": [
        {
            "location": {
                "begin": int,
                "end": int
            },
            "text": string,
            "text_normalized": string,
            "provenance_ids": [ string, string, ... ]
        }
    ],
    "purchase_order_numbers": [
        {
            "location": {
                "begin": int,
                "end": int
            },
            "text": string,
            "provenance_ids": [ string, string, ... ]
        }
    ],
    "invoice_numbers": [
        {
            "location": {
                "begin": int,
                "end": int
            },
            "text": string,
            "provenance_ids": [ string, string, ... ]            
        }
    ],
    "invoice_dates": [
        {
            "location": {
                "begin": int,
                "end": int
            },
            "text": string,
            "text_normalized": string,
            "provenance_ids": [ string, string, ... ]
        }
    ],
    "due_dates": [
        {
            "location": {
                "begin": int,
                "end": int
            },
            "text": string,
            "text_normalized": string,
            "provenance_ids": [ string, string, ... ]
        }
    ],
    "invoice_parts": [
        {
            "quantity_ordered": {
                "location": {
                    "begin": int,
                    "end": int
                },
                "text": string,
                "provenance_ids": [ string, string, ... ]
            },
            "part_description": {
                "location": {
                    "begin": int,
                    "end": int
                },
                "text": string,
                "provenance_ids": [ string, string, ... ]
            },
            "unit_price": {
                "amount": {
                    "location": {
                        "begin": int,
                        "end": int
                    },
                    "text": string,
                    "provenance_ids": [ string, string, ... ]
                },
                "currency": {
                    "location": {
                        "begin": int,
                        "end": int
                    },
                    "text": string,
                    "text_normalized": string,
                    "provenance_ids": [ string, string, ... ]
                }
            }
        }
    ]
}
```

## Schema arrangement
{: #invoices-schema-arrangement}

The `Invoices` schema is arranged as follows.

  - `buyers`: An array of buyers listed in the invoice. A buyer is defined as a party responsible paying for the goods, services, or both.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: Text regarding a buyer or buyers.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `suppliers`: An array of suppliers listed in the invoice. A supplier is defined as a party responsible for providing the goods, services, or both.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: Text regarding a supplier or suppliers.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `totals_due`: Total amount due after taxes.
    - `amount`: An amount due.
      - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
      - `text`: The amount due.
      - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
    - `currency`: The currency in which the specified amount is due.
      - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
      - `text`: The name of the currency in which the specified amount is due.
      - `text_normalized`: The normalized form of the value of the `text` field, if applicable, listed as a string in [ISO-4217](https://www.iso.org/iso-4217-currency-codes.html) format. This element is optional; it is returned only if normalized text exists.
      - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `currencies`: An array of currencies listed in the invoice.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: The name of the currency in which the specified amount is due.
    - `text_normalized`: The normalized form of the value of the `text` field, if applicable, listed as a string in [ISO-4217](https://www.iso.org/iso-4217-currency-codes.html) format. This element is optional; it is returned only if normalized text exists.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `purchase_order_numbers`: An array listing purchase-order (PO) numbers in the invoice. The PO is a document that is generated by the buyer to authorize a purchase transaction. The PO number uniquely identifies a purchase order and is generally defined by the buyer. The buyer matches the PO number in the invoice to the purchase order.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: A PO number.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `invoice_numbers`: An array of invoice numbers. An invoice number is a number assigned by a part to identify the unique invoice.
    - `location`: The location of the invoice number as defined by its `begin` and `end` indexes.
    - `text`: An invoice number.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `invoice_dates`: An array of invoice dates. An invoice date is the date on which the invoice was issued.
    - `location`: The location of the invoice date as defined by its `begin` and `end` indexes.
    - `text`: The invoice date.
    - `text_normalized`: The normalized version of the invoice date in `YYYY-MM-DD` format. This element is optional; it is returned only if normalized text exists.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `due_dates`: An array of due dates. A due date is the date on which a payment for a certain invoice is due. It is typically defined in the contract as a certain number of days following the invoice date.
    - `location`: The location of the due date as defined by its `begin` and `end` indexes.
    - `text`: The due date.
    - `text_normalized`: The normalized version of the due date in `YYYY-MM-DD` format. This element is optional; it is returned only if normalized text exists.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `invoice_parts`: An array of invoice parts. An invoice part is a unit of goods, services, or both specified in the invoice.
    - `quantity_ordered`: The number of a specified invoice part ordered by the buyer from the supplier.
      - `location`: The location of the quantity ordered. as defined by its `begin` and `end` indexes.
      - `text`: The quantity ordered.
      - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
    - `part_description`: The description of the specified invoice part.
      - `location`: The location of the part description as defined by its `begin` and `end` indexes.
      - `text`: The part description.
      - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
    - `unit_price`: The price per unit of the ordered good or service.
      - `amount`: A unit price.
        - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
        - `text`: The unit price.
        - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
      - `currency`: The currency used by the unit price.
        - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
        - `text`: The name of the currency.
        - `text_normalized`: The normalized form of the value of the `text` field, if applicable, listed as a string in [ISO-4217](https://www.iso.org/iso-4217-currency-codes.html) format. This element is optional; it is returned only if normalized text exists.
        - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.

Sample output resembles the following:

```json
{
  "buyers": [ 
    {
      "location": {
        "begin": 6701,
        "end": 6723
    },
    "text": "IBM Middle East-FZ LLC",
    "provenance_ids": ["I755","I112"]  
    } 
  ],
  "suppliers": [ 
    {
      "location": {
        "begin": 36695,
        "end": 36717
    },
    "text": "Ricoh International BV",
    "provenance_ids": ["I234","I123"] 
    } 
  ],
  "totals_due": [ 
    {
      "amount": {
        "location" : {
          "begin": 35400,
          "end": 35410
        },
        "text": "145,641.91",
        "provenance_ids": ["I212"]
      },
      "currency": {
        "location": {
          "begin": 33827,
          "end": 33830
        },
        "text": "EUR",
        "text_normalized": "EUR",
        "provenance_ids": ["I3143"]
      }
    } 
  ],
  "currencies": [
    {
      "location": {
        "begin": 33827,
        "end": 33830
      },
      "text": "EUR",
      "provenance_ids": ["I3143"]
    }, 
    {
      "location": {
        "begin": 34605,
        "end": 34608
      },
      "text": "EUR",
      "text_normalized": "EUR",
      "provenance_ids": ["I7678", "I2832"]
    }
  ],
  "purchase_order_numbers" : [ 
    {
      "location": {
        "begin": 11501,
        "end": 11511
      },
      "text": "4603344312",
      "provenance_ids": ["I7795"]
    }
  ],
  "invoice_numbers": [ 
    {
      "location": {
        "begin": 2982,
        "end": 2990
      },
      "text": "52156277",
      "provenance_ids": ["I3143", "I676", "I1142"]
    }
  ],
  "invoice_dates": [ 
    {
      "location": {
        "begin": 3237,
        "end": 3246
      },
      "text": "28 February 2018",
      "text_normalized": "2018-02-28",
      "provenance_ids": ["I222", "I354"]
    }
  ],
  "due_dates": [ 
    {
      "location": {
        "begin": 36424,
        "end": 36433
      },
      "text": "29 April 2018",
      "text_normalized":"2018-04-29",
      "provenance_ids": ["I420", "I6060"]
    } 
  ],
  "invoice_parts": [ 
    {
      "quantity_ordered": {
        "location": {
          "begin": 14441,
          "end": 14442
        },
       "text": "1",
       "provenance_ids": ["I890", "I1100", "I456"]
      },
      "part_description": {
        "location": {
          "begin": 13873,
          "end": 13889
        },
        "text": "On-Site Services",
        "provenance_ids": ["I242", "I1181"]
      },
      "unit_price": {
        "amount": {
          "location": {
            "begin": 14926,
            "end": 14935
          },
          "text": "38,720.60",
          "provenance_ids": ["I3122", "I4098", "I909"]
        },
        "currency": {
          "location": {
            "begin": 33827,
            "end": 33830
          },
          "text": "EUR",
          "text_normalized": "EUR",
          "provenance_ids": ["I1122", "I567"]
        }
      }
    }
  ]
}
```
