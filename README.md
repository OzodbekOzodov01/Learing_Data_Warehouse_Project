# 🏗️ SQL Data Warehouse Project (Bronze–Silver–Gold Architecture)

This project implements a **modern Data Warehouse** using **SQL Server** following the **Bronze → Silver → Gold** layered architecture.  
It demonstrates how to ingest raw data, clean and transform it, and finally expose analytics-ready datasets using dimensional modeling.

---

## 📌 Architecture Overview

The Data Warehouse is organized into three logical layers:

Source Systems (CSV Files)
↓
🟫 Bronze Layer (Raw Data)
↓
⬜ Silver Layer (Cleansed & Standardized)
↓
🟨 Gold Layer (Analytics / Star Schema)


---

## 🗄️ Database & Schema Setup

- Database Name: `DataWarehouse`
- Schemas:
  - `bronze` → Raw ingestion layer
  - `silver` → Cleaned and transformed layer
  - `gold` → Business-ready dimensional views

---

## 🟫 Bronze Layer (Raw Data)

### 🎯 Purpose
- Store **raw, unprocessed data**
- Exact structure as received from source systems
- No transformations or business logic applied

### 📂 Source Systems
- **CRM System**
- **ERP System**

### 📋 Bronze Tables

| Table Name | Description |
|-----------|-------------|
| `bronze.crm_cust_info` | Raw CRM customer data |
| `bronze.crm_prd_info` | Raw CRM product data |
| `bronze.crm_sales_details` | Raw CRM sales transactions |
| `bronze.erp_loc_a101` | ERP customer location data |
| `bronze.erp_px_cat_g1v2` | ERP product category data |
| `bronze.erp_cust_az12` | ERP customer demographic data |

### 🔄 Data Load
Data is loaded from CSV files using `BULK INSERT`.

Stored Procedure:
```sql
EXEC bronze.load_bronze;

### Key Characteristics
- Tables truncated before loading
- Data loaded using BULK INSERT
- Load duration logging
- Error handling using TRY...CATCH

