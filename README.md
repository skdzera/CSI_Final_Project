# CSI_DE_Project

Azure Data Integration & Pipeline Automation
# Project Overview
This project automates data extraction and transformation tasks using Azure Data Factory (ADF), Azure SQL Database,Microsoft SQL Server and Azure Data Lake Storage (ADLS). It covers conditional data copying, dynamic folder structuring, optimized data processing, and data joining using SQL and CSV sources.


# 📁 Repository Structure
```plaintext
├── ARM_config/                # ARM templates for resource deployments
├── PNGS/                      # Pipeline diagrams and screenshots
├── dataflow/                  # Dataflow JSON files for transformation logic
├── dataset/                   # Dataset JSON files (e.g., DS_thresholdCSV)
├── factory/                   # ADF factory configuration files
├── integrationRuntime/        # Integration Runtime configurations
├── linkedService/             # SQL DB and ADLS linked service definitions
├── managedVirtualNetwork/     # Virtual Network configurations (if used)
├── pipeline/                  # Main pipeline definitions
│   ├── customerjoin.json
│   ├── csiprojectpipeline1.json
│   ├── Foreach_Example2.json
│   └── SQL_CSV_Join_Parquet_Pipeline.json
├── publish_config.json        # Publishing configuration
└── README.md                  # Project documentation

```


# 1️⃣ Threshold-Based Conditional Copy
Reads threshold from CSV (DS_thresholdCSV) in ADLS.

Counts records in SQL Customer table.

If record count > threshold:

Copies data to ADLS in JSON format.

# 2️⃣ Dynamic Folder Structure Pipeline
Every pipeline run stores output in:

swift
Copy
Edit
Customer/YYYY/MM/DD/
Prevents overwriting and supports versioned data storage.

# 3️⃣ Foreach_Example2 Pipeline
Single Copy Activity extracts:

Product data where ProductID > 100.

Customer data where 100 < CustomerID < 1000.

# 4️⃣ SQL + CSV Join and Save as Parquet
Reads Customer data from SQL to azure sql database

Reads CustomerAddress from CSV.

Joins both datasets.

Filters where 1000 < CustomerID < 2000 and sorts in ascending order.

Saves output as a Parquet file in ADLS.


Execution:

Run pipelines directly from ADF.

Monitor via ADF Monitoring tab.


