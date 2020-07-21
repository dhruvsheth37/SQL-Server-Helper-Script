-- 052. Check Newly Allocated Pages to the Table - SQL Server Script

SELECT 
	OBJECT_NAME(p.object_id) AS object_name
	,i.name AS index_name
	,ps.in_row_used_page_count
FROM sys.dm_db_partition_stats ps
JOIN sys.partitions p
       ON ps.partition_id = p.partition_id
JOIN sys.indexes i
       ON p.index_id = i.index_id
       AND p.object_id = i.object_id
