Retail Data Engineering Pipeline: BuyAnything Sales Analytics
Project Overview
This project demonstrates a robust End-to-End Data Engineering pipeline built on Azure. It implements a Medallion Architecture (Bronze, Silver, Gold) to transform raw retail sales data into a structured Star Schema for analytical reporting. The project handles incremental data loading, data cleaning, and complex dimension/fact modeling using PySpark and Delta Lake.

Architecture & Technology Stack
Source: Azure SQL Database (Transactional Sales Data).

Orchestration: Azure Data Factory (ADF) using Incremental Pipelines (Watermark mechanism).

Data Lake: Azure Data Lake Storage (ADLS) Gen2 with Medallion layers.

Processing: Azure Databricks / Spark for ETL transformations.

Storage Format: Delta Lake (supporting ACID transactions and Merges).

Language: PySpark (Python) and SQL.

Data Pipeline Flow
1. Ingestion (Bronze Layer)
Used Azure Data Factory to create an incremental copy pipeline.

Implemented a Watermark table logic to fetch only new or updated records from Azure SQL DB, reducing processing costs.

Raw data is stored in the Bronze container in Parquet format.

2. Transformation (Silver Layer)
Data is read from Bronze and cleaned using PySpark.

Cleaning steps: Handling null values in SalesRegion (replaced with 'Central'), formatting date columns, and deduplication.

Cleaned data is saved as Delta tables in the Silver layer.

3. Dimensional Modeling (Gold Layer)
The data is modeled into a Star Schema to optimize query performance for BI tools:

Dimension Tables: Created Dim_Customer, Dim_Product, Dim_Date, and Dim_SalesRegion.

Fact Table: Created Fact_Sales by joining silver data with dimension keys.

Upsert Logic: Implemented MERGE operations in Delta Lake to handle record updates and prevent duplicates using unique surrogate keys.

Key Features Implemented
Incremental Loading: Efficiently moves data without reloading the entire dataset.

Null Handling: Advanced PySpark logic to clean and standardize categorical fields.

Error Handling: Addressed DELTA_MULTIPLE_SOURCE_ROW_MATCHING errors by implementing strict deduplication (dropDuplicates) before merging into Gold.

Optimized Performance: Configured Spark shuffle partitions and utilized Delta Lake's OPTIMIZE features for single-node efficiency.
