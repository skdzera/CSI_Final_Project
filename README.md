# CSI_DE_Project

End-to-End Data Pipeline Automation Using Azure Data Factory (SQL + CSV to JSON/Parquet)

# Project Overview
I would like to express my sincere gratitude to CSI (Celebal Summer Internship) for providing me the opportunity to work on this comprehensive Azure Data Factory ETL Project as part of my internship. The mentorship, guidance, and exposure to real-world data engineering tasks have significantly deepened my technical skills and understanding of modern data pipelines.
The original tasks were designed for implementation using Azure Data Factory with Azure SQL Database and Azure Data Lake Storage Gen2. However, due to environmental constraints during development, I simulated part of the process locally using SQL Server and Azure Storage Emulator, while preserving the project’s architectural integrity and objectives.

This hands-on adaptation allowed me to focus on core Data Engineering concepts such as:
1. Threshold-based conditional data extraction.
2. Automated dynamic folder structuring to handle file versioning.
3. Parameterized data ingestion using pipeline looping constructs.
4. Data merging and transformation using SQL and CSV sources.
5. Output optimization via structured formats like JSON and Parquet.

Completing this end-to-end project has enabled me to better understand the importance of modular pipeline design, data governance, and cloud-agnostic architectural patterns within the ETL lifecycle.

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

# Project Architecture
          +--------------------+
          | Threshold File (.csv) |
          |    (Stored in ADLS)   |
          +----------+-----------+
                     |
                     v
        +-------------------------------------+
        | Pipeline 1: Threshold-Based Copy    |
        |-------------------------------------|
        | - Read threshold from file          |
        | - Query SQL Customer table count    |
        | - If count > threshold:             |
        |    Copy Customer data to ADLS (JSON)|
        +-------------------------------------+
                     |
                     v
    +---------------------------------------------+
    | ADLS Folder Structure (Customer/YYYY/MM/DD) |
    +---------------------------------------------+


                   +-------------------------+
                   | Pipeline 2: Dynamic Foldering |
                   +-------------------------+
                                 |
                                 v
       +----------------------------------------------+
       | Ensures data saved into Customer/YYYY/MM/DD  |
       | folder structure every pipeline execution    |
       +----------------------------------------------+


                   +-------------------------+
                   | Pipeline 3: Foreach_Example2 |
                   +-------------------------+
                                 |
                                 v
    +--------------------------------------------------------------+
    | - Fetch Products (ProductID > 100)                           |
    | - Fetch Customers (100 < CustomerID < 1000)                  |
    | - Single Copy Activity using ForEach Loop                    |
    | - Store both datasets in ADLS                                |
    +--------------------------------------------------------------+


                   +----------------------------+
                   | Pipeline 4: Customer-Address Join |
                   +----------------------------+
                                 |
                                 v
    +-------------------------------------------------------------+
    | - Read Customer table from SQL Database                     |
    | - Read Customer Address CSV from ADLS                       |
    | - Join both datasets on CustomerID                          |
    | - Filter: 1000 < CustomerID < 2000                          |
    | - Sort ascending, save as Parquet file to ADLS              |
    +-------------------------------------------------------------+


# Datasets and Outputs

<img width="1908" height="919" alt="image" src="https://github.com/user-attachments/assets/6ad5386a-9ef7-47c4-a60b-a398b2ec2f92" />



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


