--038. Generate Shrink Script for each Database File - SQL Server Script

SELECT 
	'USE ' + db_name(dbid) + char(13) + 'DBCC SHRINKFILE (N' + quotename(sf.name,'''') + ' ,truncateonly)' 
FROM sys.sysaltfiles AS sf
INNER JOIN sys.databases d 
	ON sf.dbid = d.database_id
WHERE d.state_desc = 'online'
--AND db_name(dbid) = 'DATABASE_NAME'
