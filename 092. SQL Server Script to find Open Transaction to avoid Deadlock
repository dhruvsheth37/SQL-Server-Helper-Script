-********* 092. SQL Server Script to find Open Transaction to avoid Deadlock

SELECT
	[tst].[session_id] AS SessionID
	,[des].[login_name] AS LoginName
	,DB_NAME (tdt.database_id) AS DatabaseName
	,[tdt].[database_transaction_begin_time] AS TransactionBeginTime
	,[tdt].[database_transaction_log_bytes_used] AS LogBytesUsed    
	,[mrsh].text AS QueryText
	,[ph].[query_plan] AS QueryPlan
FROM sys.dm_tran_database_transactions [tdt]
JOIN sys.dm_tran_session_transactions [tst]
	ON [tst].[transaction_id] = [tdt].[transaction_id]
JOIN sys.[dm_exec_sessions] [des]
	ON [des].[session_id] = [tst].[session_id]
JOIN sys.dm_exec_connections [dec]
	ON [dec].[session_id] = [tst].[session_id]
LEFT OUTER JOIN sys.dm_exec_requests [der]
	ON [der].[session_id] = [tst].[session_id]
CROSS APPLY sys.dm_exec_sql_text ([dec].[most_recent_sql_handle]) AS [mrsh]
OUTER APPLY sys.dm_exec_query_plan ([der].[plan_handle]) AS [ph]
ORDER BY [TransactionBeginTime] ASC
GO
