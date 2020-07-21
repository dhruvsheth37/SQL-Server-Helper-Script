 -- 024. Find the Service Account Name Script - SQL Server
DECLARE @ServiceAccountName varchar(50)
EXECUTE master.dbo.xp_instance_regread
	N'HKEY_LOCAL_MACHINE'
	,N'SYSTEM\CurrentControlSet\Services\MSSQLSERVER'
	,N'ObjectName'
	,@ServiceAccountName OUTPUT
	
SELECT @ServiceAccountName AS ServiceAccountName
