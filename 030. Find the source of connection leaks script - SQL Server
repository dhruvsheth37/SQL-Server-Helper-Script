-- 030. Find the source of connection leaks script - SQL Server
-- For further reference refer:  http://blog.sqlgrease.com/find-source-connection-leaks/

SELECT top 100 s.last_request_end_time,
datediff(ss, s.last_request_end_time, getdate()) seconds_since_last_request_ended,
s.session_id, 
c.most_recent_sql_handle,
COALESCE(st.text, N'Statement no longer in cache') statement_text
FROM sys.dm_exec_sessions s
INNER JOIN sys.dm_exec_connections c ON
     s.session_id = c.session_id
OUTER APPLY sys.dm_exec_sql_text(c.most_recent_sql_handle) st
WHERE s.is_user_process=1
  AND s.host_name = 'DATABASE_NAME' 
  AND s.status = 'sleeping'
ORDER BY last_request_end_time
