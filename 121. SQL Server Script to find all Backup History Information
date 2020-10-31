-- 121. SQL Server Script to find all Backup History Information

SELECT 
	bs.database_name AS DatabaseName
	,CASE bs.type
		WHEN 'D' THEN 'Full'
		WHEN 'I' THEN 'Differential'
		WHEN 'L' THEN 'Transaction Log'
	END AS BackupType
	,CAST(DATEDIFF
		(SECOND,bs.backup_start_date,bs.backup_finish_date) 
		AS VARCHAR(4)) + ' ' + 'Seconds' AS TotalTimeTaken
	,bs.backup_start_date AS BackupStartDate
	,CAST(bs.first_lsn AS VARCHAR(50)) AS FirstLSN
	,CAST(bs.last_lsn AS VARCHAR(50)) AS LastLSN
	,bmf.physical_device_name AS PhysicalDeviceName
	,CAST(CAST(bs.backup_size / 1000000 AS INT) AS VARCHAR(14)) 
		+ ' ' + 'MB' AS BackupSize
	,bs.server_name AS ServerName
	,bs.recovery_model AS RecoveryModel
FROM msdb.dbo.backupset AS bs
INNER JOIN msdb.dbo.backupmediafamily AS bmf
	ON bs.media_set_id = bmf.media_set_id
WHERE bs.database_name = 'Your_Database_Name'
ORDER BY 
	backup_start_date DESC
	,backup_finish_date
