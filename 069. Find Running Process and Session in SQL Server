-- 069. Find Running Process and Session in SQL Server


-- 1) Using SP_WHO
-- Provides information like: Session ID, Logged User ID, Host Name, Session Status, Blocked Process, Database Name, Command Details, Request ID.

SP_WHO 
GO

-- 2) Using SP_WHO2 
-- Provides some additional information like : CPU Time by each session, no of Disk Reads, Last query execution time

SP_WHO2
GO


-- 3) Usign sysprocesses View
 
SELECT 
    DB_NAME(DBID) AS DataBaseName
    ,COUNT(DBID) AS NumberOfConnections
    ,LogiName 
FROM sys.sysprocesses
WHERE DBID > 0
GROUP BY DBID, LogiName
GO


-- 4) Using dm_exec_requests
 
SELECT
	der.session_id
	,est.TEXT AS QueryText
	,der.status
	,der.blocking_session_id
	,der.cpu_time
	,der.total_elapsed_time
FROM sys.dm_exec_requests AS der
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS est
