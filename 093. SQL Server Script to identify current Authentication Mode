--********* 093. SQL Server Script to identify current Authentication Mode
Use Master
GO
 
SELECT 
	CASE SERVERPROPERTY('IsIntegratedSecurityOnly')
	WHEN 0 THEN 'Mixed Mode - Authentication Mode (Both SQL Server and Windows Authentication)'
	WHEN 1 THEN 'Only Windows Authentication Mode.' 
END AS SQL_Server_Authentication_Mode
GO
