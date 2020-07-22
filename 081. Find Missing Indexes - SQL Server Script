-- 081. Find Missing Indexes - SQL Server Script

-- Script - 1 

SELECT TOP 100 PERCENT DB_NAME() AS [DB Name]
, OBJECT_NAME(dmvMID.OBJECT_ID,dmvMID.database_id) AS [Table Name]
, '/* ' + '
	[Author]: '+ REPLACE(SUSER_SNAME(), '.', ' ') + '
	[Date of Creation]: ' + CONVERT(varchar(10), GETDATE(), 101) + '
	[Contact]: '+ SUSER_SNAME() + '@technothirsty.com
	*/ ' + CHAR(10) + CHAR(10)

	+'CREATE NONCLUSTERED INDEX [IDX_' + OBJECT_NAME(dmvMID.OBJECT_ID,dmvMID.database_id) + '_'
	+ REPLACE(REPLACE(REPLACE(COALESCE(dmvMID.equality_columns,''),', ','_'),'[',''),']','') +
	CASE
		WHEN (dmvMID.equality_columns IS NOT NULL AND dmvMID.inequality_columns IS NOT NULL) THEN '_'
		ELSE ''
	END
	+ REPLACE(REPLACE(REPLACE(COALESCE(dmvMID.inequality_columns,''),', ','_'),'[',''),']','')
	+ ']'
	+ ' ON ' + dmvMID.statement
	+ ' (' + COALESCE (dmvMID.equality_columns,'')
	+ CASE
		WHEN (dmvMID.equality_columns IS NOT NULL AND dmvMID.inequality_columns IS NOT NULL) THEN ','
		ELSE
	'' END
	+ COALESCE (dmvMID.inequality_columns, '')
	+ ')' + CHAR(10)
	+ COALESCE (' INCLUDE (' + dmvMID.included_columns + ')', '') + CHAR(10)
	+ 'WITH (PAD_INDEX  = OFF, STATISTICS_NORECOMPUTE  = OFF, SORT_IN_TEMPDB = OFF, IGNORE_DUP_KEY = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS  = ON, ALLOW_PAGE_LOCKS  = ON, FILLFACTOR = 80)'
	+ ' GO'
	AS [Missing Index SQL Script]
, dmvMIGS.user_seeks as [User Seeks]
, CAST(dmvMIGS.avg_user_impact AS varchar)+ ' %'AS [Estimated Impact]
, dmvMIGS.last_user_seek AS [Last User Seek]
--, dmvMIGS.avg_total_user_cost AS [Estimated Cost on disk]
, (SELECT COUNT(*) from sys.indexes where OBJECT_ID = dmvMID.OBJECT_ID and type_desc = 'NONCLUSTERED') AS [NC Indexes]
, OBJECTPROPERTY(dmvMID.object_id, 'tableHasClustIndex') as [Is Clust Idx]
,(SELECT
CAST (SUM(
 CASE
 WHEN ps.usedpages > ps.pages THEN (ps.usedpages - ps.pages)
 ELSE 0
 END * 8) AS varchar(100)) + ' KB' AS indexsize
 FROM sys.indexes i
 INNER JOIN (
 SELECT
 OBJECT_ID,
 index_id,
 SUM (used_page_count) usedpages,
 SUM (
 CASE
 WHEN (index_id < 2) THEN (in_row_data_page_count + lob_used_page_count + row_overflow_used_page_count)
 ELSE lob_used_page_count + row_overflow_used_page_count
 END
 )pages
 FROM sys.dm_db_partition_stats
 WHERE object_id = dmvMID.OBJECT_ID
 GROUP BY object_id, index_id
 ) ps on i.index_id = ps.index_id
 WHERE i.object_id = dmvMID.OBJECT_ID) as [Total Index Size]
FROM sys.dm_db_missing_index_groups as dmvMIG
INNER JOIN sys.dm_db_missing_index_group_stats dmvMIGS
	ON dmvMIGS.group_handle = dmvMIG.index_group_handle
INNER JOIN sys.dm_db_missing_index_details dmvMID
	ON dmvMIG.index_handle = dmvMID.index_handle
WHERE dmvMID.database_ID = DB_ID()
--AND OBJECT_NAME(dmvMID.OBJECT_ID,dmvMID.database_id) LIKE '%TableName%'
ORDER BY [Estimated Impact] DESC


-- Script-2


SELECT DISTINCT TableName FROM (
SELECT TOP 50
dm_mid.database_id AS DatabaseID,
dm_migs.avg_user_impact*(dm_migs.user_seeks+dm_migs.user_scans) Avg_Estimated_Impact,
dm_migs.last_user_seek AS Last_User_Seek,
OBJECT_NAME(dm_mid.OBJECT_ID,dm_mid.database_id) AS [TableName],
'CREATE INDEX [IX_' + OBJECT_NAME(dm_mid.OBJECT_ID,dm_mid.database_id) + '_'
+ REPLACE(REPLACE(REPLACE(ISNULL(dm_mid.equality_columns,''),', ','_'),'[',''),']','') 
+ CASE
WHEN dm_mid.equality_columns IS NOT NULL
AND dm_mid.inequality_columns IS NOT NULL THEN '_'
ELSE ''
END
+ REPLACE(REPLACE(REPLACE(ISNULL(dm_mid.inequality_columns,''),', ','_'),'[',''),']','')
+ ']'
+ ' ON ' + dm_mid.statement
+ ' (' + ISNULL (dm_mid.equality_columns,'')
+ CASE WHEN dm_mid.equality_columns IS NOT NULL AND dm_mid.inequality_columns 
IS NOT NULL THEN ',' ELSE
'' END
+ ISNULL (dm_mid.inequality_columns, '')
+ ')'
+ ISNULL (' INCLUDE (' + dm_mid.included_columns + ')', '') AS Create_Statement
FROM sys.dm_db_missing_index_groups dm_mig
INNER JOIN sys.dm_db_missing_index_group_stats dm_migs
ON dm_migs.group_handle = dm_mig.index_group_handle
INNER JOIN sys.dm_db_missing_index_details dm_mid
ON dm_mig.index_handle = dm_mid.index_handle
WHERE dm_mid.database_ID = DB_ID()
ORDER BY Avg_Estimated_Impact DESC
) F
GO



-- Script-3
SELECT TOP 25
	 ROUND(DMIGS.avg_total_user_cost * DMIGS.avg_user_impact * (DMIGS.user_seeks + DMIGS.user_scans),0) AS TotalCost
	 ,DMID.[statement] AS TableName
	 ,equality_columns
	 ,inequality_columns
	 ,included_columns
FROM sys.dm_db_missing_index_groups AS DMIG
INNER JOIN sys.dm_db_missing_index_group_stats AS DMIGS
	ON DMIGS.group_handle = DMIG.index_group_handle
INNER JOIN sys.dm_db_missing_index_details AS DMID
	ON DMID.index_handle = DMIG.index_handle
ORDER BY 1 DESC

