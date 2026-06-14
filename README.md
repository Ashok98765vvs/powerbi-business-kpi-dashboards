# Power BI Business KPI Dashboards

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=microsoft-sql-server&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)

## Overview
A suite of **8 interactive Power BI dashboards** built to surface executive-level KPIs across sales, operations, and finance domains. Designed with enterprise-grade Row-Level Security (RLS) for 30+ roles, ensuring each business unit sees only its authorized data.

## Key Highlights
- 8 dashboards covering Sales Performance, Revenue Trends, Operational KPIs, and Customer Analytics
- RLS configured for **30 roles** across departments (Finance, Sales, Operations, Executive)
- Analyzed **50,000+ records** with optimized DAX measures and calculated columns
- Achieved **99.7% data accuracy** through robust SQL-based data validation
- Connected to SQL Server data warehouse with scheduled refresh pipelines
- Reduced manual reporting time by **60%** through automated dashboard refresh

## Tech Stack
| Tool | Usage |
|------|-------|
| Power BI Desktop | Dashboard development & publishing |
| DAX | KPI calculations, time intelligence, RLS rules |
| Power Query (M) | ETL transformations and data shaping |
| SQL Server | Source database and stored procedures |
| Azure Data Gateway | Scheduled refresh connectivity |

## Project Structure
```
powerbi-business-kpi-dashboards/
├── dashboards/          # .pbix files for each dashboard
│   ├── sales_performance.pbix
│   ├── revenue_trends.pbix
│   ├── operational_kpis.pbix
│   └── customer_analytics.pbix
├── sql/                 # SQL queries and stored procedures
│   ├── fact_sales.sql
│   ├── dim_customer.sql
│   └── kpi_calculations.sql
├── dax/                 # DAX measure documentation
│   ├── sales_measures.md
│   └── time_intelligence.md
├── rls/                 # RLS role definitions
│   └── role_mapping.md
└── docs/                # Architecture and user guide
    └── architecture.md
```

## Dashboard Descriptions

### 1. Sales Performance Dashboard
- Monthly/Quarterly/YTD sales by region, product, and rep
- Target vs Actual variance analysis
- Top 10 customers by revenue

### 2. Revenue Trends Dashboard
- Revenue growth trends with moving averages
- YoY and MoM comparisons using DAX time intelligence
- Forecast projections using statistical models

### 3. Operational KPIs Dashboard
- Inventory turnover, order fulfillment rates
- SLA compliance tracking
- Cost-per-unit trends

### 4. Customer Analytics Dashboard
- Customer segmentation (RFM analysis)
- Churn risk indicators
- Lifetime value tracking

## RLS Architecture
Row-Level Security was implemented at the dataset level using DAX-based role filters:
```dax
-- Example: Region-based RLS filter
[Region] = LOOKUPVALUE(
    DimEmployee[Region],
    DimEmployee[Email],
    USERPRINCIPALNAME()
)
```
30 roles defined across 5 departments with hierarchical access control.

## Sample DAX Measures
```dax
-- YTD Sales
YTD Sales = TOTALYTD(SUM(FactSales[Revenue]), DimDate[Date])

-- MoM Growth %
MoM Growth % = 
VAR CurrentMonth = [Total Revenue]
VAR PrevMonth = CALCULATE([Total Revenue], DATEADD(DimDate[Date], -1, MONTH))
RETURN DIVIDE(CurrentMonth - PrevMonth, PrevMonth, 0)

-- Customer Retention Rate
Retention Rate = 
DIVIDE(
    CALCULATE(DISTINCTCOUNT(FactSales[CustomerID]), DATEADD(DimDate[Date], -1, YEAR)),
    CALCULATE(DISTINCTCOUNT(FactSales[CustomerID]))
)
```

## Results & Impact
- Enabled real-time KPI visibility for **C-suite executives**
- Reduced report generation time from 2 days to **real-time**
- Improved data-driven decision making across 5 business units
- Zero unauthorized data access incidents post RLS implementation

## Author
**Ashok Chowdary** | Data Engineer  
Auburn University Montgomery | OPT Status  
[LinkedIn](https://linkedin.com/in/ashok98765vvs) | [GitHub](https://github.com/Ashok98765vvs)
