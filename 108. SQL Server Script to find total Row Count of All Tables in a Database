-- 108. SQL Server Script to find total Row Count of All Tables in a Database
 
SELECT
      QUOTENAME(SCHEMA_NAME(SO.schema_id)) + '.' + QUOTENAME(SO.name) AS TableName
      , SUM(SP.Rows) AS TotalRowCount
FROM sys.objects AS SO
INNER JOIN sys.partitions AS SP
	ON SO.object_id = SP.object_id
WHERE SO.type = 'U'
      AND SO.is_ms_shipped = 0x0
      AND index_id < 2 
GROUP BY 
      SO.schema_id
      ,SO.name
ORDER BY 1
