# Dataverse
Microsoft's low-code data platform underlying Power Apps and Dynamics 365. Stores data as tables with built-in relationships, business rules, and security roles. Can be linked to Fabric via Azure Synapse Link for analytics.
## Fabric Integration via Synapse Link
```
Dataverse Tables (operational)
        │
  Azure Synapse Link
        │
  OneLake (Delta format)  ← zero-ETL
        │
  Fabric Lakehouse Shortcut
        │
  Power BI Direct Lake
```

## Query via Fabric SQL Endpoint
```sql
-- After Synapse Link setup, Dataverse tables appear as Delta tables
SELECT
    accountid,
    name AS account_name,
    revenue AS annual_revenue,
    modifiedon
FROM dbo.account
WHERE statecode = 0  -- Active records only
ORDER BY modifiedon DESC;
```

## Key Dataverse Concepts
| Concept | Description |
|---|---|
| Table | Entity (like Account, Contact) |
| Column | Field with type enforcement |
| Relationship | Lookup / Many-to-many |
| Business rule | No-code validation logic |
| Security role | Row + column level permissions |