# Direct Lake Mode
A Microsoft Fabric semantic model connection mode that reads Delta Parquet files directly from OneLake without importing or using DirectQuery. Delivers near-import speed with always-current data.
## How It Works
```
OneLake Delta Tables
        │
   (no data copy)
        │
 Semantic Model (Direct Lake)
        │
  Power BI Report
```

## Requirements
- Tables must be in Fabric Lakehouse or Warehouse (Delta format)
- No calculated columns in PySpark — do transforms in Lakehouse
- Framing queries auto-run when user opens report (cold cache)

## Fallback Behavior
| Condition | Mode Falls Back To |
|---|---|
| Unsupported DAX function | DirectQuery |
| Row-level security override | DirectQuery |
| Manual fallback | Import (scheduled refresh) |

## Capacity Planning Note
Direct Lake uses Fabric capacity CUs — monitor with Fabric Capacity Metrics app.