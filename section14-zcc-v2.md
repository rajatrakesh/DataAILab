# Section 15: Zero Copy Connectors from Scratch with Databricks

![databricks-setup1](screenshots/zcc-intro.png)  

By now we all know what Zero Copy Connectors are, so we will skip the introduction.

However, for refresher sharing the link to the WDF Second call deck which can help you if needed.

[WDF Second Call Deck](https://servicenow.seismic.com/Link/Content/DCDT2jDF9JVJc8CCFWPW7HQ7mcFG)

**What are we aiming to achieve at the end of this lab?**

- For customer PoVs, how easy it is to setup with databricks environment.
- Understand key details we would need request from customer for connection and authentication for databricks

## Let's get started with the lab!

Step 1: Create a databricks account

![databricks-setup1](screenshots/databricks-setup1.png)  

Since we are doing this for internally, let's select personal use

![databricks-setup2](screenshots/databricks-setup2.png)  

For Ease of logging, I am selecting `Continue with google`

![databricks-setup3](screenshots/databricks-setup3.png)  

Select `India` for location

![databricks-setup4](screenshots/databricks-setup4.png)  

The account is getting setup!

![databricks-setup5](screenshots/databricks-setup5.png)  

Perfect! we now are in the landing page of databricks

![databricks-data-import1](screenshots/databricks-data-import1.png)  

On the left pane, select `Data Ingestion` from `Data Engineering` section.

![databricks-data-import2](screenshots/databricks-data-import2.png)  

As part of today's exercise, we are only going to create the dataset in databricks by uploading the excel/csv.

You will be able to access the excel/csv from the [link](https://servicenow-my.sharepoint.com/:x:/p/rahul_adlakha1/EVnHG_4Sd15EkDLEbJwwzzcBQmqMnIMa6pRM0UHKJQ4s7g?e=fijwwn)

![databricks-data-import3](screenshots/databricks-data-import3.png) 

Upload the excel that you've downloaded from the above sharepoint link.

![databricks-data-import4](screenshots/databricks-data-import4.png)  

Click `Create Table` buttom at the bottom

Note: we are keeping the `catalog` and `schema` same.

![databricks-data-import6](screenshots/databricks-data-import6.png)  

Perfect! The table now is getting created!

![databricks-data-import7](screenshots/databricks-data-import7.png)  

Select `SQL Warehouses` from the left pane

This is a serverless sql warehouse, which is running already!

![databricks-data-permission1](screenshots/databricks-data-permission1.png)  

Open the  `SQL Warehouse`, i.e., Serverless starter warehouse

![databricks-data-permission3](screenshots/databricks-data-permission3.png)  

Click Connection details, this is where you will find the relevant connection details that we will leverage as part of servicenow WDF zero copy.

**Checkpoint on connection details, as we will be leveraging in SN instance**

![databricks-data-permission4](screenshots/databricks-data-permission4.png)  

With this, we now are moving on to the WDF capability in ServiceNow instance.

Navigate to Workflow Data Fabric Hub.

![wdf-zcc1](screenshots/wdf-zcc1.png)  

Under WDF Hub, let's begin connecting databricks!

![wdf-zcc2](screenshots/wdf-zcc2.png)  

Let's now leverage the databricks connection that we created in the databricks environment.

![wdf-zcc3](screenshots/wdf-zcc3.png) 

Starting with the `JDBC URL` from Databricks platform.

![databricks-data-permission5](screenshots/databricks-data-permission5.png)  

Update the JDBC URL in the `Connection URL` in the databricks connection setup in the instance.

![wdf-zcc4](screenshots/wdf-zcc4.png)  

We will be using the `HTTP URL` next

![databricks-data-permission6](screenshots/databricks-data-permission6.png)  

The HTTP URL will be going into the warehouse path

Along with this, let's also provide the connection details such as
1. `Connection label` : `PoV Readiness Workshop India`
2. `Short Description` : `Temp Connection setup for workshop`

![wdf-zcc5](screenshots/wdf-zcc5.png)  

Now the next two pending fields are Oauth fields.
For this we will establish a Service Principals

Go to `Settings`

![databricks-oauth1](screenshots/databricks-oauth1.png) 

Under `Identity and Access`, select `Service Principals` and click `Manage`

![databricks-oauth2](screenshots/databricks-oauth2.png)  

Click on `Add Service Principal`

![databricks-oauth3](screenshots/databricks-oauth3.png)

Give it a name, let's call it : `test_auth_service`

![databricks-oauth4](screenshots/databricks-oauth4.png)  

Open the service principal that we just created

![databricks-oauth5](screenshots/databricks-oauth5.png)  

Select the `Secret` tab 

![databricks-oauth6](screenshots/databricks-oauth6.png) 

Click `Generate Secret`

![databricks-oauth7](screenshots/databricks-oauth7.png) 

Provide the number of days till when we want these credentials to remain.

![databricks-oauth8](screenshots/databricks-oauth8.png)  

**Critical Note: Copy the Client ID and Secret, this will not be available later**

![databricks-oauth9](screenshots/databricks-oauth9.png)  

Next, we will add the Client ID and Secret, in the ServiceNow Databricks connection.

Perfect! we now have established the connection, let make one last change in Databricks before we go ahead and test this.

![wdf-zcc6](screenshots/wdf-zcc6.png)  

In the databricks table, let's grant access of the table to the workspace.

![databricks-workspace-permission1](screenshots/databricks-workspace-permission1.png)  

Now we test! Click Test Connection

![wdf-zcc7](screenshots/wdf-zcc7.png)  

We now have the dataset available as part of our WDF hub!

Next most important piece is creation of `Data Fabric Table`
Click `Create Data Fabric Table`

![wdf-zcc10](screenshots/wdf-zcc10.png)  

Let's add the label for the Data Fabric Table : `firewall_rules`

Note that scope applies here, so you can create data fabric tables in scopes like how you would any custom table

![wdf-zcc-datafabric1](screenshots/wdf-zcc-datafabric1.png)  

Let's add the mapping for the data fabric table to based on the columns available in the data fabric table
For now we are not selecting the primary key or changing the Data type but that is a viable option

![wdf-zcc-datafabric2](screenshots/wdf-zcc-datafabric2.png)  

Perfect! with this our data fabric table got created!
 
![wdf-zcc-datafabric4](screenshots/wdf-zcc-datafabric4.png)  

**Leveraging the data fabric table in AI Agents**

![workflow-studio1](screenshots/workflow-studio1.png)  
![workflow-studio2](screenshots/workflow-studio2.png)  
![workflow-studio3](screenshots/workflow-studio3.png)  
![workflow-studio4](screenshots/workflow-studio4.png)  
![workflow-studio5](screenshots/workflow-studio5.png)  
![workflow-studio6](screenshots/workflow-studio6.png)  
![workflow-studio7](screenshots/workflow-studio7.png)  
![workflow-studio8](screenshots/workflow-studio8.png)  
![workflow-studio9](screenshots/workflow-studio9.png)  
