-- 103. SQL Server Script to find top 10 Stored Procedure which are utilizing more CPU

SELECT TOP 10
    DB_NAME(database_id) AS DatabaseName
    ,OBJECT_SCHEMA_NAME(object_id,database_id) AS SchemaName
    ,OBJECT_NAME(object_id,database_id)AS ObjectName
    ,cached_time AS CachedTime
    ,last_execution_time AS LastExecutionTime
    ,execution_count AS TotalNumberOfExecution
    ,(total_worker_time / execution_count) AS AverageCPUTime
    ,(total_elapsed_time / execution_count) AS AverageElapsedTime
    ,(total_logical_reads / execution_count) AS AverageLogicalReads
    ,(total_logical_writes / execution_count) AS AverageLogicalWrites
    ,(total_physical_reads / execution_count) AS AveragePhysicalReads
FROM sys.dm_exec_procedure_stats 
ORDER BY AverageLogicalReads DESC
