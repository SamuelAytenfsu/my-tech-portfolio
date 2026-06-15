# Cost Optimization
Strategies to minimize compute and storage spend: right-sizing Fabric capacity, pausing capacities off-hours, using Spark autoscaling, OPTIMIZE/VACUUM on Delta tables, and monitoring with the Fabric Capacity Metrics app.
## Fabric Capacity — Pause Off-Hours
```powershell
# Azure PowerShell — suspend Fabric capacity nights/weekends
$schedule = @{
    "startTime" = "18:00"
    "endTime" = "08:00"
    "timeZone" = "Eastern Standard Time"
}
Suspend-AzPowerBIEmbeddedCapacity -Name "FabricCapacityProd" -ResourceGroupName "rg-analytics"
```

## Delta Table Maintenance
```sql
-- Compact small files (run weekly)
OPTIMIZE gold_sales ZORDER BY (customer_id, order_date);

-- Remove old snapshots (save storage)
VACUUM gold_sales RETAIN 168 HOURS;  -- 7 days
```

## Spark Optimization
```python
# Avoid wide shuffles — repartition before joins
df = df.repartition(200, "customer_id")

# Cache hot DataFrames
df_dim_customer.cache()
df_dim_customer.count()  # Trigger caching
```