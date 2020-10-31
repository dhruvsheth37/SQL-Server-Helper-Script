-- 120. SQL Server Script to find last statement executed by a SPID using sys.dm_exec_input_buffer

SELECT
	der.session_id
	,ib.event_info AS QueryText
FROM sys.dm_exec_requests AS der
JOIN sys.dm_exec_sessions AS des 
	ON des.session_id = der.session_id
CROSS APPLY sys.dm_exec_input_buffer(der.session_id, der.request_id) AS ib
WHERE
	des.is_user_process = 1
GO
