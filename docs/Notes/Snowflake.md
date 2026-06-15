# Snowflake
A cloud-native data platform with separated compute and storage. Features virtual warehouses (elastic compute clusters), zero-copy cloning, Snowpark (Python/Java/Scala on Snowflake), and time travel.
## Virtual Warehouse & Cost Control
```sql
-- Auto-suspend after 5 min idle
CREATE WAREHOUSE analytics_wh
    WAREHOUSE_SIZE = 'MEDIUM'
    AUTO_SUSPEND = 300
    AUTO_RESUME = TRUE;

-- Use resource monitor to cap spend
CREATE RESOURCE MONITOR monthly_cap
    WITH CREDIT_QUOTA = 500
    TRIGGERS ON 90 PERCENT DO NOTIFY
             ON 100 PERCENT DO SUSPEND;
```

## Snowpark Python
```python
from snowflake.snowpark.session import Session
from snowflake.snowpark.functions import col, sum as sum_

session = Session.builder.configs(connection_params).create()

df = session.table("GOLD.SALES") \
    .filter(col("REGION") == "EMEA") \
    .group_by("PRODUCT") \
    .agg(sum_("REVENUE").alias("TOTAL_REV"))

df.write.mode("overwrite").save_as_table("ANALYTICS.EMEA_REVENUE")
```