---

copyright:
  years: 2020, 2022
lastupdated: "2022-05-18"

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

Line breaks are inserted randomly
:   When some files in Microsoft Office format are added to a collection, line breaks are inserted seemingly at random to the text that is stored in the `html` field in the collection's index. The unexpected line breaks can impact the efficiency of enrichments, such as custom rule recognition.

    Cause: As part of their ingestion into Discovery, such files are converted from Office format to PDF format. When the conversion happens, textual content is sometimes lost due to the nature of a PDF file. While the new lines appear to be added at random, they typically get inserted in areas where text wraps in the original document, such as in narrow text boxes or to accommodate other inline elements, such as images or diagrams.

    Solution: To avoid new line insertions, increase the width of text boxes in the original document. If the original document has a section where text wraps to accommodate an inline element, such as an image, move the image so that it is situated in its own section and the nearby text doesn't need to wrap around it. To test whether your fixes address the issue, you can convert the original file to a PDF file to check for unexpected carriage returns in the text.

After applying a pretrained Smart Document Understanding model to a PPT file, table boundaries are not recognized properly
:    During the conversion process, text that is extracted from the table is confused with text that is outside the table in some PPT pages. This issue is more likely to occur in tables with a lot of text and that have footnotes displayed just outside the table border. If you encounter this issue, export the PPT file as a PDF file, and then upload the PDF file instead. Apply a user-trained Smart Document Understanding (SDU) model to the document, and then use the SDU tool to identify the tables in the document. The resulting model handles table boundaries properly and can extract text from the tables cleanly.

## PDF file troubleshooting tips
{: #upload-data-ts-pdf}

Failed to parse document due to invalid encoding
:    Enable OCR for the file.
