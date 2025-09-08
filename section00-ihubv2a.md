# Section 0: Integration Hub – Device Issues API (Two Approaches)

**Estimated time: 35 minutes**

## Overview

In this section, you will integrate with a fictional REST API that provides device issues (computers, printers, routers).  

You will explore **two different approaches (forks):**

- **Fork 1 – Persisted Data:** Create a custom table, ingest API data on a schedule using **IntegrationHub**, and then expose it to an **AI Agent**. This simulates a real ITSM scenario with reporting and history.  
- **Fork 2 – Live Query:** Call the API directly at runtime without storing results. This is faster to set up and useful when data doesn’t need to be persisted.  

You can choose one fork to complete, or complete both to understand the trade-offs.

---

## Prerequisites

Before starting this section, please ensure you have:

- Access to an instance with **IntegrationHub** and **Flow Designer** enabled  
- Permissions to create custom tables and flows  
- An AI Agent workspace available  
- The mock API endpoint URL (provided by your instructor, e.g., `https://itsm-mock-api.servicenow.workers.dev`)

---

## Review the API

The mock service is hosted online and returns JSON data about device issues.

**Endpoints**

- `/issues` – returns latest issue per device (summary mode)  
- `/issues?device=PRN-7F3&limit=5` – returns the last 5 issues for a device (history mode)  
- `/devices` – returns list of available device IDs  
- `/health` – returns service status  

**Example call**  
`https://itsm-mock-api.servicenow.workers.dev/issues?device=PRN-7F3&limit=3`

![Ihub API Example](screenshots/ihub2-api.png)

---

## Build the Flow in Flow Designer

<!-- 1. Go to **Workflow Studio > New Flow**.  
//   - Name: `Fetch Device Issues`  
 //  ![Ihub New Flow](screenshots/ihub2-flow-new.png)
   
2. **Trigger**:  
   - Type: Scheduled  
   - Frequency: every 10 minutes  
   ![Ihub Trigger](screenshots/ihub2-trigger.png) 
   
3. **Step 1: HTTP Request**  
   - Method: GET  
   - URL: `https://<your-worker>.workers.dev/issues?limit=10`  
   - Headers: `Accept: application/json`  
   ![Ihub HTTP Step](screenshots/ihub-http.png) -->
   
1. Go to **Workflow Studio**

2. Click **New** > **Spoke**
   
	![iHub New Spoke](screenshots/ihub2-new-spoke.png)

3. Give is a **Name** : `ITSM Rest API Spoke` and **Description**: `Spoke for REST API Call` and click **Continue**.

	![iHub Spoke Description](screenshots/ihub2-spoke-desc.png)

4. Click **Create action** drop down and select **Action Designer**

	![iHub Spoke Create Action](screenshots/ihub2-spoke-create-action.png)

5. Let's name the Action Designer: `ITSM REST API Action`. Ensure that the **Application** is selected as the Spoke we created. 

	![iHub Spoke Action Description](screenshots/ihub2-spoke-action-desc.png)

6. Click **Create Input** on the right, and create two input variable. Name them `device` and `limit`. These are the parameters that we would be sending to our REST API Call. 

	![iHub Spoke Inputs](screenshots/ihub2-spoke-inputs.png)

7. Click the '+' symbol below the Inputs in the left pane, to **Add a New Step**. This is where we would put in our REST API Call. 

	![iHub Add Rest API](screenshots/ihub2-add-rest-api.png)
	
8. In the pop window, Type **REST** and choose **Perform a REST web service request**.

	![iHub - Select REST](screenshots/ihub2-select-rest.png)

9. In the next screen, make the following selections:
	- **Connection**: `Define Connection Inline`
	- **Base URL**: `https://itsm-mock-api.servicenow.workers.dev/`
	- **Build Request**: `Manually`
	- **Resource Path**: `issues?`
	- **HTTP Method**: `GET`
	- Click '+' and add 2 query parameters:
		- **Name**: `device` and `limit`
		- Drag the **Input varibles** from the right. These are the ones we had created in the previous step. 
		- `device` will have `action>device`
		- `limit` will have `action>limit`

	![iHub - Config REST](screenshots/ihub2-config-rest.png)
	
