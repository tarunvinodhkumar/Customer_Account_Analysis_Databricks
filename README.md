📌 Project Overview

This project demonstrates an end-to-end Azure Data Engineering pipeline built using:

Azure Data Factory (ADF)

Azure Data Lake Storage Gen2 (ADLS Gen2)

Azure Databricks (PySpark & Delta Lake)

Azure Key Vault

Power BI

The objective is to ingest raw banking-related data from an on-premises SQL Server, process and transform it using Databricks, implement Slowly Changing Dimensions (SCD Type 1), and build analytical insights using Power BI.

The project follows the Medallion Architecture:

🥉 Bronze Layer – Raw data ingestion

🥈 Silver Layer – Cleaned and transformed data

🥇 Gold Layer – Curated business-ready data in Delta format

🏗️ Architecture Overview

Data is extracted from On-Prem SQL Server using Azure Data Factory.

Data is landed in ADLS Gen2 (Bronze Layer).

Azure Databricks reads raw data from ADLS.

Data transformations are performed using PySpark.

Cleaned data is stored as Delta Tables (Silver Layer).

SCD Type 1 logic is applied and stored in Gold Layer.

Power BI connects to curated datasets for reporting.

🛠️ Technologies Used

Azure Data Factory

Azure Data Lake Storage Gen2

Azure Databricks

Delta Lake

PySpark

Azure Key Vault

Power BI

📂 Project Implementation Steps
🔹 Step 1: ADLS Gen2 to Databricks Connectivity

A separate notebook is created for establishing secure connectivity between ADLS Gen2 and Databricks.

Supported Authentication Methods:

✅ SAS Key Method

✅ Account Key Method

✅ Service Principal Method (Recommended)

This notebook is called inside the transformation notebooks to maintain modular design.

🔹 Step 2: Data Transformation – Silver Layer

Data cleaning and transformation performed using PySpark:

✔ Transformations Applied:

Null checks

Date validations

Duplicate checks

Removing unnecessary columns

Renaming columns

Adding Timestamp column

Data quality validations

📌 5 tables are processed (either 5 notebooks or a single cleaning notebook).

Output:

Cleaned data stored as Managed Delta Tables

Stored in Silver Layer

🔹 Step 3: Sales Analysis Notebook

A separate notebook is created with manually generated data:

Columns:

Sales ID

Sales Quantity

Selling Price

Cost

Product Name

Customer Name

Calculated Columns:

Revenue = Sales Quantity × Selling Price

Profit = Revenue − (Sales Quantity × Cost)

Stored As:

Delta Table with:

sales_id, sales_quantity, selling_price, cost,
product_name, customer_name, profit, revenue

Analytical Queries:

🔝 Highest cost per product

🏆 Customer who bought highest number of items

🔹 Step 4: SCD Type 1 Implementation – Gold Layer

Slowly Changing Dimension (Type 1) implemented for one Silver table.

SCD Type 1 Logic:

Overwrites old records with new values

No history maintained

Implemented using Delta Merge operation

Output:

Stored as Delta Table in Gold Layer

🔐 Security Implementation

Azure Key Vault used for secure credential management

Dynamic parameters used for scalable pipeline execution

Service Principal authentication supported
