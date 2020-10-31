-- 100. SQL Server script to find auto created Statistics Objects

SELECT 
	OBJECT_NAME(s.object_id) AS ObjectName
	,COL_NAME(sc.object_id, sc.column_id) AS ColumnName
	,s.name AS StatisticsName
	,STATS_DATE(s.OBJECT_ID,s.stats_id) AS StatisticUpdateDate 
FROM sys.stats AS s 
JOIN sys.stats_columns AS sc
    ON s.stats_id = sc.stats_id 
       AND s.object_id = sc.object_id
WHERE s.name like '_WA%'
ORDER BY s.name;
