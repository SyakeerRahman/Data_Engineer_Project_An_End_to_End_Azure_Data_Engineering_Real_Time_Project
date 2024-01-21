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

<img width="502" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/1e53ef30-d628-441a-a041-fb04b95a9041">

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

<img width="502" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/73de6822-4cb7-4ef7-b03a-1ae7ca35b551">

so next we are going to do transformation from bronze to silver and silver to gold

1. create 2 more workbooks and rename them to bronze to silver and silver to gold
<img width="307" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/7d1ca1ed-9c04-4644-9fac-f140ae8bd9d7">

2. open the bronze to silver workbook and write all these codes:

```
dbutils.fs.ls('mnt/bronze/SalesLT/') 

dbutils.fs.ls('mnt/silver/')

input_path = 'mnt/bronze/SalesLT/Address/Address/parquet'

df = spark.read.format('parquet').load(input_path)

display(df)

from pyspark.sql.functions import from_utc_timestamp, date_format
from pyspark.sql.types import TimestampType
df = df.withColumn("ModifiedDate", date_format(from_utc_timestamp(df["ModifiedDate"].cast(TimestampType()), "UTC"), "yyyy-MM-dd"))

display(df)

%md
DOING TRANSFORMATION FOR ALL TABLES


table_name = []
for i in dbutils.fs.ls('mnt/bronze/SalesLT/'):
   table_name.append(i.name.split('/')[0])

table_name

from pyspark.sql.functions import from_utc_timestamp, date_format
from pyspark.sql.types import TimestampType
for i in table_name:
   path = '/mnt/bronze/SalesLT/'+i+'/'+i+'.parquet'
   df = spark.read.format('parquet').load(path)
   column = df.columns
   for col in column:
      if "Date" in col or "date" in col:
         df = df.withColumn(col,date_format(from_utc_timestamp(df[col].cast(TimestampType()), "UTC"), "yyyy-MM-dd"))
    output_path = '/mnt/silver/SalesLT/' +i +'/'
    df.write.format('delta').mode("overwrite").save(output_path)

display(df
```

3. open the silver to gold workbook and write all these codes:
```
dbutils.fs.ls('mnt/silver/SalesLT/') 

dbutils.fs.ls('mnt/gold/')

input_path = 'mnt/silver/SalesLT/Address/'

df = spark.read.format('delta').load(input_path)

display(df)

from pyspark.sql import SparkSession
from  pyspark.sql.functions import col, regexp_replace
column_names = df.columns
for old_col_name in column_names
   new_col_names = "".join(["_" + char if char.isupper() and not old_col_name[i-1].isupper() else char for i, char in enumerate(ild_col_name)]).lstrip("_")
   df = df.withColumnRenamed(old_col_name, new_col_name)

display(df)

table_name = []
for i in dbutils.fs.ls('mnt/silver/SalesLT/'):
   table_name.append(i.name.split('/')[0])

table_name

for name in table_name:
   path = '/mnt/silver/SalesLT/' + name
   print(path)
   df = spark.read.format('delta').load(path)
   column_names = df.columns
   for old_col_name in column_names:
      new_col_names = "".join(["_" + char if char.isupper() and not old_col_name[i-1].isupper() else char for i, char in enumerate(ild_col_name)]).lstrip("_")
    df = df.withColumnRenamed(old_col_name, new_col_name)
output_path = '/mnt/gold/SalesLT/' + name +'/'
df.write.format('delta').mode("overwrite").save(output_path)

display(df
```

## Part 7 - Data Transformation (3) | End to End Azure Data Engineering Project

<img width="502" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/773e1d7f-1031-4d63-bd12-615a09f84152">

Now, for this part we are going to automate the process of the pipeline from Bronze to Silver and Silver to Gold

1. firstly we are going to modified a lil bit of code that we have done by removing some of the unnecessary code, so just use the code below:

BRONZE TO SILVER
```
table_name = []
for i in dbutils.fs.ls('mnt/bronze/SalesLT/'):
   table_name.append(i.name.split('/')[0])

table_name

from pyspark.sql.functions import from_utc_timestamp, date_format
from pyspark.sql.types import TimestampType
for i in table_name:
   path = '/mnt/bronze/SalesLT/'+i+'/'+i+'.parquet'
   df = spark.read.format('parquet').load(path)
   column = df.columns
   for col in column:
      if "Date" in col or "date" in col:
         df = df.withColumn(col,date_format(from_utc_timestamp(df[col].cast(TimestampType()), "UTC"), "yyyy-MM-dd"))
    output_path = '/mnt/silver/SalesLT/' +i +'/'
    df.write.format('delta').mode("overwrite").save(output_path)

display(df
```

