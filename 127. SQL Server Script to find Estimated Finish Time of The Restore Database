-- 127. SQL Server Script to find Estimated Finish Time of The Restore Database 
 
SELECT 
	session_id
	,percent_complete AS CompletedPercent
	,DATEADD(MILLISECOND,estimated_completion_time,CURRENT_TIMESTAMP) AS EstimatedFinishTime
	,(total_elapsed_time/1000)/60 AS TotalElapsedTimeInMIN
	,DB_NAME(Database_id) AS DatabaseName 
	,command
	,sql_handle
FROM sys.dm_exec_requests 
