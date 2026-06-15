# Azure Databricks
A managed Apache Spark platform on Azure co-developed by Databricks and Microsoft. Features Unity Catalog for governance, Delta Live Tables for pipeline orchestration, and MLflow for ML lifecycle management.
## Unity Catalog Namespace
```sql
-- Three-level namespace: catalog.schema.table
SELECT * FROM main.silver.sales
WHERE order_date >= '2024-01-01';

-- Grant permission
GRANT SELECT ON TABLE main.silver.sales TO `analyst@company.com`;
```

## Delta Live Tables (DLT) Pipeline
```python
import dlt
from pyspark.sql.functions import col

@dlt.table(comment="Raw sales from event hub")
def bronze_sales():
    return spark.readStream.format("cloudFiles") \
        .option("cloudFiles.format", "json") \
        .load("/raw/sales/")

@dlt.table
@dlt.expect_or_drop("valid_order", "order_id IS NOT NULL")
def silver_sales():
    return dlt.read_stream("bronze_sales") \
        .withColumn("amount", col("amount").cast("double"))
```