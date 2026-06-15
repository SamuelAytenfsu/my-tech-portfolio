# Azure Synapse Analytics
Microsoft's integrated analytics service combining big data (Spark pools), data warehousing (dedicated SQL pools), and data integration (pipelines). Now partially superseded by Microsoft Fabric.
## When to Use vs Fabric
| Scenario | Choose |
|---|---|
| Net-new analytics | Microsoft Fabric |
| Existing Synapse investment | Keep + integrate with Fabric via Mirroring |
| Large dedicated SQL pool | Synapse still preferred |
| Spark + Lakehouse + BI | Fabric |

## External Table (PolyBase)
```sql
CREATE EXTERNAL TABLE dbo.SalesExternal (
    order_id NVARCHAR(50),
    amount DECIMAL(18,2),
    order_date DATE
)
WITH (
    LOCATION = 'gold/sales/',
    DATA_SOURCE = MyADLS,
    FILE_FORMAT = ParquetFormat
);
```

## Synapse Link → Cosmos DB
Enables zero-ETL analytics on operational data — reads Cosmos DB change feed into Synapse Spark pool.