# Delta Lake
An open-source storage layer on top of Parquet files that adds ACID transactions, schema enforcement, time travel, and CDC (Change Data Capture) capabilities to data lakes.
## Key Features
| Feature | Description |
|---|---|
| ACID | Atomic commits — partial writes never visible |
| Time Travel | Query historical snapshots |
| Schema Enforcement | Rejects bad-schema writes |
| OPTIMIZE/ZORDER | File compaction + data skipping |

## Time Travel Example
```python
# Read as of a specific version
df = spark.read.format("delta") \
    .option("versionAsOf", 5) \
    .load("/Tables/silver_sales")

# Restore table to version
from delta.tables import DeltaTable
dt = DeltaTable.forPath(spark, "/Tables/silver_sales")
dt.restoreToVersion(5)
```

## OPTIMIZE + Z-ORDER
```sql
OPTIMIZE silver_sales
ZORDER BY (customer_id, order_date);
```