--sys.dm_exec_function_stats which returns the aggregate performance statistics for cached functions, which is similar to sys.dm_exec_query_stats and it returns information about scalar functions, In-Memory functions and CLR functions.

SELECT TOP 30
	d.object_id
	,d.database_id
	,OBJECT_NAME(object_id, database_id) AS FunctionName
	,d.cached_time
	,d.last_execution_time
	,d.total_elapsed_time
	,d.total_elapsed_time/d.execution_count AS [avg_elapsed_time]
	,d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_function_stats AS d  
ORDER BY [total_worker_time] DESC; 
