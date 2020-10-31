--************** 083. SQL Server 2014: Monitor Memory Optimized Tables which stored in Memory
--SQL Server 2014 introduced the concept of In-Memory Database which provides the best combination of RDBMS + In-Memory Database.
--SQL DBA is monitoring the size of tables, indexes and other fragmentation related information.
--When we say that SQL Server tables stored in memory, we should also keep our eyes open on the utilization of memory.
--SQL Server 2014 also introduced one DMV (sys.dm_db_xtp_table_memory_stats) to check the memory utilization of Memory Optimized Tables.
--Using this view, you can find memory information like allocated memory and used memory for tables and indexes.

 
SELECT  
	OBJECT_ID 
	,OBJECT_SCHEMA_NAME(object_id) + '.' + OBJECT_NAME(object_id) AS TableName
	,memory_allocated_for_table_kb 
	,memory_used_by_table_kb 
	,memory_allocated_for_indexes_kb 
	,memory_used_by_indexes_kb
FROM sys.dm_db_xtp_table_memory_stats
GO
