--Get all schemas in SQL Server database
SELECT 
    s.name as schema_name, 
    s.schema_id,
    u.name as schema_owner
FROM sys.schemas s
INNER JOIN sys.sysusers u
ON u.uid = s.principal_id
ORDER BY s.name
