-- 072. Find CPU usage per Different Objects - SQL Server Script

SELECT 
	DB_NAME(st.dbid) AS DatabaseName
	,OBJECT_SCHEMA_NAME(st.objectid,dbid) AS SchemaName
	,cp.objtype AS ObjectType
	,OBJECT_NAME(st.objectid,dbid) AS Objects
	,MAX(cp.usecounts)AS Total_Execution_count
	,SUM(qs.total_worker_time) AS Total_CPU_Time
	,SUM(qs.total_worker_time) / (max(cp.usecounts) * 1.0) AS Avg_CPU_Time 
FROM sys.dm_exec_cached_plans cp 
INNER JOIN sys.dm_exec_query_stats qs 
	ON cp.plan_handle = qs.plan_handle
CROSS APPLY sys.dm_exec_sql_text(cp.plan_handle) st
WHERE DB_NAME(st.dbid) IS NOT NULL
GROUP BY DB_NAME(st.dbid),OBJECT_SCHEMA_NAME(objectid,st.dbid),cp.objtype,OBJECT_NAME(objectid,st.dbid) 
ORDER BY sum(qs.total_worker_time) desc
