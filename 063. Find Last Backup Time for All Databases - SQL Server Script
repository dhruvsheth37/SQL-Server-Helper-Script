-- 063. Find Last Backup Time for All Databases - SQL Server Script  

SELECT 
	D.name	
	,CASE 
	   WHEN MAX(B.backup_finish_date) IS NULL 
		THEN 'Backup not taken' 
		ELSE CONVERT(VARCHAR(100),MAX(B.backup_finish_date)) 
	END AS LastBackupDate
FROM sys.databases AS D
LEFT OUTER JOIN msdb.dbo.backupset AS B 
	ON D.name = B.database_name AND B.type = 'D'
GROUP BY D.name
ORDER BY 2 DESC
