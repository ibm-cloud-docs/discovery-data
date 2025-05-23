---

copyright:
  years: 2019, 2025
lastupdated: "2023-02-28"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Use regular expressions to find terms
{: #domain-regex}

Define regular expressions that capture patterns of significance, such as that `AB10045` is the syntax that is used for your order numbers. 
{: shortdesc}

Define regular expressions that can identify and extract information from fields in your collection.

For example, this regular expression finds occurrences of credit card numbers of a specific format and length.

```text
4[0-9]{15}
```
{: codeblock}

The following regular expression finds occurrences of a US social security number.

```text
(?!666|000|9\d{2})\d{3}-(?!00)\d{2}-(?!0{4})\d{4}
```
{: codeblock}

To add a regular expression, complete the following steps:

1.  From the *Teach domain concepts* section of the *Improvement tools* panel, choose **Regular expression**.
1.  Click **Upload**.
1.  Optional: Specify a facet path to categorize any text that matches the regular expression. The text can be filtered by this facet later.

    If you use a hierarchy of categories, add a period between category names in the facet path to represent the hierarchy. For example, if you are adding a regex that can recognize phone numbers, you might have a facet path such as `international.europe`.
1.  Add the regular expression.

    - Use a Java&trade; regular expression.

      For more information, see the [Java documentation](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html){: external}. Another useful resource is [Regex 101](https://regex101.com/){: external}.
    - Keep the regular expression as short and understandable as possible.
    - The best regular expressions resolve to a match or non-match quickly.
    - Use common patterns. For example, use `a(b|c|d)` instead of `(ab|ac|ad)`.
    - The regular expression engine might fail if it backtracks because it can't make a negative match toward the end of the string and then attempts too many permutations. To prevent backtracks, consider using a possessive quantifier, such as `(a+b*)++c`.
1.  Click **Create**.
1.  Choose the collection and field to search for occurrences of text that match this regular expression pattern.

In the output, the information that is extracted by the regular expression enrichment can be found under `enriched_{field_name}`, within the `entities` array.

In this example, the **Facet Path** is `regex.cccardnumber`, and the field that is selected for enrichment is `text`.

```json
{
  "enriched_text": [
    {
      "entities": [
        {
          "path": ".regex.cccardnumber",
          "type": "cccardnumber",
          "text": "4000000000000000"
        }
      ]
    }
  ],
  "text": [
    "He has 2 phones, 090-1234-5678 and 080-1234-5678. His credit card number is 4000000000000000."
  ]
}
```
{: codeblock}

When you submit test queries from the *Improve and customize* page, you can add a facet that is based on the `enriched_text.entities.model_name` field. As a result, the `cccardnumber` regular expression enrichment that you created is displayed as a facet value by which documents can be filtered. For more information about creating facets, see [Adding facets](/docs/discovery-data?topic=discovery-data-facets#facetexist).

## Regular expression limits
{: #regex-limits}

The number of regular expressions that you can define per service instance depends on your {{site.data.keyword.discoveryshort}} plan type.

| Plan | Regular expressions per service instance |
|--------------|---------------------------------|
| Cloud Pak for Data |                 Unlimited |
| Premium      |                             100 |
| Enterprise |                               100 |
| Plus (includes Trial) |                     20 |
{: caption="Regular expression plan details" caption-side="top"}
