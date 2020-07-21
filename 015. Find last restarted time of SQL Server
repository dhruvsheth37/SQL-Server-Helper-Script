-- 015. Find last restarted time of SQL Server

--Using sys.dm_exec_sessions: 
SELECT login_time FROM sys.dm_exec_sessions WHERE session_id = 1
GO


--Using sys.dm_os_sys_info:
SELECT sqlserver_start_time FROM sys.dm_os_sys_info
GO 

--Using sys.databases:
SELECT create_date FROM sys.databases WHERE name = 'tempdb' 
GO

--Using sys.traces:
SELECT start_time FROM sys.traces WHERE is_default = 1  
GO

--Using sysdatabases:
SELECT crdate FROM sysdatabases WHERE name='tempdb'  
GO
