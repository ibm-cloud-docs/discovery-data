---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-06"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting ingestion
{: #troubleshoot-ingestion}

Learn about solutions and workarounds to problems you might encounter when you add data to a collection.
{: shortdesc}

This information applies both to managed and installed instances of {{site.data.keyword.discoveryshort}}. For more troubleshooting tips for installed deployments only, see [Troubleshooting {{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}} deployments](/docs/discovery-data?topic=discovery-data-troubleshoot).
{: note}

## Microsoft document troubleshooting tips
{: #upload-data-ts-ms}

Failed to prepare document for SDU processing
:    Some DOC, PPT, and XSL files that use older features which are no longer supported by Microsoft Office can cause ingestion issues. If you encounter this issue, open the file in a more recent version of Microsoft Office and convert the file to the DOCX, PPTX, or XSLX format respectively, and then upload the DOCX, PPTX, or XSLX file.

Line breaks are inserted randomly to some DOCX files
:    When some DOCX files are added to a collection, line breaks are inserted randomly to the text that is stored in the `html` index field. The unexpected line breaks can impact the efficiency of enrichments, such as custom rule recognition. If you encounter this issue, convert the DOCX file to a PDF file, and then import the PDF file.

After applying a pretrained Smart Document Understanding model to a PPT file, table boundaries are not recognized properly
:    During the conversion process, text that is extracted from the table is confused with text that is outside the table in some PPT pages. This issue is more likely to occur in tables with a lot of text and that have footnotes displayed just outside the table border. If you encounter this issue, export the PPT file as a PDF file, and then upload the PDF file instead. Apply a user-trained Smart Document Understanding (SDU) model to the document, and then use the SDU tool to identify the tables in the document. The resulting model handles table boundaries properly and can extract text from the tables cleanly.

## PDF file troubleshooting tips
{: #upload-data-ts-pdf}

Failed to parse document due to invalid encoding
:    Enable OCR for the file.
