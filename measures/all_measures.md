# DAX Measures (AllMeasures)

This document lists the key DAX measures used in the Power BI report and explains **what each measure does** and **why it exists**.

---

## 1) Base Measures (Core KPIs)

These are the foundational measures used across visuals and as building blocks for other calculations.

### AvgofSales
**Purpose:** Average sales value in the current filter context.
```DAX
AvgofSales = AVERAGE( FactSales[Sales] )
```

### AvgofProfit
**Purpose:** Average profit value in the current filter context.
```DAX
AvgofProfit = AVERAGE( FactSales[Profit] )
```

### SumofSales
**Purpose:** Total sales in the current filter context.
```DAX
SumofSales = SUM( FactSales[Sales] )
```

### SumofProfit
**Purpose:** Total profit in the current filter context.
```DAX
SumofProfit = SUM( FactSales[Profit] )
```

---

## 2) Filtered Measures (Specific Business Conditions)

### SumofSales2013
**Purpose:** Total sales for the year **2013**.
```DAX
SumofSales2013 =
CALCULATE(
    SUM( FactSales[Sales] ),
    DimDate[Year] = 2013
)
```

### SumofSalesLow
**Purpose:** Total sales for the **Low** discount band.
```DAX
SumofSalesLow =
CALCULATE(
    SUM( FactSales[Sales] ),
    DimDiscountBand[DiscountBand] = "Low"
)
```

### SumofSalesLow2013
**Purpose:** Total sales for **Low** discount band in **2013**.
```DAX
SumofSalesLow2013 =
CALCULATE(
    SUM( FactSales[Sales] ),
    DimDiscountBand[DiscountBand] = "Low",
    DimDate[Year] = 2013
)
```

---

## 3) Time Intelligence Measures (YoY & YTD)

### SumofSalesSPLY
**Purpose:** Sales for the **Same Period Last Year (SPLY)**.
```DAX
SumofSalesSPLY =
CALCULATE(
    SUM( FactSales[Sales] ),
    SAMEPERIODLASTYEAR( DimDate[Date] )
)
```

### SumofSalesSPLYPer
**Purpose:** Ratio of current sales to last year's sales.
```DAX
SumofSalesSPLYPer =
DIVIDE(
    [SumofSales],
    [SumofSalesSPLY],
    BLANK()
)
```

### SumofSalesYTD
**Purpose:** Year-to-date cumulative sales.
```DAX
SumofSalesYTD =
CALCULATE(
    SUM( FactSales[Sales] ),
    DATESYTD( DimDate[Date] )
)
```

### SumofSalesYTDSPLY
**Purpose:** Last year's YTD sales for comparison.
```DAX
SumofSalesYTDSPLY =
CALCULATE(
    [SumofSalesYTD],
    SAMEPERIODLASTYEAR( DimDate[Date] )
)
```

---

## Notes
- All measures respect the current report filter context unless explicitly overridden.
- Time intelligence measures require a properly configured date table (`DimDate`).
