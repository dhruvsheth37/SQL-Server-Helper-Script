-- 064. Find a different Server Property - SQL Server Script
 
 
SELECT 
	SERVERPROPERTY('MachineName') AS HostName
	,SERVERPROPERTY('InstanceName') AS InstanceName
	,SERVERPROPERTY('Edition') AS EditionInfo
	,SERVERPROPERTY('ProductLevel') AS ProductType 
	,CASE SERVERPROPERTY('IsClustered') 
		WHEN 1 THEN 'Clustered' 
		ELSE 'StandAlone' 
	END AS SQLServerType
	,@@VERSION AS SQLServerVersion
