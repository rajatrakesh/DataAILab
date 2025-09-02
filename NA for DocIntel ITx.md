# Now Assist for Document Intelligence
Now Assist for Doc Intel allows you review documents for key information and extract document data for use in your workflows.

# 📑 Use Case: Now Assist for Document Intelligence in ITSM

## 1. What We Are Building
We are building an **intelligent incident enrichment solution** within **ServiceNow ITSM** that leverages **Now Assist for Document Intelligence**.  
The solution demonstrates how AI can **read, understand, and extract structured information from unstructured attachments** (e.g., screenshots, PDFs, images) added to incidents using Now Assist for Document Intelligence.

The lab is designed to enable you with the following:
1. Creation of custom table (extension of task table)
2. Building Document Extraction use cases
3. Using the Document extraction use cases in the custom OOTB Document & Visual Insights AI Agents


## It makes following capabilities available to AI Agents:
- Document Extraction: Agents can extract information from documents and review the information, which then can be stored in mapped tables and fields in the workflow.
- Document Q&A: AI Agents can review documents and can help provide answers to pre-defined questions.
- Attachment Summarization: AI Agents utilized Now Assist for Doc Intel to get a summary of attachment content, along with the record summary for validation or comparison.
- Document Chat: AI Agents can now interact with the document in Now Assist for Virtual Agent and can get chat responses based on Document Content.

# Use Case: 
   - A user raises an incident (e.g., “Unable to connect to DB server”) as part of extended incident table.
   - The user attaches a screenshot of the error message (JPEG/PNG).  
The system automatically extracts key error fields and updates them into the **Incident record**, eliminating manual data entry.


## 2. How We Are Building
1. **Incident Extended Table Creation**  
   - Create a new table extended of incident task table with the relevant new columns (error code, application name and timestamp)

2. **Now Assist for Document Intelligence**  
   - NA for Doc Intel use case creation with individual fields.  
   - It identifies structured fields such as:  
     - **Application**: Microsoft SQL Server Management Studio  
     - **Server**: DB-PROD-02  
     - **Error Code**: 18456  
     - **Timestamp**: 2025-09-01 14:32:08  

3. **Incident Table Update**  
   - AI auto-populates these values into Incident fields or custom columns (e.g., `u_error_code`, `u_application_name` and `timestamp`).  


## 3. Why We Are Building
- **Current Problem**:  
  - Agents spend valuable time **reading unstructured documents/screenshots** and manually copying details into incident fields.  
  - This delays resolution and increases the risk of missing critical information.  

- **Value of Document Intelligence**:  
  - ✅ **Automated Extraction**: Transforms screenshots/logs into structured data.  
  - ✅ **Improved Agent Productivity**: Reduces manual data entry.  
  - ✅ **Faster Resolution**: Error codes and server names are instantly visible.  
  - ✅ **Better Reporting**: Structured error fields can be tracked in **Performance Analytics**.  
  - ✅ **Scalable AI Use Case**: Works for invoices, logs, access forms, and audit evidence.  


## What roles do I need to build Now Assist for Doc Intel Use cases?
- DocIntel Admin
- DocIntel Manager
- DocIntel Extraction Agent

## What plugins do I need to activate Now Assist for Doc Intel?
- Now Assist
- Document Intelligence
- Now Assist for Document Intelligence
- Now Assist Platform

## Building of Now Assist for Doc Intel Use Cases

![NA4DI](screenshots/NA4DIScreenshot.png)

Document Extraction use cases:
- Use cases where we must extract defined field of information from a document, the format of the document can be pdf, jpg, png.

Especially cases, where the attachment is part of a record (either custom attachment table or the sys_attachment table) and the extracted fields get updated as part of a target table.

## What roles do I need to build Now Assist for Doc Intel Use cases?
- DocIntel Admin
- DocIntel Manager
- DocIntel Extraction Agent

## What plugins do I need to activate Now Assist for Doc Intel?
- Now Assist
- Document Intelligence
- Now Assist for Document Intelligence
- Now Assist Platform

