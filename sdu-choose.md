---

copyright:
  years: 2019, 2023
lastupdated: "2023-06-15"

keywords: document structure

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Analyzing documents based on their structure
{: #sdu-choose}

Create a model that understands the content of a document based on the document's format and structure.
{: shortdesc}

First, decide whether you want to use a pretrained model or define your own.

Pretrained model
:   Applies a noncustomizable model that extracts text and identifies tables, lists, and sections.

    Instead of training the model yourself, you can apply an existing model that is trained to identify tables, lists, and sections in various types of documents.

    If capturing information from tables is critical to your use case, consider using a pretrained model.

    For more information, see [Apply a pretrained SDU model](/docs/discovery-data?topic=discovery-data-sdu-pretrained).

User-trained model
:   Opens the Smart Document Understanding tool that you can use to pick certain types of text to store in fields other than the `text` field. 

    When you label a section of a document as a custom field, later you can apply enrichments to the field or split your documents on each occurrence of the field. You can search or filter by the field, or omit the field from the index.

    For more information, see [Define a user-trained SDU model](/docs/discovery-data?topic=discovery-data-configuring-fields).

Text extraction only
:   Indexes any text that is recognized in the source documents in the `text` field. This option is used by default.
