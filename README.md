# biovanguard-life-sciences-commercial-analytics
End-to-end Life Sciences Commercial Analytics project using Databricks, PySpark, SQL, Delta Lake, Medallion Architecture, SCD Type 2, incremental data loading, data quality validation, dimensional modeling, and interactive dashboards for pharmaceutical sales and territory performance.
# BioVanguard Life Sciences Commercial Analytics

## 📌 Project Overview

The **BioVanguard Life Sciences Commercial Analytics** project implements an end-to-end data engineering and analytics solution using Databricks and the Lakehouse architecture.

The project transforms pharmaceutical commercial data into a structured, reliable, and analytics-ready data warehouse. It enables business users to analyze prescription activity, pharmaceutical sales, healthcare providers, healthcare organizations, products, sales representatives, and territory performance through interactive dashboards.

## 🎯 Business Problem

BioVanguard Therapeutics faced challenges managing commercial data distributed across multiple source files.

The major challenges included:

- **Fragmented data:** Prescription, healthcare provider (HCP), healthcare organization (HCO), product, and sales representative data were maintained separately.
- **Territory history:** Sales representative territory changes could cause historical sales to be attributed to the wrong territory.
- **Inconsistent revenue calculations:** Gross sales, rebates, and net sales required consistent business definitions.
- **Incremental loading:** Reprocessing data could introduce duplicate records without proper load controls.
- **Limited business visibility:** Leadership needed a unified dashboard to monitor sales, prescriptions, products, channels, and territories.

## 💡 Project Objectives

- Build a structured commercial data warehouse using Databricks.
- Implement the Bronze, Silver, and Gold Medallion Architecture.
- Clean, standardize, and validate source data.
- Implement Slowly Changing Dimension Type 2 (SCD Type 2) to preserve territory history.
- Implement incremental and idempotent fact loading.
- Create a dimensional model with five dimensions and one fact table.
- Develop reusable Gold-layer analytics views.
- Build interactive dashboards for commercial business analysis.
- Validate data quality and support reliable reporting.

## 🛠️ Technology Stack

- **Platform:** Databricks
- **Data Processing:** Python, PySpark
- **Query Language:** SQL
- **Storage Format:** Delta Lake
- **Governance:** Unity Catalog
- **Architecture:** Medallion Architecture
- **Data Modeling:** Dimensional Modeling / Star Schema
- **Historical Tracking:** SCD Type 2
- **Incremental Processing:** Delta Lake MERGE
- **Orchestration:** Databricks Lakeflow Jobs
- **Visualization:** Databricks AI/BI Dashboards
- **Compute:** Databricks Serverless Compute

## 🏗️ Architecture

The project follows the Medallion Architecture.

### 1. Bronze Layer — Raw Data

The Bronze layer stores the ingested source data.

Responsibilities:
- Ingest source files.
- Preserve source data for downstream processing.
- Provide the initial landing layer for the pipeline.

### 2. Silver Layer — Cleaned and Validated Data

The Silver layer standardizes and prepares data for analytics.

Responsibilities:
- Clean and standardize source records.
- Validate data quality.
- Check for duplicate records and invalid values.
- Prepare business entities for dimensional modeling.
- Support the preparation of historical dimension records.

### 3. Gold Layer — Business-Ready Data

The Gold layer provides the dimensional warehouse and analytics-ready datasets.

**Dimension tables:**
- `dim_date`
- `dim_hcp`
- `dim_hco`
- `dim_product`
- `dim_sales_rep`

**Fact table:**
- `fact_daily_commercial_sales`

**Supporting tables:**
- `stg_fact_daily_commercial_sales`
- `etl_load_control`

The fact table captures commercial activity at the documented grain of date, HCP, HCO, product, sales representative, and channel.

## 🔄 Key Data Engineering Implementations

### Slowly Changing Dimension Type 2

SCD Type 2 preserves historical changes in sales representative attributes, including territory assignments.

This allows historical commercial activity to be analyzed using the appropriate territory history instead of automatically assigning all historical sales to the representative's current territory.

### Incremental Data Loading

