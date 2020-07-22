-- 077. sys.column_store_row_groups to find information on Columnstore row groups - SQL Server 2014

-- sys.column_store_row_groups system view for finding the information on the Columnstore row groups, which introduced first in SQL Server 2014
-- Using the system view, we can find information regarding number of rows physically stored and the column for number of rows marked as deleted. By using deleted rows, one can decide whether rebuild required or not.

SELECT
	OBJECT_NAME([csrg].[object_id]) AS TableName
	,[i].[name] AS IndexName
	,[csrg].[row_group_id]
	,[csrg].[delta_store_hobt_id]
	,[csrg].[state_description]
	,[csrg].[total_rows]
	,[csrg].[deleted_rows]
	,[csrg].[size_in_bytes]
FROM sys.column_store_row_groups AS csrg
LEFT OUTER JOIN sys.indexes AS i
	ON [csrg].[object_id] = [i].[object_id]
		AND [csrg].[index_id] = [i].[index_id]
ORDER BY [TableName],[IndexName]

GO
