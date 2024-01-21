# Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project

## Part 1- End to End Azure Data Engineering Project | Project Overview

<img width="550" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/295eedb1-730e-4d81-9db8-a420bf486d70">

This project is an end to end data platform right from Data Ingestion, Data Transformation, Data Loading and Reporting. 

The tools that are covered in this project are,

1. Azure Data Factory
2. Azure Data Lake Storage Gen2
3. Azure Databricks
4. Azure Synapse Analytics
5. Azure Key vault
6. Azure Active Directory (AAD) and
7. Microsoft Power BI

The use case for this project is building an end to end solution by ingesting the tables from on-premise SQL Server database using Azure Data Factory and then store the data in Azure Data Lake. Then Azure databricks is used to transform the RAW data to the most cleanest form of data and then we are using Azure Synapse Analytics to load the clean data and finally using Microsoft Power BI to integrate with Azure synapse analytics to build an interactive dashboard. Also, we are using Azure Active Directory (AAD) and Azure Key Vault for the monitoring and governance purpose. 

## Part 2- Environment Setup | End to End Azure Data Engineering Project

<img width="545" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/ccba59ef-d071-488b-a039-d4559dcf8b2e">

### create a resource group - (rg-data-engineering-project) and inside it create:

1. Azure Data Factory
2. Azure Databricks
3. Storage Account
4. Azure Synapse Analytics
5. Key Vault

<img width="436" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/05f0274f-da6a-4123-9bbb-cc0edf727594">

### open ssms and restore database AdventureWorks (version according to your SSMS version) and create user login and password

``ruby
create login syakeer with password = '!@#Password!'
create user syakeer for login syakeer
`` 

### open key vault resources and generate 2 secret key where 1 for username = syakeer and 1 for password = !@#Password!'

<img width="567" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/de14baf3-b747-4c9e-89b8-ed47a43f6f06">

## Part 3- Data Ingestion (1) | End to End Azure Data Engineering Project
 
<img width="379" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/3e75db6a-33cd-4d4f-9189-25dd0902c6ba">

Now we gonna work with the first step which is to configure our connection from ADF to our on-premise SQL Server

### open azure data factory and inside manage create a new integration runtime to connect to our on premise server

1. for integration runtime setup can put name as 'SHIR' as Self Hosted Integration Runtime and description as used to connect to SQL Server
2. choose Option 1: Express setup
3. After finish install, open Microsoft Integration Runtime Integration Manager to see if it active and this will allow us to connect from ADF to on-premise SQL Server

<img width="578" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/c27a0b24-c055-4074-ba33-859bb1d4fc3a">

### on azure data factory, inside author create a new pipeline and use copy data for activites and in the source dataset, choose sql server

<img width="548" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/029582fb-8012-4ece-b66f-04bff94316ec">

1. set the Linked Services as below
<img width="194" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/f6870999-801c-465f-b01e-fb9ed4f743e3">

2. use Azure key Vault instead of password, so click new+ as below
<img width="202" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/4fb7c60e-d764-4326-bbe8-69856655f2d7">

3. the loading will fail because of permission, so go back to Key Vault resources
<img width="209" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/235dc1fe-12d7-4e27-8afc-ff235b4b42a1">

4. in the Key Vault, on Access Policies create new user
<img width="314" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/22d3fcde-cc5f-46ba-9bb7-ba16cd52a173">
<img width="206" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/672caed3-300d-49c0-8de2-b7a96492c542">
<img width="290" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/cebae3b3-5e69-460d-8f9a-7f63e227c15f">
and finally just create

5. now go back to ADF, click refresh on the secret name and click password
<img width="211" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/6485d42c-313c-49ed-b274-ae5956f9bd26">
if connection successfull, click create

6. on the tabe name, choose address as we will extract that table to our datawarehouse
<img width="221" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/32e651ee-23c4-4172-b776-d964224dd4c8">

7. so for now the source options will be settle for now
<img width="247" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/2c6287dd-e6f8-4cbc-9478-066b5a03f05d">

### Since the source part is settle, we are going to move to the 2nd part which is the sink part

<img width="374" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/30128a22-ad9c-4e47-b11e-c22dc6615fd3">

1. click on the sink part and click new, choose azure data lake gen 2 storage and parquet format and name it as address_parquet and the linked services as below
<img width="188" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/24448aa7-e118-42fd-ade5-eb71cd5a7288">

2. open storage account and create bronze container
<img width="193" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/72c50eae-d58c-4aaa-8f09-ce54adacb9b3">

3. now on adf, use the bronze folder
<img width="239" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/a80f3ebb-9369-40a2-9ece-85d8daeb4adb">

4. click the Debug to run the pipeline and after successful, the address table now will be availabe inside our storage account in bronze container
<img width="356" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/6cd35013-3ea7-4a34-8110-7c3494a2ddfa">

5. However, we do not want to do this mutiple time to bring every table from SQL Server to our datawarehouse, so in the next step we are going to bring all the available table inside our dw in 1 single pipeline. So go back to storage account and delete the address_parquet file


