-- Check If Mirroring enable for Database Script - SQL Server

SELECT
	d.name as DatabaseName
	,CASE
		WHEN dm.mirroring_state is NULL THEN 'Mirroring is not configured'
		ELSE 'Mirroring is configured'
	END as MirroringStatus
FROM sys.databases d
INNER JOIN sys.database_mirroring dm
	ON d.database_id=dm.database_id
