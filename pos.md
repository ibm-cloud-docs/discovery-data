---

copyright:
  years: 2019, 2020
lastupdated: "2020-02-10"

keywords: purchase order,purchase orders,purchase order understanding,purchase order parsing,parsing

subcollection: discovery-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:pre: .pre}
{:note: .note}
{:codeblock: .codeblock}
{:screen: .screen}
{:important: .important}
{:preview: .preview}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Understanding the Purchase orders enrichment
{: #purchase_orders}

<!-- ![Cloud Pak for Data only](images/cpdonly.png) --> The Discovery for Content Intelligence enrichments (`Contracts`, `Invoices`, and `Purchase orders`) are available only if you have purchased and installed Discovery for Content Intelligence and chosen the **Project type** of **Document retrieval**.
{: note}

You can analyze purchase orders by using the `Purchase orders` enrichment.
{: shortdesc}

The `Purchase orders` enrichment returns the following schema.

```json
{
   "buyers": [  
      {  
         "location": {  
            "begin": int,
            "end": int
         },
         "text": string,
         "provenance_ids": [string, string, ...]
      }
   ],
   "purchase_order_numbers":[  
      {  
         "location": {  
            "begin": int,
            "end": int
         },
         "text": string,
         "provenance_ids": [string, string, ...]
      }
   ],
   "purchase_order_dates": [  
      {  
         "location": {  
            "begin": int,
            "end": int
         },
         "text": string,
         "text_normalized": string,
         "provenance_ids": [string, string, ...]
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
         "provenance_ids": [string, string, ...]
      }
   ],
    "payment_terms": [
      {
         "location": {
            "begin": int,
            "end": int
         },
         "text": string,
         "text_normalized": string,
         "interpretation": {
            "value" : string,
            "numeric_value" : int,
            "unit": string
          },
         "provenance_ids": [string, string, ...]
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
         "provenance_ids": [string, string, ...]
      }
   ],
   "suppliers": [  
      {  
         "location": {  
            "begin": int,
            "end": int
         },
         "text": string,
         "provenance_ids": [string, string, ...]
      }
   ],
   "supplier_ids": [  
      {  
         "location": {  
            "begin": int,
            "end": int
         },
         "text": string,
         "provenance_ids": [string, string, ...]
      }
   ],
   "bill_to": [  
      {  
         "location": {  
            "begin": int,
            "end": int
         },
         "text": string,
         "provenance_ids": [string, string, ...]
      }
   ],
   "ship_to": [  
      {  
         "location": {  
            "begin": int,
            "end": int
         },
         "text": string,
         "provenance_ids": [string, string, ...]
      }
   ],
   "invoice_to": [  
      {  
         "location": {  
            "begin": int,
            "end": int
         },
         "text": string,
         "provenance_ids": [string, string, ...]
      }
   ],
   "line_items": [  
      {  
         "item_description": {  
            "location": {  
               "begin": int,
               "end": int
            },
            "text": string,
            "provenance_ids": [string, string, ...]
         },
         "quantity_ordered": {  
            "location": {  
               "begin": int,
               "end": int
            },
            "text": string,
            "provenance_ids": [string, string, ...]
         },
         "unit_price": {  
            "location": {  
               "begin": int,
               "end": int
            },
            "text": string,
            "provenance_ids": [string, string, ...]
         }
      }
   ],
   "total_amounts": [  
      {  
         "location": {  
            "begin": int,
            "end": int
         },
         "text": string,
         "provenance_ids": [string, string, ...]
      }
   ],
   "tax_totals": [  
      {  
         "location": {  
            "begin": int,
            "end": int
         },
         "text": string,
         "provenance_ids" : [string, string, ...]
      }
   ],
   "tax_ids": [  
      {  
         "location": {  
            "begin": int,
            "end": int
         },
         "text": string,
         "provenance_ids" : [string, string, ...]
      }
   ],
   "quote_numbers": [  
      {  
         "location": {  
            "begin": int,
            "end": int
         },
         "text": string,
         "provenance_ids" : [string, string, ...]
      }
   ]

}

```

The schema is arranged as follows.

  - `buyers`: An array of buyers that are listed in the purchase order. A buyer is defined as a party responsible paying for the goods, services, or both.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: Text that pertains to a buyer or buyers.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `purchase_order_numbers`: An array of purchase-order numbers that are listed in the input document.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: Text that identifies a purchase-order number.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `purchase_order_dates`: An array of purchase-order dates that are listed in the input document.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: Text regarding a purchase-order date.
    - `text_normalized`: The normalized form of the purchase-order date in the format `YYYY-MM-DD`.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `due_dates`: An array of due dates that are listed in the input document.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: Text regarding a due date.
    - `text_normalized`: The normalized form of the due date in the format `YYYY-MM-DD`.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `payment_terms`: An array of payment terms that are listed in the input document.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: Text regarding payment terms.
    - `text_normalized`: The normalized form of the value of the `text` field. This element is optional; it is returned only if normalized text exists.
    - `interpretation`: The details of the normalized text, if applicable.
        - `value`: A string that lists the value that was found in the normalized text.
        - `numeric_value`: An integer or double that expresses the numeric value of the `value` key.
        - `unit`: A string that lists the unit of the value that was found in the normalized text.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `currencies`: An array of currencies that are listed in the input document.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: The name of the currency in which the specified amount is due.
    - `text_normalized`: The normalized form of the value of the `text` field, listed as a string in [ISO-4217 currency code](https://www.iso.org/iso-4217-currency-codes.html){: external} format. This element is optional; it is returned only if normalized text exists.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `suppliers`: An array of suppliers that are listed in the input document.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: Text regarding a supplier or suppliers.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `supplier_ids`: An array of supplier identifiers that are listed in the input document.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: Text regarding a supplier identifier or identifiers.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `bill_to`: An array of buyer names that are listed in the input document.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: Text regarding a buyer name or names.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `ship_to`: An array of shipping addresses that are identified in the input document.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: Text regarding a shipping address or addresses.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `invoice_to`: An array of buyers who receive purchase orders.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: Text regarding a buyer or buyers who receive purchase orders.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `line_items`: An array that describes the line items that are identified in the input document. Each line item consists of the following objects:
    - `item_description`: A description of the item.
      - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
      - `text`: Text describing the line item.
      - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
    - `quantity_ordered`: The quantity of the item that is being ordered.
      - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
      - `text`: The quantity ordered.
      - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
    - `unit_price`: The unit price per item.
      - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
      - `text`: The unit price of the specified item.
      - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `total_amounts`: An array that lists the total amount or amounts due for the purchase order.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: The total amount or amounts.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `tax_totals`: An array that lists the total amount of taxes specified in the purchase order.
     - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: The total tax amount.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `tax_ids`: An array that lists the tax identifiers specified in the purchase order.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: The tax identifier.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support.
  - `quote_numbers`: An array that lists the quote numbers specified in the purchase order.
    - `location`: An object that identifies the location of the element. The object contains two index numbers, `begin` and `end`. The index numbers indicate the beginning and ending positions, respectively, of the element as character numbers in the HTML document that the service created from your input document.
    - `text`: The quote number.
    - `provenance_ids`: An array of one or more hashed values that you can send to IBM to provide feedback or receive support. 
    
Sample output resembles the following:

```json
{
  "currencies" : [ {
    "location" : {
      "begin" : 8960,
      "end" : 8972
    },
    "text" : "U.S. Dollars",
    "text_normalized" : "USD",
    "provenance_ids": ["P12234"]
  } ],
  "payment_terms" : [ {
    "location" : {
      "begin" : 6627,
      "end" : 6638
    },
    "text" : "net 60 days",
    "text_normalized" : "60 days",
    "interpretation": {
        "value" : "60",
        "numeric_value" : 60,
        "unit": "days"
    },
    "provenance_ids": ["P12234"]
  } ],
  "total_amounts" : [ {
    "location" : {
      "begin" : 10833,
      "end" : 10840
    },
    "text" : "1000.00",
    "provenance_ids": ["P12234"]
  } ],
  "bill_to" : [ ],
  "purchase_order_dates" : [ {
    "location" : {
      "begin" : 3741,
      "end" : 3752
    },
    "text" : "27-JAN-2018",
    "text_normalized": "2018-01-27",
    "provenance_ids": ["P12234"]
  } ],
  "due_dates": [ {
    "location": {
      "begin": 2324,
      "end": 2332
    },
    "text": "29-APR-18",
    "text_normalized": "2018-04-29",
    "provenance_ids": ["P12234"]
  } ],
  "invoice_to" : [ ],
  "purchase_order_numbers" : [ {
    "location" : {
      "begin" : 2796,
      "end" : 2804
    },
    "text" : "78237634",
    "provenance_ids": ["P12234"]
  } ],
  "buyers" : [ {
    "location" : {
      "begin" : 11180,
      "end" : 11191
    },
    "text" : "Vinay Kumar",
    "provenance_ids": ["P12234"]
  } ],
  "ship_to" : [ {
    "location" : {
      "begin" : 1612,
      "end" : 1633
    },
    "text" : "45 Main Street Bhopal",
    "provenance_ids": ["P12234"]
  } ],
  "suppliers" : [ {
    "location" : {
      "begin" : 2011,
      "end" : 2026
    },
    "text" : "IBM Corporation",
    "provenance_ids": ["P12234"]
  } ],
  "line_items" : [ {
    "quantity_ordered" : {
      "location" : {
        "begin" : 9669,
        "end" : 9670
      },
      "text" : "1",
      "provenance_ids": ["P12234"]
    },
    "item_description" : {
      "location" : {
        "begin" : 9420,
        "end" : 9442
      },
      "text" : "IBM SW Annual License ",
      "provenance_ids": ["P12234"]
    },
    "unit_price" : {
      "location" : {
        "begin" : 10128,
        "end" : 10136
      },
      "text" : "1000.00 ",
      "provenance_ids": ["P12234"]
    }
  }, {
    "quantity_ordered" : {
      "location" : {
        "begin" : 10361,
        "end" : 10362
      },
      "text" : "1",
      "provenance_ids": ["P12234"]
    },
    "item_description" : {
      "location" : {
        "begin" : 9420,
        "end" : 9442
      },
      "text" : "IBM SW Annual License ",
      "provenance_ids": ["P12234"]
    },
    "unit_price" : {
      "location" : {
        "begin" : 10128,
        "end" : 10136
      },
      "text" : "1000.00 ",
      "provenance_ids": ["P12234"]
    }
  } ],
  "supplier_ids" : [ {
    "location" : {
      "begin" : 5124,
      "end" : 5129
    },
    "text" : "98457",
    "provenance_ids": ["P12234"]
  } ],
  "total_amounts": [ {
    "text": "17,788.80",
    "location": {
      "begin": 23945,
      "end": 23954
    },
    "provenance_ids" : ["P12234"]
  } ],
  "tax_totals": [ {
    "text": "0.00",
    "location": {
      "begin": 21279,
      "end": 21283
    },
    "provenance_ids": ["P12234"]
  } ],
  "tax_ids": [ {
    "text": "13-0871985",
    "location": {
      "begin": 5071,
      "end": 5079
    },
    "provenance_ids": ["P12234"]
  } ],
  "quote_numbers": [ {
    "text": "17509437",
    "location": {
      "begin": 19689,
      "end": 19697
    },
    "provenance_ids": ["P12234"]
  } ]  
}
```
