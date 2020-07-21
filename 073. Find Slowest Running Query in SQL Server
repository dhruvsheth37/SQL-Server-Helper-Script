-- 073. Find Slowest Running Query in SQL Server
 
SELECT TOP 10 
	SUBSTRING(qt.TEXT, (qs.statement_start_offset/2)+1,
	((CASE qs.statement_end_offset WHEN -1 THEN DATALENGTH(qt.TEXT)
	ELSE qs.statement_end_offset END - qs.statement_start_offset)/2)+1
	) AS Query
	,qp.query_plan
	,qs.execution_count
	,qs.total_logical_reads
	,qs.last_logical_reads
	,qs.total_logical_writes
	,qs.last_logical_writes
	,qs.total_worker_time
	,qs.last_worker_time
	,qs.total_elapsed_time
	,qs.last_elapsed_time
	,qs.last_execution_time	
FROM sys.dm_exec_query_stats qs
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) qt
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle) qp
ORDER BY qs.total_logical_reads DESC
