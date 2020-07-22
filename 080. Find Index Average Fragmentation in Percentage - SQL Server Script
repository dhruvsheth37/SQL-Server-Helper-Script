-- 080. Find Index Average Fragmentation in Percentage - SQL Server Script

SELECT object_name(ips.object_id) AS TableName
	,i.name AS IndexName
	,ips.index_type_desc AS IndexType
	,ips.avg_fragmentation_in_percent 
	,ips.fragment_count
	,ips.page_count
FROM sys.dm_db_index_physical_stats (DB_ID(),NULL, NULL, NULL ,NULL) AS ips
INNER JOIN sys.indexes AS i ON ips.OBJECT_ID = i.OBJECT_ID
	AND ips.index_id = i.index_id
 
