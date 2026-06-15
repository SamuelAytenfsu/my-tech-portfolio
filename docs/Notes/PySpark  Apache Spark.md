# PySpark — Common Patterns
A distributed in-memory data processing engine. PySpark is the Python API for Spark. Used in Fabric Notebooks and Databricks for large-scale ETL, ML feature engineering, and data transformation.
## Window Functions
```python
from pyspark.sql.window import Window
from pyspark.sql.functions import row_number, lag, col

w = Window.partitionBy("customer_id").orderBy("order_date")

df = df.withColumn("row_num", row_number().over(w)) \
       .withColumn("prev_order_date", lag("order_date", 1).over(w))
```

## Broadcast Join (small table optimization)
```python
from pyspark.sql.functions import broadcast

df_large.join(broadcast(df_small), on="customer_id", how="left")
```

## Schema Enforcement
```python
from pyspark.sql.types import StructType, StructField, StringType, LongType

schema = StructType([
    StructField("order_id", StringType(), False),
    StructField("amount", LongType(), True)
])
df = spark.read.schema(schema).json("/Bronze/orders/")
```