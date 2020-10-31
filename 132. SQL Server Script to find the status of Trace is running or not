-- 132. SQL Server Script to find the status of Trace is running or not

SELECT 
	CASE T.is_default
		WHEN 1 THEN 'Default/System Trace'
		WHEN 0 THEN 'User Defined Trace'
	END AS TraceType
	,CASE T.status
		WHEN 1 THEN 'Running'
		WHEN 0 THEN 'Stopped'
	END AS TraceStrace
	,ES.session_id AS SessionID
	,ES.login_name AS LoginName
	,T.Path AS TraceFilePath
FROM sys.traces AS T
LEFT JOIN sys.dm_exec_sessions AS ES
	ON T.reader_spid = ES.session_id
