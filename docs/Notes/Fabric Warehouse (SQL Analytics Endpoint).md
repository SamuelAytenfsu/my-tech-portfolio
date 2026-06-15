# Fabric Warehouse
A serverless T-SQL analytics experience in Microsoft Fabric. The SQL Analytics Endpoint provides read-only T-SQL access to Lakehouse Delta tables; the Fabric Warehouse provides full read/write T-SQL with cross-database queries.
## Cross-Database Query
```sql
-- Query across Lakehouse and Warehouse in same workspace
SELECT
    s.order_id,
    s.revenue,
    c.customer_segment
FROM SalesLakehouse.dbo.gold_sales AS s
INNER JOIN AnalyticsWarehouse.dbo.dim_customer AS c
    ON s.customer_id = c.customer_id
WHERE s.order_date >= '2024-01-01';
```

## Warehouse vs SQL Analytics Endpoint
| | Warehouse | SQL Analytics Endpoint |
|---|---|---|
| Access | Read + Write | Read-only |
| DDL Support | Yes (CREATE TABLE) | No |
| Source | Warehouse tables | Lakehouse Delta files |
| Primary use | BI + serving layer | Ad-hoc Lakehouse queries |

## Row-Level Security
```sql
CREATE SECURITY POLICY SalesRegionPolicy
ADD FILTER PREDICATE dbo.fn_SecurityPredicate(region)
ON dbo.gold_sales
WITH (STATE = ON);
```