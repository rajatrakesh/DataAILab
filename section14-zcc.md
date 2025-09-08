# Zero Copy Lab

Pre-requisites:
Zero Copy Connectors setup (Estimated time 15 minutes)
Bring your own YP5+ DemoHub instances with Zero Copy Connectors narratives pre-installed.

FOLLOW INSTRUCTIONS ON THIS PAGE: https://demohub.service-now.com/kb_view.do?sys_kb_id=38f60ec92b43aa5099d1fe1fed91bf38 

>Note that installation of narrative(either Snowflake or Databricks) is mandatory as it installs the sn_data_fabric_zcc plugin

##Overview:

You will learn how to create a Data Fabric table and how to use it in a subflow that you will then pass to an agent.

### Part 1: Creating a data fabric table


Instruction	Image
Navigate to Workflow Data Fabric Hub. If you had followed the setup instructions, your screen should look like the image. Click "Edit"

**Do not click "Test Connection"**

![Zcc](screenshots/zcc-1.png)

	
Click "Save and connect", then click "Continue" on the pop-up box. It should take about 30 seconds to load.	
You will be directed to the "Data assets" tab. These contain all the tables in the corresponding "catalog" in Databricks.

Click the "wdf_demo_now" folder	

![Zcc](screenshots/zcc-2.png)


We will use a sample dataset for POS transactions.
Click "pos_transaction_logs"
Data fabric tables tab should be empty as we have not created any data fabric tables yet.
Click "Columns", this will show you all the columns in the "pos_transaction_logs" table
Click "Create data fabric table"	


![Zcc](screenshots/zcc-3.png)


On "New data fabric table", enter Label: "Retail POS Transactions"
Name will be automatically generated
Click "Continue"

>Note that scope applies here, so you can create data fabric tables in scopes like how you would any custom table	

![Zcc](screenshots/zcc-4.png)

Click the select all check box as we want all the columns
Toggle true on primary for "transaction_id" - This will be our record identifier
Click "Finish", the "Confirm"	

![Zcc](screenshots/zcc-5.png)

Congratulations! You've successfully created a Data fabric table using ZCC with Databricks.
Click on the more icon next to your new data fabric table, then click "Open list"	

![Zcc](screenshots/zcc-6.png)

You will be brought to the list view of all records on the data fabric table. You can interact with this table like how you would on any other table in ServiceNow.	

![Zcc](screenshots/zcc-7.png)

## Part 2: Creating a subflow


Navigate to Workflow Studio
Click New > Subflow	

![Zcc](screenshots/zcc-8.png)

We will create the subflow from scratch. Click "Build on your own" tab.
Name the subflow: Lookup POS Transactions
Change Run as: "System user"
Click "Build subflow on your own"	

![Zcc](screenshots/zcc-9.png)

We will assume that the AI agent will want to query the last 4 digits of the card number, as well as the amount of the transaction
Create 2 inputs
Card number - string
Amount - string	

![Zcc](screenshots/zcc-10.png)

Create 2 outputs
Label: Card vendor, type: string
Label: Status of transaction, type: string	

![Zcc](screenshots/zcc-11.png)

Add a new action > Look Up Record
We are only returning for one record for simplicity

![Zcc](screenshots/zcc-12.png)
	
Table: Retail POS Transactions
Conditions: 
Amount is drag amount from input
AND
Card number contains drag Card number from input	

![Zcc](screenshots/zcc-13.png)

Add "Flow Logic" action > "Assign subflow outputs"
Add a new row to assign to "Card vendor" output with the "Card vendor" data pill from the look up record action
Do the same for "Status of transaction"

![Zcc](screenshots/zcc-14.png)
![Zcc](screenshots/zcc-15.png)
	
Let's test our Subflow.
First "Save" the subflow, then click "Test"
Enter Card number 7894, and Amount is 92.83	

![Zcc](screenshots/zcc-16.png)

View test results	

![Zcc](screenshots/zcc-17.png)


Go back and publish the flow	

![Zcc](screenshots/zcc-18.png)

## Part 3: Use in Agent

Create a new AI Agent
Use Now Assist: This agent retrieves POS transaction data.
Save and continue	

![Zcc](screenshots/zcc-19.png)
![Zcc](screenshots/zcc-20.png)

Add a tool: Subflow
Follow the inputs in the screenshot
Click Add
Save and continue
Hint: Remember to publish your subflow from before, if not the execution won't work in the next step	

![Zcc](screenshots/zcc-21.png)
![Zcc](screenshots/zcc-22.png)
![Zcc](screenshots/zcc-23.png)

Skip the next 2 pages for now to get to the testing page.

Your newly created AI agent should be selected. Enter the following task:
"help me find the information for a transaction that is 102.13, for a card number ending 7894"
Test	

![Zcc](screenshots/zcc-24.png)

Was it successful? What message did you get?	

![Zcc](screenshots/zcc-25.png)

