# Now Assist for Document Intelligence
Now Assist for Doc Intel allows you review documents for key information and extract document data for use in your workflows.

## 📑 Use Case: Now Assist for Document Intelligence in ITSM

## 1. What We Are Building
We are building an **intelligent incident enrichment solution** within **ServiceNow ITSM** that leverages **Now Assist for Document Intelligence**.  
The solution demonstrates how AI can **read, understand, and extract structured information from unstructured attachments** (e.g., screenshots, PDFs, images) added to incidents using Now Assist for Document Intelligence.

The lab is designed to enable you with the following:
1. Creation of custom table (extension of incidnet task table)
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


## Pre-requisites for Now Assist for Doc Intel
- Custom Table Creation (Extension of Incident task table)
- Incident creation
- Document Extraction Skill Activation

# Let's Get Started!

## Part 1 - Create a custom table that extends Incident Task
Purpose/Why: We want a place to capture extracted fields per artifact, without polluting the base Incident table.

In your demohub instance, go to All - Search `System Definition` > Table

![ITxNA4DI](screenshots/Table1.png)

Once you're in the Tables, click the `New` button from top right corner

![ITxNA4DI](screenshots/Table2.png)

Provide the `Label`, in this case we are calling it `Incident Error`, with this the `Name` value automatically gets created, `u_incident_error`
We are creating a extended table of Incident tasks, In the `Extends` Search for Incident Task and select from the drop down.
Since this is extended table of `Incident task`, we don't want to create a new module, however we want to make sure it is available in existing module, so we will go to `Add Module to menu` and search for `self-serve`
Next we go to `Controls` Tab

![ITxNA4DI](screenshots/Table3.png)

On the same table creation page, In the `Controls` tab, we check `Auto-Number`
Next, we will provide `Prefix`, which in this case will be `INCE`
`Number` will be `1000`
'Number of Digits` we will keep as `6`

Note, this is customizable, you have your own structure of `Auto-Number`

Next, we will move on to `Application Access` for manage access controls

![ITxNA4DI](screenshots/Table4.png)

As part of `Application Access` tab, we will check the following
`Can Create`
`Can Read`
`Can Update`

Click `Submit`

✅ With this, we have completed creation of custom extended table for incident task!

![ITxNA4DI](screenshots/Table5.png)

![ITxNA4DI](screenshots/Table6.png)

Now we have the custom table available as part of the `Tables`
We will search for the table and configure the columns required for the use case.

![ITxNA4DI](screenshots/Table7.png)

In the table, go to the `Columns` Tab, Insert new columns, by clicking the `Insert new row` at the bottom
Where we provide the `Label`, `Name` and `Type` of the column.

✅ Great! we now have completed the column creation as part of the custom table.

![ITxNA4DI](screenshots/TableCol1.png)

Next, we go to the `Incident Error` table, Click `New` on the top right corner.

![ITxNA4DI](screenshots/TableCol2.png)

In a the same window, we will have a `New Record` creation for `Incident Error`
As part of the `New Record`, you will be able to see the `Number` being Auto-generated, this is based on the configuration we created as part of the table creation.

![ITxNA4DI](screenshots/TableIncident1.png)

Next Click on the `Attachment` icon on top right corner.

![ITxNA4DI](screenshots/TableIncident2.png)

You will see `Attachments` window come up, Click Choose file.

![ITxNA4DI](screenshots/TableIncident3.png)

Select the `error` screenshot present as part of the exercise.

![ITxNA4DI](screenshots/error.png)

![ITxNA4DI](screenshots/TableIncident4.png)

With this the error screenshot is now part of the new `Incident Error` record.
Provide a `Short Description`, and Click `Submit`

![ITxNA4DI](screenshots/TableIncident5.png)

✅ Well Done! We now have completed the pre-requisite for the Now Assist for Document Intelligence

![ITxNA4DI](screenshots/TableIncident6.png)

## Part 2 – Activating and Configuring the Document Extraction Use Case
Why/Purpose: To automate the capture of critical information from error images, we will configure Document Intelligence to identify and extract key fields. The extracted values will then be automatically mapped and populated into the custom table columns, reducing manual data entry and ensuring accuracy in incident task management.

To begin, we go to the Admin > Now Assist Admin

![ITxNA4DI](screenshots/NADI1.png)

As part of Now Assist Admin, we go to `Now Assist Skills`

![ITxNA4DI](screenshots/NADI2.png)

In Now Assist Skill, from the left pane, select `Platform`

![ITxNA4DI](screenshots/NADI3.png)

As part of Now Assist Skill for Platform, in the top right, Search for `Document`
You will find two skills:
1. Document Extraction
2. Document Q&A

As part of today's exercise, we will `Activate` Document Extraction Skill.

![ITxNA4DI](screenshots/NADI4.png)

Once you `Activate` Document Extraction Skill, we will create use case by clicking `New use case`

![ITxNA4DI](screenshots/NADI5.png)

## Step 1: Define Use Case

To create a new use case, we start by defining the use case
Provide the following details:
1. Use Case Name
2. Target Table

![ITxNA4DI](screenshots/NADIUseCase1.png)

As part of today's workshop, let's provide the follow details to the fields

1. Use Case Name: `Incident Code`
2. Target Table: `Incident Error` - This you will select from the drop down list.

![ITxNA4DI](screenshots/NADIUseCase2.png)

## Step 2: Define Fields

Next, we will define the fields for the `Incident Code` use case

Name: `give name of the field`
Details: Details field is critical as it used to help the LLM, find the correct data from the document, write the information about the field that we are extracting such that it helps explain the field information. Also provide an example if possible.
Field: `Text` (Default)
Target Field: `search the target field based from the columns of the target table` (If we search, we will see the options)

