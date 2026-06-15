# Medallion Architecture
A layered data design pattern with Bronze (raw), Silver (cleaned/conformed), and Gold (aggregated/business-ready) layers. Enables incremental data quality improvements while preserving raw source fidelity.
## Layer Responsibilities
| Layer | Data State | Transformations |
|---|---|---|
| Bronze | Raw as-is | None — append only |
| Silver | Cleaned, typed, joined | Dedup, cast, filter nulls |
| Gold | Business metrics | Agg, denorm, semantic model-ready |

## Bronze → Silver PySpark
```python
from pyspark.sql.functions import col, to_timestamp, trim

df_bronze = spark.read.format("delta").load("Bronze/sales_raw")

df_silver = (
    df_bronze
    .dropDuplicates(["order_id"])
    .filter(col("order_id").isNotNull())
    .withColumn("order_date", to_timestamp(col("order_date_str"), "yyyy-MM-dd"))
    .withColumn("customer_name", trim(col("customer_name")))
    .drop("order_date_str")
)

df_silver.write.format("delta").mode("overwrite").save("Silver/sales")