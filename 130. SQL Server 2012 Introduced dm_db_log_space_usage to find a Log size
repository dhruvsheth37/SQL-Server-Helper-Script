-- 130. SQL Server 2012 Introduced dm_db_log_space_usage to find a Log size

SELECT
	DB_NAME(database_id) AS DatabaseName
	,ROUND(CONVERT(FLOAT,total_log_size_in_bytes/1024)/1024,2) AS LogSizeInMB
	,ROUND(CONVERT(FLOAT,used_log_space_in_bytes/1024)/1024,2) AS LogUsedSizeInMB
	,ROUND(used_log_space_in_percent,2) AS LogUsedPercentInMB
FROM
sys.dm_db_log_space_usage
