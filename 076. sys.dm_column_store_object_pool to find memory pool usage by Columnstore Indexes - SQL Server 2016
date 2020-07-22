-- 076. sys.dm_column_store_object_pool to find memory pool usage by Columnstore Indexes - SQL Server 2016

-- sys.dm_column_store_object_pool system view for finding the memory pool usage by different types of Columnstore Index objects, which introduced first in SQL Server 2016

-- object_type column have below values:
--1 = COLUMN_SEGMENT
--2 = COLUMN_SEGMENT_PRIMARY_DICTIONARY
--3 = COLUMN_SEGMENT_SECONDARY_DICTIONARY
--4 = COLUMN_SEGMENT_BULKINSERT_DICTIONARY
--5 = COLUMN_SEGMENT_DELETE_BITMAP


SELECT 
	OBJECT_NAME(csop.[object_id]) AS TableName
	,[i].[name] AS IndexName
	,[c].[name] AS ColumnName
	,[csop].[column_id]
	,[csop].[row_group_id]
	,[csop].[object_type_desc]
	,[csop].[access_count]
	,[csop].[memory_used_in_bytes]
	,[csop].[object_load_time]
FROM sys.dm_column_store_object_pool AS csop
LEFT OUTER JOIN sys.index_columns AS ic
	ON [ic].[index_column_id] = [csop].[column_id] 
		AND [ic].[index_id] = [csop].[index_id] 
		AND [ic].[object_id] = [csop].[object_id]
LEFT OUTER JOIN sys.columns AS c
	ON [ic].[object_id] = [c].[object_id] 
		AND [ic].[column_id] = [c].[column_id]
LEFT OUTER JOIN sys.indexes AS i
	ON [i].[object_id] = [csop].[object_id] 
		AND [i].[index_id] = [csop].[index_id]
ORDER BY [csop].[memory_used_in_bytes] DESC
GO
