# Customer360_DLT_Project

# Customer 360 Analytics using Delta Live Tables (DLT) on Databricks

## 📌 Project Overview
This project demonstrates the use of **Delta Live Tables (DLT)** to build a scalable ETL pipeline for Customer 360 analytics.  
The pipeline ingests **Customer Profiles, Orders, and Support Tickets**, applies transformations, and generates **business KPIs** such as:

- Average resolution time by customer region
- Customer lifetime value (CLV)
- Support ticket volume trend analysis

## 🏗️ Architecture
1. **Ingestion**: Raw CSVs are ingested from Azure Data Lake (ADLS) into Bronze tables.
2. **Transformation**: Data is cleaned, joined, and enriched in Silver tables.
3. **Aggregation & KPIs**: Gold tables compute business metrics for reporting.
4. **Visualization**: Results can be consumed via Databricks SQL dashboards or Power BI.

<img width="959" height="502" alt="image" src="https://github.com/user-attachments/assets/5c5c3233-a1cb-4d6c-9148-e00ef473dae6" />

## 🚀 Tech Stack
- **Azure Databricks** (Delta Live Tables, PySpark, Delta Lake)
- **Azure Data Lake Storage (ADLS Gen2)**
- **Python**
- **Terraform (optional for infra setup)**

## 📂 Repository Structure
- `notebooks/` → DLT notebooks for ingestion, transformations, KPIs
- `datasets/` → Sample CSVs for practice
- `dlt_pipeline.json` → Pipeline configuration

## ▶️ How to Run
1. Upload datasets to your ADLS container.
2. Import notebooks into Databricks workspace.
3. Deploy `dlt_pipeline.json` in Databricks DLT UI.
4. Start the pipeline and explore results.

## 📊 Example KPI
```sql
-- Average resolution time per customer
SELECT 
    c.customer_id,
    c.customer_name,
    ROUND(AVG(t.resolution_time), 2) AS avg_res_time
FROM customers c
LEFT JOIN tickets t ON c.customer_id = t.customer_id
GROUP BY c.customer_id, c.customer_name;
