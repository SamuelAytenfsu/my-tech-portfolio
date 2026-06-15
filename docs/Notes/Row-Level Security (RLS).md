# Row-Level Security (RLS)
A data access control pattern that restricts which rows a user can see in a report or query, based on their identity or role. Implemented in Power BI semantic models (DAX USERPRINCIPALNAME) and in SQL-based warehouse tables.
## Power BI DAX Implementation
```dax
-- Define role "Region Manager" with filter on DimRegion:
[Region Email] = USERPRINCIPALNAME()

-- Or map via a security table:
[Region] IN
    CALCULATETABLE(
        VALUES(UserRegionMap[Region]),
        UserRegionMap[Email] = USERPRINCIPALNAME()
    )
```

## Object-Level Security (OLS) — hide tables
```
Via Tabular Editor or TMSL:
{
  "name": "SalaryData",
  "metadataPermission": "None"   // Hidden from role
}
```

## SQL Warehouse RLS
```sql
CREATE FUNCTION dbo.fn_RegionPredicate(@region NVARCHAR(50))
RETURNS TABLE WITH SCHEMABINDING AS
RETURN SELECT 1 AS result
WHERE @region = (SELECT region FROM dbo.UserRegions WHERE email = USER_NAME());

CREATE SECURITY POLICY RegionPolicy
ADD FILTER PREDICATE dbo.fn_RegionPredicate(region)
ON dbo.gold_sales WITH (STATE = ON);
```