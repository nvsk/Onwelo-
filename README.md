# Onwelo-
assignment
**The csv files are sent by the client to the email address you have access to. The files are to be downloaded automatically because they have a fixed name. The files are to be saved on the Azure platform.** <br />
**1. What tools will you use to download the files, where will you save them?** <br />
**Ans:** <br />
   **Azure Databricks (Pyspark notebook) or Azure VM (Python + Airflow)**<br />
      •	Connect to mail server<br />
      •	Filter emails with attachments<br />
      •	Extract attachments to files<br />
      •	Save files in Azure Blob Storage / ADLS Gen2 as csv files ( Bronze Layer) <br /> 

**2. What will be the connection between the tools you choose?**<br />
 **Ans:** <br />
       Azure Databricks notebook can be used for developing code and scheduling on cluster. <br />
       Azure Databricks can be easily integrated with Azure blob storage and SQL database.<br />
      ADLS Gen2 can be mounted on DBFS (databricks file system). SQL server can be connected though JDBC; <br />
       For Python: sqlalchemy, Azure DataLake service client libraries can be used;<br />
  
**After saving, the files are to be cleaned of rows that are empty, and after cleaning, the file is to be saved in such a way that they are available in the SQL serverless database. You should connect PowerBi to this server and publish the report online.**<br />

**1. With what tools will you do this and what will the connection between them look like?**<br />
**Ans:**<br />
   **Azure Databricks (Pyspark notebook) or Azure VM (Python + Airflow)**<br />
   •	Read files from Bronze layer<br />
   •	Create dataframe (Pyspark / Pandas)<br />
   •	Clean the data<br />
   •	Write to Azure Blob Storage/ADLS Gen2 as json / parquet files (Silver Layer)<br />
   •	Create / Update external tables in Azure SQL serverless database (Gold Layer)<br />
   Gold layer is something which is readily consumed by Power BI  for preparing Dashboards with minimum calculations and transformations<br />
   
**2. How will the connection between the SQL database and PowerBi online report look like?**<br />
**Ans:**<br />
   From PowerBI  Desktop, connect to Azure SQL database in Direct Query mode to reflect the latest data changes more frequently<br />
Or from app.powerbi.com  Dataflow can be used to import data from Azure SQL database ,  build pipeline and schedule <br />
Prepare Dashboards and publish to web with embeded URL<br />
Save this URL as html file<br />
Open this html file when required to monitor the Dashboards created in PowerBI<br />
This embeded URL can also be used as iframe in any Web Application (React.js)<br />

**In addition, write how the particular items will be run and what tool you will use to monitor the entire process and inform the user via email about the execution or error in the process.**<br />
**Ans:**<br />
  Depending on scheduled frequency of Azure Databricks Notebook / Airflow job, Data gets refreshed and dashboards will be updated<br />
  Email communication can be setup both in both Azure Databricks and Airflow to communicate Success / Failure of jobs<br />
  Logs can be used to diagnose the error and fix the pipeline<br />
