---

copyright:
  years: 2020, 2022
lastupdated: "2022-12-15"

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting ingestion
{: #troubleshoot-ingestion}

Learn about solutions and workarounds to warnings or errors that you might encounter when you add data to a collection.
{: shortdesc}

This information applies both to managed and installed instances of {{site.data.keyword.discoveryshort}}. For more troubleshooting tips for installed deployments only, see [Troubleshooting {{site.data.keyword.discoveryfull}} Cartridge for {{site.data.keyword.icp4dfull}} deployments](/docs/discovery-data?topic=discovery-data-troubleshoot).
{: note}

Unable to process one or more documents
:    This notification is displayed in the page header when a processing delay of any kind occurs in any project across the entire service instance. If the message is displayed while you are adding data to a collection, you can ignore it. If any problems occur that are related to the creation of your collection, a message is displayed in the *Activity* page for the collection. Check there for any pertinent messages.

## Microsoft document troubleshooting tips
{: #upload-data-ts-ms}

Failed to prepare document for SDU processing
:    Some DOC, PPT, and XLS files that use older features which are no longer supported by Microsoft Office can cause ingestion issues. If you encounter this issue, open the file in a more recent version of Microsoft Office and convert the file to the DOCX, PPTX, or XLSX format respectively, and then upload the DOCX, PPTX, or XLSX file.

Line breaks are inserted randomly
:   When some files in Microsoft Office format are added to a collection, line breaks are inserted seemingly at random to the text that is stored in the `html` field in the collection's index. The unexpected line breaks can impact the efficiency of enrichments, such as custom rule recognition.

    Cause: As part of their ingestion into Discovery, such files are converted from Office format to PDF format. When the conversion happens, textual content is sometimes lost due to the nature of a PDF file. While the new lines appear to be added at random, they typically get inserted in areas where text wraps in the original document, such as in narrow text boxes or to accommodate other inline elements, such as images or diagrams.

    Solution: To avoid new line insertions, increase the width of text boxes in the original document. If the original document has a section where text wraps to accommodate an inline element, such as an image, move the image so that it is situated in its own section and the nearby text doesn't need to wrap around it. To test whether your fixes address the issue, you can convert the original file to a PDF file to check for unexpected carriage returns in the text.

After applying a pretrained Smart Document Understanding model to a PPT file, table boundaries are not recognized properly
:    During the conversion process, text that is extracted from the table is confused with text that is outside the table in some PPT pages. This issue is more likely to occur in tables with a lot of text and that have footnotes displayed just outside the table border. If you encounter this issue, export the PPT file as a PDF file, and then upload the PDF file instead. Apply a user-trained Smart Document Understanding (SDU) model to the document, and then use the SDU tool to identify the tables in the document. The resulting model handles table boundaries properly and can extract text from the tables cleanly.

Document cannot be converted to PDF format
:    If you are using an installed deployment in a FIPS-enabled cluster, you might see a message when you ingest Microsoft Word documents that says, `Document cannot be processed because it cannot be converted to PDF format. Convert the document to PDF format before you add it to the collection`. You can ignore this message. It is displayed prematurely. Give the service more time and the document will be ingested successfully.

## PDF file troubleshooting tips
{: #upload-data-ts-pdf}

Failed to parse document due to invalid encoding
:    Enable OCR for the file.

## Enrichment troubleshooting tips
{: #upload-data-ts-enrichments}

Table Understanding: *n* input tables excluded by enrichment
:    If tables in a document have inconsistent column and row spans or are too large for the system to process completely, the table understanding enrichment is not applied to them. Information from such tables cannot be returned in search results. If you want the table understanding enrichment to be applied to a table that was skipped, consider editing the table. Change a table with inconsistent column and row spans to have a simpler table format. Split a large table into many smaller tables.

    To find the table where the enrichment was not applied, check the warning message. It lists the character offsets where the table begins and ends in the HTML representation of the document. To see the full warning message and get the document ID, click **View all**, and then make a note of the document ID. From the *Improve and customize* page, submit an empty search query to return all of the indexed documents. Look for the document ID. (You can change the search result settings to show the document ID as the result title.) Click the **View passage in document** link for your document, and then click **Open advanced view**. Choose to view the document as JSON and then look for the `html` field. Copy and paste the HTML representation of the document into a text editor. Look for the character offsets that were listed in the original warning message to find the table.
