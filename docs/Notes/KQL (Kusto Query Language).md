# KQL — Kusto Query Language
A read-optimized query language used in Microsoft Fabric Real-Time Analytics (Eventhouse), Azure Data Explorer, and Log Analytics. Optimized for time-series and log data at scale.
## Basic Pattern
```kql
// Filter → Project → Aggregate
SensorReadings
| where timestamp > ago(1h)
| where plant_id == "Plant-01"
| project timestamp, temperature, vibration
| summarize avg_temp = avg(temperature),
            p95_vibe = percentile(vibration, 95)
    by bin(timestamp, 5m)
| render timechart
```

## Common Operators
| Operator | Purpose |
|---|---|
| `where` | Filter rows |
| `project` | Select/rename columns |
| `summarize` | Aggregate |
| `join` | Combine tables |
| `extend` | Add computed column |
| `bin()` | Time bucketing |

## Use in Fabric Eventhouse
Real-Time Analytics stores streaming data in Kusto tables — KQL replaces SQL for sub-second queries on millions of rows.