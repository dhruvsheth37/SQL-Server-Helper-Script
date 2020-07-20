-- Find fragmentation of Columnstore Indexes Script - SQL Server 2016

SELECT 
	OBJECT_NAME([i].[object_id]) AS TableName
	,[i].[name] AS IndexName	
	,[csrgps].[state_desc]
	,[csrgps].[total_rows]
	,[csrgps].[deleted_rows]
	,[csrgps].[size_in_bytes]
	,[csrgps].[trim_reason_desc]
	,[csrgps].[transition_to_compressed_state_desc]
	,[csrgps].[has_vertipaq_optimization]	
	,[csrgps].[created_time]
	,[csrgps].[closed_time]
	,100 * (ISNULL(csrgps.[deleted_rows],0)) / total_rows AS 'IsFragmentation'
FROM sys.indexes AS i
INNER JOIN sys.dm_db_column_store_row_group_physical_stats AS csrgps
	ON [i].[object_id] = [csrgps].[object_id] 
		AND [i].index_id = [csrgps].index_id  
ORDER BY [TableName], [IndexName]
