# DAX — Key Patterns
A formula language for creating calculated columns, measures, and tables in Power BI and Analysis Services. Uses a functional, context-aware evaluation model (row context vs. filter context).
## Time Intelligence
```dax
-- Month-to-date
Revenue MTD =
TOTALMTD([Total Revenue], DimDate[Date])

-- Prior year comparison
Revenue PY =
CALCULATE(
    [Total Revenue],
    SAMEPERIODLASTYEAR(DimDate[Date])
)

-- YoY Growth %
Revenue YoY % =
DIVIDE([Total Revenue] - [Revenue PY], [Revenue PY], 0)
```

## Context Transition (CALCULATE)
```dax
-- Filter context: show only North region regardless of slicer
North Revenue =
CALCULATE(
    [Total Revenue],
    DimRegion[Region] = "North"
)

-- ALLEXCEPT: remove all filters except one column
Market Share =
DIVIDE(
    [Total Revenue],
    CALCULATE([Total Revenue], ALLEXCEPT(DimProduct, DimProduct[Category]))
)
```