Incremental processing loads new fact records while avoiding duplicate inserts when the same business keys are processed again.

The pipeline uses Delta Lake `MERGE` with insert-only behavior for unmatched fact business keys.

### Control Table

The `etl_load_control` table supports tracking and controlling data loads.

It provides a foundation for monitoring load execution and maintaining an auditable incremental-processing workflow.

### Data Quality Validation

Data quality checks help verify the reliability of the processed data.

Examples include:
- Row count validation.
- Random record verification.
- Column-level validation.
- Duplicate record checks.
- Stratification checks.
- Referential integrity checks.

## 📊 Business Metrics

The solution supports analysis of:

- Total prescriptions (TRx).
- New prescriptions (NRx).
- Units dispensed.
- Gross sales.
- Rebates.
- Net sales.
- Product performance.
- Sales channel performance.
- Healthcare provider and healthcare organization activity.
- Sales representative and territory performance.
- Historical territory changes.
- Data quality indicators.

### Business Calculation Definitions

- **Gross Sales** = Units Dispensed × WAC Price
- **Rebate Amount** = Gross Sales × Rebate Percentage
- **Net Sales** = Gross Sales − Rebate Amount

Actual results depend on the source data and the business definitions implemented in the project.

## 📈 Dashboard

The interactive commercial analytics dashboard is organized into four pages.

### 1. Executive Overview
Provides a high-level view of commercial performance, including prescription and sales KPIs.

### 2. Product & Channel
Supports comparisons across pharmaceutical products and commercial channels.

### 3. Providers & Territory
Supports analysis of healthcare providers, healthcare organizations, sales representatives, and territories.

### 4. Territory History & Data Quality
Supports historical territory analysis and visibility into selected data quality checks.

## 🗂️ Data Warehouse Design

The Gold layer follows a dimensional modeling approach.

The five dimensions provide descriptive context for commercial activity, while the fact table stores measurable business activity.

This structure supports analytical queries across dates, healthcare providers, healthcare organizations, products, representatives, and channels.

## 🚀 Expected Business Benefits

- Centralized commercial reporting.
- Consistent sales and prescription metrics.
- Improved visibility into product and channel performance.
- Historical territory analysis.
- Reduced risk of duplicate fact records during repeated incremental loads.
- Better data quality visibility.
- Faster access to business-ready analytics.
- Improved support for commercial decision-making.

## 📁 Repository Contents

Organize the repository to reflect the actual files you upload. A suggested structure is:

```text
biovanguard-life-sciences-commercial-analytics/
│
├── README.md
├── notebooks/
│   ├── bronze_ingestion
│   ├── silver_transformation
│   ├── gold_dimensions
│   ├── scd_type_2
│   ├── incremental_fact_load
│   └── data_quality_validation
│
├── sql/
│   ├── dimension_tables.sql
│   ├── fact_table.sql
│   └── analytics_views.sql
│
├── dashboard/
│   └── dashboard_screenshots/
│
└── docs/
    └── project_documentation
```

*Note: This is a suggested folder structure. Keep only the files and folders that actually exist in your repository.*

## 👩‍💻 Skills Demonstrated

- Data Engineering
- Databricks
- Python and PySpark
- SQL
- Delta Lake
- Medallion Architecture
- Dimensional Data Modeling
- SCD Type 2
- Incremental Data Processing
- Data Quality Testing
- ETL/ELT Pipeline Design
- Data Warehouse Development
- Data Visualization
- Pharmaceutical Commercial Analytics

## ⚠️ Disclaimer

This is a fictional pharmaceutical commercial analytics case study for learning and demonstration purposes. The business, products, and commercial data should not be interpreted as real pharmaceutical sales or clinical evidence.

## 🏁 Conclusion

The BioVanguard project demonstrates how a modern Databricks Lakehouse can transform fragmented pharmaceutical commercial data into a structured data warehouse and interactive analytics solution.

By combining data ingestion, transformation, historical tracking, incremental loading, validation, dimensional modeling, and dashboard reporting, the project establishes a foundation for reliable commercial performance analysis.
