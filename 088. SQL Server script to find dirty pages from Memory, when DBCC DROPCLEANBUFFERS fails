--******** 088. SQL Server script to find dirty pages from Memory, when DBCC DROPCLEANBUFFERS fails 
--Dirty pages mean has not written to disk and Clean pages say the page is brought in to memory by the buffer manager.
--Reference : https://www.sqlskills.com/

SELECT 
    DatabaseName
	,DirtyPageCount
	,CleanPageCount
	,[DirtyPageCount] * 8 / 1024 AS DirtyPageInMB
    ,[CleanPageCount] * 8 / 1024 AS CleanPageInMB
FROM
    (SELECT
        (CASE WHEN ([database_id] = 32767)
            THEN N'Resource Database'
            ELSE DB_NAME ([database_id]) END) AS [DatabaseName],
        SUM (CASE WHEN ([is_modified] = 1)
            THEN 1 ELSE 0 END) AS [DirtyPageCount],
        SUM (CASE WHEN ([is_modified] = 1)
            THEN 0 ELSE 1 END) AS [CleanPageCount]
FROM sys.dm_os_buffer_descriptors
GROUP BY [database_id]) AS [buffers]
ORDER BY [DatabaseName]
GO
