-- 033. Find top 10 most CPU utilizing Queries - SQL Server Script

--Query 1 
SELECT TOP 10
	deqs.execution_count AS TotalExecutionTime
	,OBJECT_NAME(objectid) AS ObjectName
	,QueryText = SUBSTRING(
		dest.text,
		deqs.statement_start_offset/2,         
		(CASE WHEN deqs.statement_end_offset = -1 
			THEN len(CONVERT(nvarchar(MAX), dest.text)) * 2 
			ELSE deqs.statement_end_offset 
			END - deqs.statement_start_offset)/2)	
	,DatabaseName = db_name(dest.dbid) 
FROM sys.dm_exec_query_stats AS deqs
CROSS APPLY sys.dm_exec_sql_text(deqs.sql_handle) AS dest
--where db_name(dest.dbid) ='YOUR_DATABASE_NAME'
ORDER BY deqs.execution_count DESC
GO

--Query 2
---------********* Most expensive queries starts****** ------------
SELECT TOP 10 SUBSTRING(qt.TEXT, (qs.statement_start_offset/2)+1,
((CASE qs.statement_end_offset
WHEN -1 THEN DATALENGTH(qt.TEXT)
ELSE qs.statement_end_offset
END - qs.statement_start_offset)/2)+1),
qs.execution_count,
qs.total_logical_reads, qs.last_logical_reads,
qs.total_logical_writes, qs.last_logical_writes,
qs.total_worker_time,
qs.last_worker_time,
qs.total_elapsed_time/1000000 total_elapsed_time_in_S,
qs.last_elapsed_time/1000000 last_elapsed_time_in_S,
qs.last_execution_time,
qp.query_plan
FROM sys.dm_exec_query_stats qs
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) qt
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle) qp
ORDER BY qs.total_logical_reads DESC -- logical reads
-- ORDER BY qs.total_logical_writes DESC -- logical writes
-- ORDER BY qs.total_worker_time DESC -- CPU time
---------********* Most expensive queries Ends****** ------------
