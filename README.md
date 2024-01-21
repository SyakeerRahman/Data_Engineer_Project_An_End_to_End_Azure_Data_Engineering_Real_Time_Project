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

# create a resource group - (rg-data-engineering-project) and inside it create:

1. Azure Data Factory
2. Azure Databricks
3. Storage Account
4. Azure Synapse Analytics
5. Key Vault

<img width="436" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/05f0274f-da6a-4123-9bbb-cc0edf727594">

# open ssms and restore database AdventureWorks (version according to your SSMS version) and create user login and password

``ruby
create login syakeer with password = '!@#Password!'
create user syakeer for login syakeer
`` 

# open key vault resources and generate 2 secret key where 1 for username = syakeer and 1 for password = !@#Password!'

<img width="567" alt="image" src="https://github.com/SyakeerRahman/Data_Engineer_Project_An_End_to_End_Azure_Data_Engineering_Real_Time_Project/assets/105381652/de14baf3-b747-4c9e-89b8-ed47a43f6f06">

## Part 3- Data Ingestion (1) | End to End Azure Data Engineering Project
## Part 4- Data Ingestion (2) | End to End Azure Data Engineering Project
## Part 5 - Data Transformation (1) | End to End Azure Data Engineering Project |Mounting the Datalake
## Part 6 - Data Transformation (2) | End to End Azure Data Engineering Project
## Part 7 - Data Transformation (3) | End to End Azure Data Engineering Project
## Part 8 - Data Loading (Azure Synapse Analytics) | End to End Azure Data Engineering Project
## Part 9 - Data Reporting (Power BI) | End to End Azure Data Engineering Project 
## Part 10 - Security and Governance (AAD) | End to End Azure Data Engineering Project
## Part 11 (FINAL) - END to END Pipeline Testing | Azure Data Engineering End to End Real Time Project
