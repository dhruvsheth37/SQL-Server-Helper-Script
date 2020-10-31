-- ****** 084. Script to find the Forwarded Records count of a Table - SQL Server
-- In the below script, you can add a filter of your database and table for getting the number of Forwarding Records. 
SELECT
	OBJECT_NAME(object_id) as TableName
	,index_type_desc
	,page_count
	,avg_page_space_used_in_percent
	,avg_record_size_in_bytes
	,forwarded_record_count
FROM sys.dm_db_index_physical_stats
(
	DB_ID('database_name')
	,OBJECT_ID('table_name')
	,NULL
	,NULL
	,'DETAILED'
)
GO
