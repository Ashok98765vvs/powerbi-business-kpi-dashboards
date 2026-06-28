# Power BI Reports

This folder contains metadata and documentation for each Power BI report in this project.

---

## Report Inventory

### 1. Executive Revenue Dashboard
- **File:** `Executive_Revenue_Dashboard.pbix`
- **Purpose:** High-level revenue performance for C-suite and VP-level stakeholders
- **Refresh:** Daily at 6:00 AM EST via Power BI Service scheduled refresh
- **Data Sources:** Azure Synapse Analytics, Snowflake (PROD_DB.ANALYTICS)
- **Key Pages:**
  - Revenue Overview (MoM, YoY, YTD)
  - Product Mix Analysis
  - Regional Breakdown
- **Key Measures:** Total Revenue, Revenue MoM Growth %, Revenue YTD

---

### 2. Customer Retention KPI Dashboard
- **File:** `Customer_Retention_KPIs.pbix`
- **Purpose:** Track customer churn, retention, and lifetime value
- **Refresh:** Weekly on Monday 7:00 AM EST
- **Data Sources:** Snowflake (PROD_DB.CUSTOMER), CRM export via ADF pipeline
- **Key Pages:**
  - Retention Cohort Analysis
  - Churn Risk Segments
  - Customer LTV Trends
- **Key Measures:** Active Customers, Customer Retention Rate, Avg Deal Size

---

### 3. Operations & Pipeline Dashboard
- **File:** `Operations_Pipeline_Dashboard.pbix`
- **Purpose:** Sales pipeline health, deal conversion, and operational efficiency
- **Refresh:** Daily at 7:30 AM EST
- **Data Sources:** Snowflake (PROD_DB.SALES), Salesforce API via ADF
- **Key Pages:**
  - Pipeline Funnel
  - Win/Loss Analysis
  - Rep Performance
- **Key Measures:** Pipeline Conversion Rate, Avg Deal Size, Open Pipeline Value

---

## Data Model Notes

- All reports use a shared **Date dimension table** (`DimDate`) with fiscal year support
- Relationships follow a **star schema** pattern
- Row-Level Security (RLS) is applied on the `Region` dimension for regional managers
- All monetary values in **USD**