10. Click **Save**. Click **Test** to test our API. 
	- In the test window, type `PRN-7F3` as **device**
	- **Limit** it to `4`
   - Click **Run Test**
   
	![iHub - Test REST API](screenshots/ihub2-test-rest-api.png)
	
11. If the test is successful, you will see the **Response Body** has been populatd. 

	![iHub - Test REST Result](screenshots/ihub2-test-rest-result.png)

12. Clicking on the **Response Body** shows additional details about the messages returned (raw)

	![iHub - Test Result Raw](screenshots/ihub2-test-rest-result-raw.png)

13. The next thing we need to do is to add a **JSON Parser** as a step after the REST Step. This is to be able to read the individual values from the response body that has been returned. 
	- Click '+' symbol below the REST Step
	- Add `JSON Parser` from the list

	![iHub - Choose JSON Parser](screenshots/ihub2-choose-json-parser.png)

14. Once **JSON Parser** Step has been added, drag `Response Body` from `REST Step` on the right panel, to the field **Source Data**. You would also need to **manually** copy the **Response Body** from the prior test into the block below, before you are able to **Generate Target**. 

>If you no longer have that, you can run that same base url earlier in a browser window to get the json text. 

	![iHub - JSON Response Body](screenshots/ihub2-json-response-body.png)
	
15. Click **Generate Target**. This will extract the file information from the response body, and this will be displayed in the **Target** Panel

	![iHub - JSON Generate](screenshots/ihub2-json-generate.png)
	
16. Now we need add output variable to our **Action Outline**. Click the **Outputs**

	![iHub - Edit Output](screenshots/ihub2-edit-output.png)

17. Click **Edit Output**. Change/Add the label as follows:
	- Change the **Label** to `device issues`
	- Change the **Type** to `Array.Object`

	![iHub - Change Label](screenshots/ihub2-edit-output-label.png)

18. Expand the **JSON Parser Step** to review the `root` Object.

	![iHub - JSON Parser Step](screenshots/ihub2-json-parser-step.png)

19. Click **Exit Edit Mode**. Drag the `issues` from the **JSON Parser Step**, into the `device issues` variable. 

	![iHub - Action Output](screenshots/ihub2-action-output.png)

20. **Save** the Action. Now let's test the entire flow by clicking **Test**
	
21. While testing the full action, let's provide the following values:
	- **Device**: `PRN-7F3`
	- **limit**: `3`
	
	![iHub - Test Action](screenshots/ihub2-test-action.png)
	
22. After the action has been successfully run, it show show the following:

	![iHub - Test Action Success](screenshots/ihub2-test-action-success.png)

23. If everything has run successfully, the **device issues** should be populated correctly. 	
	
	![iHub - Test Action Log](screenshots/ihub2-test-action-log.png)
	
23. Click the values displayed in **device issues**, to view the values populated in the `Array Object`

	![iHub - Array Result](screenshots/ihub2-array-result.png)
	
24. Everything looks good. Let's **Publish** the action. 

	![iHub - Publish](screenshots/ihub2-publish.png)
	
Since we have completed the creation of the spoke. Now we can test it with 2 options. 

-------

## Step: Let's persist this data into a Custom Table

Navigate to **System Definition > Tables** and create a new table:

![Ihub Create Table](screenshots/ihub2-createtable.png)

**Table Name:** `u_ext_device_issue`

**Fields to add:**

- `u_ext_id` (String, 64, unique)  
- `u_device_id` (String, 64)  
- `u_ci_class` (String, 40)  
- `u_device_name` (String, 255)  
- `u_location` (String, 100)  
- `u_owner` (String, 100)  
- `u_status` (Choice: open, acknowledged, resolved)  
- `u_severity` (Choice: low, medium, high, critical)  
- `u_issue_code` (String, 50)  
- `u_short_description` (String, 255)  
- `u_detected_at` (Date/Time)  
- `u_suggested_kb` (URL)  
- `u_vendor_ticket` (String, 100)  
- `u_sla_remaining_min` (Integer)

