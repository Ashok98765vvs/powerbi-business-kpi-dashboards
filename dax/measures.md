# DAX Measures Reference

This document lists all custom DAX measures used across the Power BI KPI dashboards.

---

## Revenue Metrics

### Total Revenue
```dax
Total Revenue =
CALCULATEX(
    SUMMARIZE(
        Sales,
        Sales[ProductKey],
        "Revenue", SUMX(Sales, Sales[Quantity] * Sales[UnitPrice])
    ),
    [Revenue]
)
```

### Revenue MoM Growth %
```dax
Revenue MoM Growth % =
VAR CurrentMonth = [Total Revenue]
VAR PriorMonth =
    CALCULATE(
        [Total Revenue],
        DATEADD('Date'[Date], -1, MONTH)
    )
RETURN
    DIVIDE(CurrentMonth - PriorMonth, PriorMonth, 0)
```

### Revenue YTD
```dax
Revenue YTD =
CALCULATE(
    [Total Revenue],
    DATESYTD('Date'[Date])
)
```

---

## Customer Metrics

### Active Customers
```dax
Active Customers =
DISTINCTCOUNT(Sales[CustomerID])
```

### Customer Retention Rate
```dax
Customer Retention Rate =
VAR RetainedCustomers =
    CALCULATE(
        DISTINCTCOUNT(Sales[CustomerID]),
        FILTER(
            Sales,
            CALCULATE(COUNTROWS(Sales), DATEADD('Date'[Date], -1, MONTH)) > 0
        )
    )
VAR TotalLastMonth =
    CALCULATE(
        DISTINCTCOUNT(Sales[CustomerID]),
        DATEADD('Date'[Date], -1, MONTH)
    )
RETURN
    DIVIDE(RetainedCustomers, TotalLastMonth, 0)
```

---

## Operational KPIs

### Average Deal Size
```dax
Avg Deal Size =
DIVIDE([Total Revenue], [Active Customers], 0)
```

### Pipeline Conversion Rate
```dax
Conversion Rate =
DIVIDE(
    CALCULATE(COUNTROWS(Deals), Deals[Status] = "Won"),
    COUNTROWS(Deals),
    0
)
```