## Building of Now Assist for Doc Intel Use Cases
Document Extraction use cases:
- Use cases where we must extract defined field of information from a document, the format of the document can be pdf, jpg, png.
Especially cases, where the attachment is part of a record (either custom attachment table or the sys_attachment table) and the extracted fields get updated as part of a target table.

## Pre-requisites for Now Assist for Doc Intel
- Custom Table Creation (Extension of Incident task table)
- Incident creation
- Document Extraction Skill Activation

# Let's Get Started!

## 1) Create a custom table that extends Incident Task
Why: We want a place to capture extracted fields per artifact, without polluting the base Incident table.

In your demohub instance, go to All - Search `System Definition` > Table

![ITxNA4DI](screenshots/Table1.png)

Once you're in the Tables, click the `New` button from top right corner

![ITxNA4DI](screenshots/Table2.png)

Provide the `Label`, in this case we are calling it `Incident Error`, with this the `Name` value automatically gets created, `u_incident_error`
We are creating a extended table of Incident tasks, In the `Extends` Search for Incident Task and select from the drop down.
Since this is extended table of Incident task, we don't want to create a new module, however we want to make sure it is available in existing module, so we will go to `Add Module to menu` and search for `self-serve`

![ITxNA4DI](screenshots/Table3.png)
![ITxNA4DI](screenshots/Table4.png)
![ITxNA4DI](screenshots/Table5.png)
![ITxNA4DI](screenshots/Table6.png)
![ITxNA4DI](screenshots/Table7.png)
![ITxNA4DI](screenshots/TableCol1.png)
![ITxNA4DI](screenshots/TableCol2.png)
![ITxNA4DI](screenshots/TableIncident1.png)
![ITxNA4DI](screenshots/TableIncident2.png)
![ITxNA4DI](screenshots/TableIncident3.png)
![ITxNA4DI](screenshots/TableIncident4.png)
![ITxNA4DI](screenshots/TableIncident5.png)
![ITxNA4DI](screenshots/TableIncident6.png)
![ITxNA4DI](screenshots/NADI1.png)
![ITxNA4DI](screenshots/NADI2.png)
![ITxNA4DI](screenshots/NADI3.png)
![ITxNA4DI](screenshots/NADI4.png)
![ITxNA4DI](screenshots/NADI5.png)
![ITxNA4DI](screenshots/NADIUseCase1.png)
![ITxNA4DI](screenshots/NADIUseCase1.png)
![ITxNA4DI](screenshots/NADIUseCase1.png)
![ITxNA4DI](screenshots/NADIUseCase1.png)
![ITxNA4DI](screenshots/NADIUseCase1.png)
![ITxNA4DI](screenshots/NADIUseCase1.png)
![ITxNA4DI](screenshots/NADIUseCase1.png)
![ITxNA4DI](screenshots/NADIUseCase1.png)
![ITxNA4DI](screenshots/NADIUseCase1.png)
![ITxNA4DI](screenshots/NADIUseCase1.png)
![ITxNA4DI](screenshots/NADIUseCase1.png)
![ITxNA4DI](screenshots/NADIUseCaseAutofillComplete.png)
![ITxNA4DI](screenshots/NADIUseCaseComplete.png)
![ITxNA4DI](screenshots/NADIUseCaseFA.png)
![ITxNA4DI](screenshots/NADIUseCaseIntegrate1.png)
![ITxNA4DI](screenshots/NADIUseCaseIntegrate2.png)
![ITxNA4DI](screenshots/NADIUseCaseIntegrate3.png)
![ITxNA4DI](screenshots/NADIUseCaseIntegrate4.png)
![ITxNA4DI](screenshots/NADIUseCaseIntegrate5.png)
![ITxNA4DI](screenshots/NADIUseCaseIntegrate6.png)
![ITxNA4DI](screenshots/NADIUseCaseIntegrate7.png)
![ITxNA4DI](screenshots/NADIUseCaseIntegrate8.png)
![ITxNA4DI](screenshots/NADIUseCaseIntegrate9.png)
![ITxNA4DI](screenshots/NADIUseCaseIntegrate10.png)
![ITxNA4DI](screenshots/NADIUseCaseIntegrate11.png)
![ITxNA4DI](screenshots/NADIUseCaseIntegrate12.png)