## Part 4- Data Ingestion (2) | End to End Azure Data Engineering Project

so now we are going to copy all the tables from SQL Server to our datawarehouse using Azure Data Factory pipeline

1. inside ADF, in Author create a new pipeline and rename it to copy_all_table, for activities use lookup
<img width="479" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/7cc16659-874c-43aa-bb29-511a16b16ef8">

2. for settings > source dataset > create new+ > and set properties as below:
<img width="229" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/0668d2d8-426f-47b4-ae98-bbbc6803e061">
and instead of table, use query and paste the query inside the box and run the pipeline (debug):
``ruby
select
s.name as SchemaName
t.name as TableName
FROM sys.tables t
INNER JOIN sys.schemas s
ON t.schema_id = t.schema_id
WHERE s.name = 'SalesLT'
``

3. add a new activity ForEach, rename it to ForEach Schema Table, on the settings > item > add dynamic content

<img width="346" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/f5f187f7-d29f-4cb7-b3a8-17920cf52efb">

``ruby
@activity('look for all table').output.value
``
and on the activiy setting (highlighted in yellow) and click on the pencil icon so that we will go inside the ForEach activities 


4. inside the ForEach, drag copy activity and set source dataset and also the query as below so that we will grab all the table name from the schema

<img width="332" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/e65799d8-0886-4c8e-adbe-3175d299ab54">

``ruby
@{concat(select * from ', item.SchemaName,'.', item.TableName)}
``

5. for sink, set it as below
<img width="248" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/c95107eb-62ea-4f54-ae16-5dfad8422e15">

beside the sink dataset, click on pencil icon and create parameter > new+ and add schemaname & tablename

<img width="372" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/120b4a10-1c92-4cd5-8c08-c6e702f41d27">

after that go to the sink and set it as below 
<img width="458" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/d7034761-88d4-4547-9d19-253467a4ab3e">

in the sink, click again the pencil icon and on the connecton part, put the query as below
<img width="471" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/1e94c7c4-bc7b-4050-b744-e2649949c1c7">
``ruby
@{concat(dataset().schemaname, '/',dataset().tablename)}
@{concat(dataset().tablename,'.parquet')}
``

6. click debug and wait for the pipeline to complete the job, now go to monitor tab to see whether all the job succeed or not

<img width="547" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/da930e85-97c6-4e08-97b3-e61b4838c080">

7. go to storage account and open the bronze container to see all the table that have been brought to the datawarehouse
<img width="547" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/ac844796-78c7-4a59-96d0-1d3578cd4716">


## Part 5 - Data Transformation (1) | End to End Azure Data Engineering Project |Mounting the Datalake

1. Launch databrick workspace > click on compute tab and create new compute

<img width="407" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/488ecbb0-fd11-4d64-8f7d-ab783bec1361">
<img width="232" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/41ff3683-0bb6-4b6c-963f-4509c3d09c68">

2. create a new workbook

<img width="357" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/9de178a8-7a8e-476c-8acf-6cfc2af4a87b">

3. pass the code inside the workbook, change the container-name to (bronze, silver, gold) and storage-account-name to storage account

``ruby
configs = {
  "fs.azure.account.auth.type": "CustomAccessToken",
  "fs.azure.account.custom.token.provider.class": spark.conf.get("spark.databricks.passthrough.adls.gen2.tokenProviderClassName")
}
# Optionally, you can add <directory-name> to the source URI of your mount point.
dbutils.fs.mount(
  source = "abfss://<container-name>@<storage-account-name>.dfs.core.windows.net/",
  mount_point = "/mnt/<mount-name>",
  extra_configs = configs)
``
<img width="391" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/f6d3bc66-3cea-4b48-8c08-6094ac534d99">

## Part 6 - Data Transformation (2) | End to End Azure Data Engineering Project

so next we are going to do transformation from bronze to silver and silver to gold

1. create 2 more workbooks and rename them to bronze to silver and silver to gold
<img width="307" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/7d1ca1ed-9c04-4644-9fac-f140ae8bd9d7">

2. open the bronze to silver workbook and write all these codes:

``ruby
dbutils.fs.ls('mnt/bronze/SalesLT/') <br />
dbutils.fs.ls('mnt/silver/')
`` <br />
``ruby
dbutils.fs.ls('mnt/silver/')
``
``ruby
input_path = 'mnt/bronze/SalesLT/Address/Address/parquet'
``
``ruby
df = spark.read.format('parquet').load(input_path)
``








## Part 7 - Data Transformation (3) | End to End Azure Data Engineering Project
## Part 8 - Data Loading (Azure Synapse Analytics) | End to End Azure Data Engineering Project
## Part 9 - Data Reporting (Power BI) | End to End Azure Data Engineering Project 
## Part 10 - Security and Governance (AAD) | End to End Azure Data Engineering Project
## Part 11 (FINAL) - END to END Pipeline Testing | Azure Data Engineering End to End Real Time Project
