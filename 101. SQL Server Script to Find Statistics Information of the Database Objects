-- 101. SQL Server Script to Find Statistics Information of the Database Objects

-- Different 3 ways to Find Statistics Information of the Database Objects

-- 1. Using sys.indexes
SELECT 
    SCHEMA_NAME(SCHEMA_ID) AS SchemaName
    ,OBJECT_NAME(o.OBJECT_ID) AS ObjectName
    ,i.name AS IndexName
    ,STATS_DATE(o.OBJECT_ID,i.index_id) AS StatisticUpdateDate 
FROM sys.indexes AS i 
JOIN sys.objects AS o 
	ON i.object_id = o.object_id 
WHERE o.object_id > 100 AND index_id > 0 
  AND is_ms_shipped = 0
GO

-- 2. Using DBCC
DBCC SHOW_STATISTICS ('Table_Name', 'Index_Name') 
GO


-- 3. Using sys.stats
SELECT 
	OBJECT_NAME(object_id) AS ObjectName
	,name AS StatisticName
	,STATS_DATE(object_id, stats_id) AS StatisticUpdateDate	
FROM sys.stats;
GO
