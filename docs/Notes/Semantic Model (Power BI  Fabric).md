# Semantic Model
A metadata layer built on top of tabular data that defines measures, hierarchies, relationships, and business logic using DAX. Formerly called a 'dataset' in Power BI.
## Structure
```
SemanticModel/
  ├── Tables
  │   ├── DimDate
  │   ├── DimCustomer
  │   └── FactSales
  ├── Relationships
  │   └── FactSales[DateKey] → DimDate[DateKey]
  └── Measures
      └── [Total Revenue] = SUMX(FactSales, FactSales[Qty] * FactSales[Price])
```

## DAX Measure Example
```dax
Total Revenue YTD =
TOTALYTD(
    [Total Revenue],
    DimDate[Date]
)
```

## Direct Lake Mode
In Fabric, semantic models can connect directly to Lakehouse Delta tables without import or DirectQuery overhead.