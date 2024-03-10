# Project Overview
This project revolves around extracting data from a local machine to explore and implement the Azure Self Hosted Integration Runtime concept. Initially, my laptop serves as the local machine, yet in practical scenarios, this could originate from any servers in data centers. Using this data source, we employ Azure Data Factory pipelines to stage it into the data lake in a parquet format. Subsequently, we adopt the lakehouse architecture, designating the staging layer as the bronze layer. Leveraging Databricks notebook, we execute transformations to transition data from the bronze to the silver layer. Finally, the refined data, structured according to the Data Warehouse schema, is stored in the gold layer for PowerBI visualizations.

# Project Architecture
![lakearch](https://github.com/sathyaNEU/Azure-Lakehouse-Project/assets/144740003/e929be83-589e-4c47-bdde-9edc3cde4490)

# Tools 
+ Microsoft SQL Server
+ Azure Data Lake Gen2
+ Azure Data Factory
+ Azure Databricks
+ Azure Key Vault
+ Microsoft Power BI

## Workflows
+ Branch : collab-self/pipeline/SqlServerDataIngestion_bronze_Pipeline.json - Utilizing the Azure Self Hosted Integrated Runtime, this pipeline extracts data from a Microsoft SQL Server DB located on my local machine, and stages as it is into the bronze layer within Azure Data Lake Gen2.
+ Branch : collab-self/pipeline/CreateViewForAllTables.json - The pipeline initiates its child copy data activity, triggering the internally compiled stored procedure within the Synapse SQL workspace for execution. Primarily, the stored procedure generates views based on input files passed from the parent activity. Subsequently, the pipeline scans all parquet files within the gold layer, generating corresponding views.

## Transformations
+ Replaced all nulls with appropriate values specific to each table
+ Converted column name's as per the case requirement of this project
+ Filtered rows from the input schema as per business requirement assumed for this project
+ Mapped price category for SalesOrderHeader fact table based on purchase price range csv file
+ To enhance the project's complexity, Bad Data was injected into the SalesLT schema. Subsequently, a data cleaning pipeline was implemented to scrutinize whether ZipCodes are correctly associated with their respective geographic locations.

## Security
+ All credentials integrated into the pipelines were secured via Azure Key Vault, safeguarding the code's confidentiality when deployed onto public platforms like Git.
+ Access privileges were regulated using System Assigned Managed Identity, SAS, and Account keys wherever applicable.