SILVER TO GOLD
```
table_name = []
for i in dbutils.fs.ls('mnt/silver/SalesLT/'):
   table_name.append(i.name.split('/')[0])

table_name

for name in table_name:
   path = '/mnt/silver/SalesLT/' + name
   print(path)
   df = spark.read.format('delta').load(path)
   column_names = df.columns
   for old_col_name in column_names:
      new_col_names = "".join(["_" + char if char.isupper() and not old_col_name[i-1].isupper() else char for i, char in enumerate(ild_col_name)]).lstrip("_")
    df = df.withColumnRenamed(old_col_name, new_col_name)
output_path = '/mnt/gold/SalesLT/' + name +'/'
df.write.format('delta').mode("overwrite").save(output_path)

display(df
```

2. Open Azure Data Factory and go to manage tab and create new linked services and add databricks
<img width="553" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/e45e38c8-5183-47c2-b149-d348c92f480f">

3. for the linked servce details, follow as below

<img width="230" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/d1baebd9-dc4f-47c9-a8af-78cb408b7a9f">

go to databricks and click on the username on the top right corner and click user setting, and click on generate new token, make sure to COPY THE TOKEN IMMEDIATELY
<img width="557" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/5856558c-7b68-4f07-a2ce-014cb8f17c8e">

now open Key Vault Resouces and create new secret key and paste the token inside secret value
<img width="323" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/04ceab5f-856a-412d-a4fc-2e2961af34ba">

continue the link service setup as below
<img width="213" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/7318d438-abcc-4eb3-8c19-a40793e1f422">

4. click publish all
<img width="421" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/c0b6a427-72a9-4515-be7b-ea9494ecae43">

5. now open back the ADF pipeline, and drag notebooks activites into the pipeline and set the path of notebooks using bronze to silver notebooks

<img width="562" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/d5cbd37c-f9d4-4a97-8bfa-deb309cc093d">
<img width="221" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/c740177a-177d-4dbd-8048-dba7eb095558">
<img width="215" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/89f4d31e-7170-4dc1-8545-e7d24db4d836">

6. repeat the same step but using silver to gold notebooks

<img width="458" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/9786d68b-9540-4ec0-acd0-af30efd6b1c6">

7. click publish and click trigger now. see the pipeline status under monitor tab

<img width="544" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/d227e9ab-2d48-4b24-8c86-e4e337a46abf">

## Part 8 - Data Loading (Azure Synapse Analytics) | End to End Azure Data Engineering Project

<img width="502" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/a0d881ef-0897-4c2a-9042-bdf1140ef804">

Now since we already have  a gold database, we are going to load it inside Azure Synapse Analytics which are  build on top of Azure Data Factory,
click on the azure synapse analytics resource and open Synapse Studio
<img width="257" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/53fecd4c-3fea-49cd-98f5-487da4ce56b8">

1. create a new sql database by going to data tab and click + and choose SQL database, we are going with serverless pool since we are just going to use the compute power to do the query and not dedicated pool since this will use the database and compute power (much expensive)
<img width="327" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/50cbf57a-458a-426a-878b-e66207736305">
<img width="116" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/a7ae108a-6fa3-4d33-9d57-b5fd4ff8fb90">


2. now go to the linked and query top 100  rows for address adn set the file format to delta
<img width="469" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/e910f25d-4ccd-49ee-a514-49f25bad6cfc">

3. create view address as we will use that later to connect to power bi
<img width="487" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/9a5c5b4c-6e43-47e6-bbbf-0842798c829b">

4. instead of repeating step 3 for all tables, we are going to build a pipeline that will create view for all the tables inside the synapse analytics. this step is quiet similar to the Part 4- Data Ingestion (2) | End to End Azure Data Engineering Project where we will use ForEach activity.

5. before that we need to write a stored procedure
<img width="541" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/30f5fe38-77b4-487d-ba3e-4b86270e347f">

```
USE gold_db
GO

CREATE OR ALTER PROC CreateSQLServerlessView_gold @ViewName nvarchar(100)
AS
BEGIN

DECLARE @statement VARCHAR(MAX)

  SET @statement = N'CREATE OR ALTER VIEW ' + @ViewName + ' AS
     SELECT *
     FROM
         OPENROWSET(
         BULK ''https://mrkdatalakegen2.dfs.core.windows.net/gold/SalesLT/' @ViewNAme + '/'',
         FORMAT = ''DELTA''
      ) as [result]


EXEC (@statement)

END
GO

```
6. create new link service for azure sql database and set the name to serverlessSQLdb
<img width="575" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/b865323c-870d-4324-955d-b68da201f948">
<img width="221" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/6babd486-f11d-48fc-9723-b95f38d219d8">