![Ihub Create Table](screenshots/ihub2-table.png)

Now let's create a flow to persist this data into the table that we created in the above step. 

**Open Workflow Studio** and create a new **Flow**. 

Give it a name `Save API Data to Table`.

First thing that we need to do is add a trigger. We will add the trigger to run just once. 

![Ihub Flow Trigger](screenshots/ihub2-flow-trigger.png)

> This step isn't applicable, but to create a flow, a trigger is required. 

In the next step, we would connect to the REST Service and get the data. Click **Action** to then add the **Action** that we had created earlier. 

![Ihub Flow Create](screenshots/ihub2-flow-create-action.png)

Let's provide a set of test values, to test the action, as follows:
	- **device**: `PRN-7F3`
	- **limit**: `3`

![Ihub Input Rest values](screenshots/ihub2-flow-rest-values.png)

Next step, let's add a **For each loop** to iterate through the values, that we would save to the table created previously. 

Add a **Flow Logic** and choose the **For Each**. 

![Ihub For Each](screenshots/ihub2-flow-for-each.png)

Drag the `Device Issues` array object into the Flow loop. 

![Ihub For Each](screenshots/ihub2-flow-for-each-values.png)

Once the for each loop is created, now we need to need an **Action** to **Create Record** into the table. 

Then choose all columns from the table `u_ext_device_issues` that you need to save values into. In the data fields, drag the respective fields from the right panel, under `Object` - > `issues_object`. 

![Ihub - Create Record](screenshots/ihub2-create-record.png)

The above step will insert all values into the table. As a last *Optional* step, we will add a **Lookup Records** action to validate that the records have been committed to the table. 

Add the **Lookup Records** action, and add the table `u_ext_device_issues` and select a criteria `ext_id` as `is not empty`

![Ihub - Lookup Records](screenshots/ihub2-lookup-records.png)

Finally, let's **Test** the complete flow. The results should look something like this: 

![Ihub - Test Flow](screenshots/ihub2-test-flow.png)

Click the successful test to check individual values. 

![Ihub - Test Flow](screenshots/ihub2-test-flow-1.png)

![Ihub - Test Flow](screenshots/ihub2-test-flow-2.png)

![Ihub - Test Flow](screenshots/ihub2-test-flow-3.png)

>The count would be displayed as `3` in the test if you have run this flow the first time. With every subsequent flow, this value will increment with 3 (using the same input parameters)

--------

## Step: Let's build an AI Agent to call this API 

In addition to persisting these values into the table, the **Action** that we created earlier, could also be leveraged in an AI Agent. 

Create an AI Agent and setup the following values: 

**Name**: `ITSM Device Issues Agent`
**Description**: `This AI Agent is designed to assist users to find past and current issues with devices. It can query and find out what recent issues have been reported for a specific device or type of devices. The purpose of this agent is to then provide a summary of all issues.`
**AI Agent Role**:`This agent queries recent incidents or issues that have been reported for a particular device, or type of devices. It will provide various information to the user, based on the input from the user on the type of device.`
**Instructions**:`1. Ask user for which device they would like to monitor. If no device name is given, it means the response will be broader across different devices. 
2. If a limit has been provided, then it will limit the output to that number. 
3. An array will be returned, that may have 1 or multiple issues. 
3. Organises the output and presents it to the user in a human readable format.`

![Ihub - AI Agent](screenshots/ihub2-ai-agent-1.png)

Next, let's add a **Flow Action** tool, to the AI Agent:

**Name**:`Query Recent Issues Encountered`
**Description**: `Retrieve recent issues that have been reported for a particular device`
**Select flow action**:`Get ITSM Device Info from API`

![Ihub - AI Agent](screenshots/ihub2-ai-agent-2.png)

Let's execute this agent with the prompt `Find the past 3 issues encountered by device PRN-7F3`

![Ihub - AI Agent](screenshots/ihub2-ai-agent-execution.png)

------

This completes the lab for **Integration Hub**. 

**Next Step:** [Section 1 - Start using Gen AI on Day 1](section1-start-using-genai.md)
