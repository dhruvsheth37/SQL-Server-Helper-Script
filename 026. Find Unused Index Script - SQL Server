-- 026. Find Unused Index Script - SQL Server

-- ******* Script - 1 Starts ****** ------
SELECT  
o.name AS ObjectName
, i.name AS IndexName
, i.index_id AS IndexID
, dm_ius.user_seeks AS UserSeek
, dm_ius.user_scans AS UserScans
, dm_ius.user_lookups AS UserLookups
, dm_ius.user_updates AS UserUpdates
, p.TableRows
, au.used_pages AS IndexSizeInBytes
, 'DROP INDEX ' + QUOTENAME(i.name)
+ ' ON ' + QUOTENAME(s.name) + '.'
+ QUOTENAME(OBJECT_NAME(dm_ius.OBJECT_ID)) AS 'drop statement'
FROM sys.dm_db_index_usage_stats dm_ius
INNER JOIN sys.indexes i ON i.index_id = dm_ius.index_id 
AND dm_ius.OBJECT_ID = i.OBJECT_ID
INNER JOIN sys.objects o ON dm_ius.OBJECT_ID = o.OBJECT_ID
INNER JOIN sys.schemas s ON o.schema_id = s.schema_id
INNER JOIN (SELECT SUM(p.rows) TableRows, p.index_id, p.OBJECT_ID,p.partition_id
FROM sys.partitions p GROUP BY p.index_id, p.OBJECT_ID,p.partition_id) p
ON p.index_id = dm_ius.index_id AND dm_ius.OBJECT_ID = p.OBJECT_ID
INNER JOIN sys.allocation_units AS au ON au.container_id = p.partition_id 
WHERE OBJECTPROPERTY(dm_ius.OBJECT_ID,'IsUserTable') = 1
AND dm_ius.database_id = DB_ID()
AND i.type_desc = 'nonclustered'
AND i.is_primary_key = 0 --This line excludes primary key constarint
AND i.is_unique_constraint = 0 --This line excludes unique key constarint
AND dm_ius.user_seeks<5
ORDER BY (dm_ius.user_seeks + dm_ius.user_scans + dm_ius.user_lookups) ASC
-- ******* Script - 1 Ends ****** ------

-- ******* Script - 2 Starts ****** ------

SELECT 'DROP INDEX '+OBJECT_NAME(dm_db_index_usage_stats.object_id)+'.'+indexes.name AS Drop_Index, user_seeks, user_scans, user_lookups, user_updates
 
FROM
    sys.dm_db_index_usage_stats
    INNER JOIN sys.objects ON dm_db_index_usage_stats.OBJECT_ID = objects.OBJECT_ID
    INNER JOIN sys.indexes ON indexes.index_id = dm_db_index_usage_stats.index_id AND dm_db_index_usage_stats.OBJECT_ID = indexes.OBJECT_ID
WHERE
    indexes.is_primary_key = 0 --This line excludes primary key constarint
    AND
    indexes. is_unique = 0 --This line excludes unique key constarint
    AND 
    dm_db_index_usage_stats.user_updates <> 0 -- This line excludes indexes SQL Server hasn’t done any work with
    AND
    dm_db_index_usage_stats. user_lookups = 0
    AND
    dm_db_index_usage_stats.user_seeks = 0
    AND
    dm_db_index_usage_stats.user_scans = 0
ORDER BY
    dm_db_index_usage_stats.user_updates DESC
    
-- ******* Script - 2 Ends ****** ------    
