# Credit Card Fraud ETL Pipeline (Bronze → Silver → Gold)

## Project Overview

This project demonstrates a **full end-to-end ETL pipeline** using **Databricks, PySpark, Delta Lake, and GCP** for analyzing credit card fraud data.  

The pipeline follows a **Medallion Architecture** (Bronze → Silver → Gold), simulating an enterprise-grade data engineering workflow. It also includes **dashboards and visualizations** for fraud analysis.

---

## Dataset

- **Source:** Credit Card Transactions dataset (`creditcard.csv`)  
- **Size:** ~284,807 transactions  
- **Columns:**  
  - `Time` : Seconds since the first transaction  
  - `V1` … `V28` : Principal components of anonymized features  
  - `Amount` : Transaction amount  
  - `Class` : Fraud label (0 = Non-fraud, 1 = Fraud)  

- **Storage:** Uploaded to **GCS bucket** and accessed via **Databricks External Catalog**

---

## Architecture
Bronze Layer
└── Raw CSV data from GCS
Silver Layer
└── Cleaned, deduplicated, typed Delta table
Gold Layer
└── Aggregated tables for analysis:
- Fraud % by Amount Bucket
- Top 10 High-Risk Transactions
- Hourly Fraud Trends
- Fraud vs Non-Fraud Summary
Visualizations
└── Databricks dashboards using Gold tables

## Technologies Used

- **Databricks** (Notebook + Delta Lake + SQL + Dashboard)  
- **PySpark** for ETL transformations  
- **GCP** (Google Cloud Storage for dataset storage)  
- **Delta Lake** for Silver/Gold tables  
- **GitHub** for version control  

---

## Pipeline Details

### 1. Bronze Layer
- Raw ingestion from `creditcard.csv` in GCS
- Table: `creditcard_bronze`
- Contains **original data with no cleaning**

### 2. Silver Layer
- Cleaned, deduplicated, typed data  
- Table: `creditcard_silver`  
- Transformations:
  - Removed duplicates
  - Filled nulls
  - Cast `Amount` → double, `Class` → int

### 3. Gold Layer
- Aggregated and analytics-ready tables:

| Table | Description |
|-------|------------|
| `gold_fraud_amount_bucket` | Fraud percentage by transaction amount ranges |
| `gold_top_risk_txns` | Top 10 highest-amount fraudulent transactions |
| `gold_fraud_hourly` | Hourly fraud trend analysis |
| `gold_fraud_summary` | Summary stats for fraud vs non-fraud |

- Advanced metrics like **fraud correlation with transaction amount** also computed.

---

## Visualizations & Dashboards

- **Fraud % by Amount Bucket** → Bar Chart  
- **Hourly Fraud Trend** → Line Chart  
- **Top 10 High-Risk Transactions** → Table Visualization  
- **Fraud vs Non-Fraud Summary** → Pie/Bar Chart  
- **Dashboard Screenshot Examples**:

![Dashboard Example](images/dashboard.png)  

> Dashboards created using Databricks SQL visualization tools.

---

## How to Run

1. **Open the notebook** in Databricks Workspace (`CreditCard_Fraud_ETL.ipynb`)  
2. Make sure you have a **running cluster** attached  
3. Run **cells sequentially**:  
   - Bronze ingestion (load raw CSV)  
   - Silver cleaning & transformation (deduplicate, cast types, fill nulls)  
   - Gold aggregation & advanced metrics  
4. View Gold tables via **Catalog → creditcard_schema**  
5. Create **visualizations** from Gold tables:  
   - Bar chart: Fraud % by Amount Bucket  
   - Line chart: Hourly Fraud Trend  
   - Pie/Bar chart: Fraud vs Non-Fraud Summary  
6. Combine visuals into a **Databricks Dashboard**  
7. Optional: Take **screenshots of dashboards** to include in GitHub for portfolio showcase  

> ✅ Note: In Databricks notebooks, SQL cells are executed natively. No conversion is needed. 

---

## Project Highlights

- Enterprise-grade **Medallion Architecture** implementation  
- End-to-end **ETL with PySpark + Delta Lake**  
- Advanced **fraud analytics tables**  
- **Visualization-ready Gold layer** for dashboards  
- GitHub-ready for **interview showcase**

## Repository Structure

CreditCard_Fraud_ETL/
├── CreditCard_Fraud_ETL.py # Main Databricks notebook
├── images/ # Screenshots of dashboards
├── README.md # Project documentation
├── requirements.txt # PySpark dependencies (optional)



## Contact

- **Name:** Lakshmikanth Gandham  
- **GitHub:** [https://github.com/lakshmikanthgandham/dbc_creditcardanalysis] 
- **Email:** lakshmikanth.gandham9@gmail.com
