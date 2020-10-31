-- 133. SQL Server Script to find Installation Date, time and Authentication Mode

SELECT 
	createdate AS InstallationDate 
	,CASE SERVERPROPERTY('IsIntegratedSecurityOnly')   
		WHEN 1 THEN 'Windows Authentication'  
		WHEN 0 THEN 'Windows and SQL Server Authentication'  
	END AS AuthenticationMode
	,SERVERPROPERTY('servername') AS ServerName
FROM master.sys.syslogins 
WHERE name LIKE 'NT AUTHORITY\SYSTEM'
