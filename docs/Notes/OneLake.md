# OneLake
The single, tenant-wide data lake underlying all Microsoft Fabric workloads. All Fabric items (Lakehouses, Warehouses, Eventhouses) store data in OneLake using Delta Parquet format, accessible via ABFS (Azure Blob File System) protocol.
## Access Paths
```python
# ABFS path format
abfss://<workspace_id>@onelake.dfs.fabric.microsoft.com/<lakehouse_id>/Tables/<table>

# Example in PySpark
df = spark.read.format("delta").load(
    "abfss://myworkspace@onelake.dfs.fabric.microsoft.com/SalesLH.Lakehouse/Tables/gold_sales"
)
```

## Shortcuts
OneLake Shortcuts create virtual mounts to external storage without moving data:
```
Supported Sources:
  - ADLS Gen2
  - Azure Blob Storage
  - Amazon S3
  - Google Cloud Storage
  - Another OneLake workspace
```

## OneLake Explorer (Windows)
Mount OneLake as a local drive and browse Lakehouse tables like a file system.