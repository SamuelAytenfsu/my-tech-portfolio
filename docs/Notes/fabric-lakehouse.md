# Fabric Lakehouse Architecture
A unified analytics platform in Microsoft Fabric that combines the flexibility of a data lake with the structure of a data warehouse. Data is stored as Delta Parquet files in OneLake with Bronze/Silver/Gold medallion layers.
## The Medallion Pattern
A robust framework for data organization:
* **Bronze (Raw):** Landing zone, ingested via Data Factory. No transformations applied.
* **Silver (Cleansed):** Data quality checks, deduplication, and schema enforcement (PySpark).
* **Gold (Curated):** Business-ready data modeled as Star Schemas for Power BI.

## Key Performance Strategy
* **Direct Lake Mode:** The game changer. Eliminates import latency by querying Parquet files directly in the Lakehouse.
* **Optimization:** Always partition by `Date` and use V-Order to accelerate engine reads.
# Microsoft Fabric Lakehouse

## Medallion Architecture
```
OneLake/
  ├── Bronze/   # Raw ingested data (no transforms)
  ├── Silver/   # Cleaned, joined, typed
  └── Gold/     # Aggregated, business-ready
```

## PySpark Write Example
```python
df.write.format("delta") \
    .mode("overwrite") \
    .option("overwriteSchema", "true") \
    .save("abfss://workspace@onelake.dfs.fabric.microsoft.com/lakehouse.Lakehouse/Tables/silver_sales")
```

## Key Concepts
- **OneLake:** Single tenant-wide storage layer (like ADLS Gen2)
- **Shortcuts:** Virtual mounts to external data sources
- **Notebooks + Spark:** Primary compute for ELT pipelines