7. copy servelrless SQL endpoint to be paste into fully qualified domain name  
<img width="454" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/49ed0fab-074d-456d-a26e-be3aa7406194">


8. go to  integrate tab and click on metadata to create activity to get table names
<img width="499" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/d63db20d-d42c-4750-92c3-363e5d27d4e8">
<img width="536" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/914bfd97-a8da-4ee4-acb6-63f48c6164d1">

9. add ForEach activity into the pipeline and in the setting for items add dynamic content
<img width="461" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/eafea935-1d09-424d-ab0e-024c8281365b">
```
@activity('Get Tablenames').output.childItems
```

10. click on the pencil icon inside the ForEach activity to edit and drag stored procedure activity and in setting set the linked service to serverlessSQLdb
<img width="510" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/afcf8110-cea0-4047-aa0b-afd9109c5e89">
```
@item().name
```

11. publish the changes , add trigger and trigger now and see whether successful or not
<img width="554" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/d54c7676-195f-4892-a30b-01792a1fefa8">
<img width="206" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/1fa130d5-2df0-4cdf-919b-0cde0bb8bdb4">



## Part 9 - Data Reporting (Power BI) | End to End Azure Data Engineering Project 

<img width="543" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/6b91a64e-3f0c-4b7b-b48c-75538b527fdf">


1. Now we are going to connect Power BI desktop to the views gold_db that we have just created. so firstly make sure to open PowerBI desktop and on the source copy the serverless SQL endpoint from the synapse properties

<img width="422" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/5d04f545-3bb7-4dae-84ff-fb1cb195d97a">
<img width="459" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/6176fedf-f673-45e1-9a14-948862daed92">

sign in to microsoft account (the one with the pipeline just now)
<img width="293" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/1295fb5f-4079-4ae9-953b-85811f5c8b8e">

2. bring all the table inside power bi

3. manage the relationship between tables inside the powerbi
<img width="539" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/f54a5ff4-85b0-461c-8b17-fbd66c071d0f">

4. create your own dashoard using the data given
<img width="445" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/d46c6e6c-1558-4614-ad36-d1f8328c23f7">


## Part 10 - Security and Governance (AAD) | End to End Azure Data Engineering Project

since we ahve finished the reporting, what if we want to give permission to other data engineer or other employeee to access our resource group? the best way is to create group through azure active directory.

<img width="570" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/8023b3ac-0a0c-467c-a767-d47152435955">

1. open Azure Active Directory resources and click on the group
<img width="387" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/dffa29d7-b560-4531-9675-967d46796587">

2. create a new group, give the owner role to you and member can be add accordingly to the reuqirement

<img width="312" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/c13747e8-9153-497c-93d0-3a0f230d8caf">

3. go to resource group, under IAM tab, click + and add role assignment, this will give permission to those who are needed to manage the resource also

<img width="340" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/02b0ffd8-87b9-4083-a248-896aa6ee7395">
<img width="224" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/000e897d-2d88-43dd-9d32-51e9cd5367c2">
<img width="308" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/b2cf669b-ec67-4c36-b849-2d9b030e63e7">

4. now those with permission can access the resources and do any changes/ maintain the resources.


## Part 11 (FINAL) - END to END Pipeline Testing | Azure Data Engineering End to End Real Time Project

1. Now we will set a trigger time that will trigger the pipeline to run at certain time so that we dont need to trigger it manually everytime. Go to ADF resource and click on the active pipeline and add trigger. and publish it

<img width="544" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/f07a2372-67cc-4ede-8c8d-2e0f71424434">

2. Now we will go to the SSMS to insert new data inside Customer data

```
SET IDENTITY_INSERT [AdventureWorksLT2019].[SalesLT].[Customer]
([CustomerID],
 [NameStyle],
 [Title],
 [FirstName],
 [MiddleName],
 [LastName],
 [Suffix],
 [CompanyName],
 [SalesPerson],
 [EmailAddress],
 [Phone],
 [PasswordHash],
 [PasswordSalt],
 [rowguid]
 [ModifiedDate])
VALUES
(595959,'Mr.','John','SR','Max','Jr.','xyz','adventure-works\John','john@gmail.com','13456-095-0045','Trade','Analyst','1F54D149-9FDD-B425-BAE25CE','2015-12-12')

SET IDENTITY_INSERT [AdventureWorksLT2019].[SalesLT].[Customer] OFF;
```

3. we can see the pipeline in process at that time that we set the trigger.
<img width="593" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/0d6afef1-1d72-4a27-8546-8366a7425c1c">
