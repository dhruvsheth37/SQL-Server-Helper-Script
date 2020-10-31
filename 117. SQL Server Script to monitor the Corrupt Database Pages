-- 117. SQL Server Script to monitor the Corrupt Database Pages

SELECT 
	SD.NAME AS DatabaseName
	,SP.file_id AS FileID
	,MF.physical_name AS PhysicalFilePath
	,SP.page_id AS PageID
	,CASE 
		WHEN SP.event_type = 1
			THEN '823 error caused by an operating system CRC error or 824 error other than a bad checksum or a torn page'
		WHEN SP.event_type = 2
			THEN 'Bad checksum'
		WHEN SP.event_type = 3
			THEN 'Torn Page'
		WHEN SP.event_type = 4
			THEN 'Restored (The page was restored after it was marked bad)'
		WHEN SP.event_type = 5
			THEN 'Repaired (DBCC repaired the page)'
		WHEN SP.event_type = 7
			THEN 'Deallocated by DBCC'
	END AS EventDescription
	,SP.error_count AS ErrorCount
	,SP.last_update_date AS LastUpdated
FROM msdb.dbo.suspect_pages AS SP
INNER JOIN sys.databases AS SD 
	ON SD.database_id = SP.database_id
INNER JOIN sys.master_files AS MF 
	ON MF.database_id = SP.database_id
		AND MF.file_id = SP.file_id