Most critical information, that you need focus on is the `Details` part. This field is essential to find the field from the document.

*Field 1*

Field name: `application name`
Details: `This is the impacted application name, for which we are getting the error`
Target field: `u_application_name`
Field Type: `Text`
Check `Single field is required for extraction`

![ITxNA4DI](screenshots/NADIUseCase3.png)

*Field 2*

Field name: `error code`
Details: `this is a numeric code for the error given by the application`
Target field: `u_error_code`
Field Type: `Text`
Check `Single field is required for extraction`

![ITxNA4DI](screenshots/NADIUseCase4.png)

*Field 3*

Field name: `timestamp`
Details: `This is the timestamp of error occurance`
Target field: `u_error_code`
Field Type: `Text`
Check `Single field is required for extraction`

![ITxNA4DI](screenshots/NADIUseCase5.png)

With this we now have created all three fields for the use case

![ITxNA4DI](screenshots/NADIUseCase6.png)

## Step 3: Test Output

Click, `Test a new document` button

To test the fields extraction, we will use the `Incident error` table record that we created
For the testing, Let's select `Upload from record` and search the number `INCE001002`

Next, let's link the record.

![ITxNA4DI](screenshots/NADIUseCase7.png)

Once, the record gets linked, the use case starts looking for the attachment in the record.
It prepares the document and refect the same on the screen.
### Note: Sometimes it may take longer to process the document, to valide click `refresh`button on the right pane.

![ITxNA4DI](screenshots/NADIUseCase8.png)

Once the document is processed, you will see the extracted fields from the document.
In this case, it will be application name, error code, and timestamp.
Before we submit the test results, we need to review the extracted values.
Go to More > Click `To review`
Individually click on each field value, this will complete the review of each field extracted value and there will be no more fields in the `To review` section.

![ITxNA4DI](screenshots/NADIUseCase9.png)

![ITxNA4DI](screenshots/NADIUseCase10.png)

Once completed, in the top right corner, select `submit`.
In the pop-up, select `Confirm and Submit`

![ITxNA4DI](screenshots/NADIUseCase11.png)

## Step 4: Add Integrations

Next we move on to creation of integration with the custom table
In this step, we will integrate what we have done so far to extract the values then process them and eventually update the custom table record with the individual field values.

Click the `Add Integration` button.

Provide the following details:
1. Integration Name : `IncidentErrorExtract`
2. What type of Integration you want to set? : `Extract Values` (Select from drop down)

Click `Save`

![ITxNA4DI](screenshots/NADIUseCaseIntegrate1.png)

Now Let's add the second integration to process the values extracted.

Click the `Add Integration` button.

Provide the following details:
1. Integration Name : `IncidentErrorProcess`
2. What type of Integration you want to set? : `Process task` (Select from drop down)

![ITxNA4DI](screenshots/NADIUseCaseIntegrate2.png)

As part of process task, we need to provide the condition as well.

From the first drop down, select `Number`

![ITxNA4DI](screenshots/NADIUseCaseIntegrate3.png)

From the second drop down, select `is not empty`

### Essential Qn: Why are we doing this?
- We are doing this to make sure that the incident record is properly defined to make sure that it exists before it go ahead and update the columns.

![ITxNA4DI](screenshots/NADIUseCaseIntegrate4.png)

With this we now have both the integrations available in the use case.

![ITxNA4DI](screenshots/NADIUseCaseIntegrate5.png)

These integrations are nothing but flows that we have created automatically without going to `Flow Designer`
### One critical thing to Note: We need to activate these integrations in the flow designer.

Open `IncidentErrorExtract` integration, click `Open in Flow Designer` button.

![ITxNA4DI](screenshots/NADIUseCaseIntegrate7.png)

In the flow designer, activate the flow by clicking `Activate` top right corner.

![ITxNA4DI](screenshots/NADIUseCaseIntegrate8.png)

Confirm Activate

![ITxNA4DI](screenshots/NADIUseCaseIntegrate9.png)

Similarly, for the process integration, Open `IncidentErrorProcess` integration, click `Open in Flow Designer` button.

![ITxNA4DI](screenshots/NADIUseCaseIntegrate10.png)

In the flow designer, activate the flow by clicking `Activate` top right corner.

![ITxNA4DI](screenshots/NADIUseCaseIntegrate11.png)

Confirm Activate

![ITxNA4DI](screenshots/NADIUseCaseIntegrate12.png)

Go back to the Integration tab, click the gear icon for Settings

![ITxNA4DI](screenshots/NADIUseCaseIntegrate5.png)

We now need to activate the full extraction mode, by enabling the toggle. Check out the screenshot below!

### Purpose/Why? : Full Automation mode, helps the AI Agent to extracts the fields and process without actually reviewing the field information, like we did in Step 3

![ITxNA4DI](screenshots/NADIUseCaseFA.png)

## Last step: Review and Activate

![ITxNA4DI](screenshots/NADIUseCaseComplete.png)

✅ Well Done! We have completed the use case creation.

Now let's re-run the test output step, to validate if the extraction and process for auto-fill in the incident works

Once you're done, you will see the the incident record with the below values!

![ITxNA4DI](screenshots/NADIUseCaseAutofillComplete.png)


**Next Section:** [Section 12 - Reading Data from Custom Table](section12-reading-custom-table-data.md)
**Previous Section:** [Section 10 - Create Custom Table](section10-create-custom-table.md)
**Back to:** [Main README](README.md)
