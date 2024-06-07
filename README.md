# Onwelo-
assignment
**The csv files are sent by the client to the email address you have access to. The files are to be downloaded automatically because they have a fixed name. The files are to be saved on the Azure platform.**
1. What tools will you use to download the files, where will you save them?

   **Azure Databricks (Pyspark notebook) or Azure VM (Python + Airflow)**
      •	Connect to mail server
      •	Filter emails with attachments
      •	Extract attachments to files
      •	Save files in Azure Blob Storage / ADLS Gen2 as csv files ( Bronze Layer)  

2. What will be the connection between the tools you choose?
 Ans: Azure Databricks notebook can be used for developing code and scheduling on cluster. Azure Databricks can be easily integrated with Azure blob storage and SQL database.
      ADLS Gen2 can be mounted on DBFS (databricks file system). SQL server can be connected though JDBC
   For Python: sqlalchemy, Azure DataLake service client libraries can be used;
  
**After saving, the files are to be cleaned of rows that are empty, and after cleaning, the file is to be saved in such a way that they are available in the SQL serverless database. You should connect PowerBi to this server and publish the report online.**

1. With what tools will you do this and what will the connection between them look like?
Ans:
   **Azure Databricks (Pyspark notebook) or Azure VM (Python + Airflow)**
   •	Read files from Bronze layer
   •	Create dataframe (Pyspark / Pandas)
   •	Clean the data
   •	Write to Azure Blob Storage/ADLS Gen2 as json / parquet files (Silver Layer)
   •	Create / Update external tables in Azure SQL serverless database (Gold Layer)
   Gold layer is something which is readily consumed by Power BI  for preparing Dashboards with minimum calculations and transformations
   
2. How will the connection between the SQL database and PowerBi online report look like?
Ans:
   From PowerBI  Desktop, connect to Azure SQL database in Direct Query mode to reflect the latest data changes more frequently
Or from app.powerbi.com  use Dataflow to import data from Azure SQL database ,  build pipeline and schedule 
Prepare Dashboards and publish to web with embeded URL
Save this URL as html file
Open this html file when required to monitor the Dashboards created in PowerBI
This embeded URL can also be used as iframe in any Web Application (React.js)

**In addition, write how the particular items will be run and what tool you will use to monitor the entire process and inform the user via email about the execution or error in the process.**
Ans:
  Depending on scheduled frequency of Azure Databricks Notebook / Airflow job, Data gets refreshed and dashboards will be updated
  Email communication can be setup both in both Azure Databricks and Airflow to communicate Success / Failure of jobs.
  Logs can be used to diagnose the error and fix the pipeline
