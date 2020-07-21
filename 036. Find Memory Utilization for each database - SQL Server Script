-- 036. Find Memory Utilization for each database - SQL Server Script

SELECT
	CASE 
		WHEN database_id = 32767 
			THEN 'Resource DB' 
		ELSE DB_NAME (database_id) 
	END AS DatabaseName
	,COUNT (1) AS Buffer_PageCount
	,(COUNT (1) * 8)/1024 AS Used_MemoryInMB 	
FROM sys.dm_os_buffer_descriptors
GROUP BY database_id
ORDER BY db_name(database_id)
