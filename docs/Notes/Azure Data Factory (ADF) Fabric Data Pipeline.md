# ADF / Fabric Data Pipeline
A cloud ETL/ELT orchestration service for moving and transforming data across sources. In Microsoft Fabric, Data Pipelines use the same ADF runtime but run natively inside Fabric workspaces.
## Common Pattern: Incremental Load
```json
{
  "activities": [
    {
      "name": "LookupLastWatermark",
      "type": "Lookup",
      "source": { "type": "AzureSqlSource",
        "sqlReaderQuery": "SELECT MAX(modified_date) FROM watermark_table" }
    },
    {
      "name": "CopyNewRows",
      "type": "Copy",
      "dependsOn": [{"activity": "LookupLastWatermark"}],
      "inputs": [{ "type": "AzureSqlTable" }],
      "outputs": [{ "type": "Parquet", "location": "Bronze/" }]
    }
  ]
}
```

## Fabric Pipeline vs ADF
| | ADF | Fabric Pipeline |
|---|---|---|
| Runtime | Azure IR | Same (Fabric-hosted) |
| Integration | ARM-deployed | Workspace item |
| Cost model | Pay per run | Fabric capacity |