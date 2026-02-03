# 🏗️ SQL Server Data Warehouse: Bronze-Silver-Gold Architecture

[![SQL Server](https://img.shields.io)](https://www.microsoft.com)
[![Architecture](https://img.shields.io)](https://learn.microsoft.com)
[![License: MIT](https://img.shields.io)](https://opensource.org)

## 📌 Project Overview
This project implements a complete end-to-end **Data Warehouse** using the **Medallion (Bronze → Silver → Gold)** architecture within SQL Server. It demonstrates a robust ETL pipeline—transforming raw, fragmented data from CRM and ERP systems into an analytics-ready Star Schema.

---

## 🧱 Architecture Details

The pipeline follows a structured three-layer approach to ensure data integrity and traceability:

1.  **Bronze (Raw):** Landing zone for source data (CSV). Truncate-and-load strategy to preserve original state.
2.  **Silver (Cleansed):** Data standardization, deduplication (Window Functions), and business rule application.
3.  **Gold (Analytics):** Consumer-ready layer featuring a **Star Schema** (Fact & Dimension views) optimized for Power BI/Tableau.

---

## 🗄️ Database Design

**Database Name:** `DataWarehouse`

| Schema | Layer | Purpose |
| :--- | :--- | :--- |
| `bronze` | **Raw** | Direct ingestion of CRM/ERP files. |
| `silver` | **Transformed** | Cleansed, standardized, and validated data. |
| `gold` | **Presentation** | Business-ready Dimension and Fact views. |

---

## 🚀 ETL Process & Transformations

### 1. Ingestion (Bronze)
Managed via stored procedures using `BULK INSERT`. 
- **Action:** `EXEC bronze.load_bronze;`

### 2. Processing (Silver)
High-level transformations applied:
- **Deduplication:** Utilizing `ROW_NUMBER()` to identify latest records.
- **Normalization:** Standardizing Gender (M/F → Male/Female) and Marital Status.
- **Data Integrity:** Handling `NULL` values, trimming whitespace, and correcting invalid sales calculations.
- **Action:** `EXEC silver.load_silver;`

### 3. Dimensional Modeling (Gold)
Designed as a **Star Schema** for high-performance querying:
- **`gold.dim_customers`**: Unified view of CRM & ERP customer data.
- **`gold.dim_products`**: Product details enriched with category hierarchies.
- **`gold.fact_sales`**: Central transaction table linked via surrogate keys.

---

## 🛠️ Tech Stack & Key Concepts
*   **Engine:** [Microsoft SQL Server](https://www.microsoft.comsql-server-downloads)
*   **Language:** T-SQL (Stored Procedures, Views, CTEs, Window Functions)
*   **Modeling:** Star Schema (Fact & Dimension Tables)
*   **Concepts:** Data Quality, SCD (Slowly Changing Dimensions) logic, and Error Handling.

---

## 📈 Future Enhancements
- [ ] Implement **Incremental Loading** to reduce processing time.
- [ ] Add **Data Quality Tests** (Great Expectations style) within SQL.
- [ ] Integrate **SSIS or Azure Data Factory** for orchestration.
- [ ] Implement **SCD Type 2** for historical tracking in dimensions.

---

## 📝 How to Run
1. Execute the scripts in the `/scripts/schema/` folder to create the database and layers.
2. Run the Bronze load procedure:
   ```sql
   EXEC bronze.load_bronze;
   ```
3. Run the Silver transformation procedure:
   ```sql
   EXEC silver.load_silver;
   ```
4. Query the Gold views for reporting!
   ```sql
   SELECT * FROM gold.fact_sales;
   SELECT * FROM gold.dim_customer;
   SELECT * FROM gold.dim_product;
   ```
---

**Learned Recorce:** YouTube

**Tought By:** DataWithBaraa

**Author:** Ozodbek Ozodov
