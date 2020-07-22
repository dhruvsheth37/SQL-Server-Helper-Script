-- 078. Find Outdated Statistics - SQL Server Script
-- The purpose behind finding the outdated Statistics is, we should update those outdated indexes else our performance get hamppered due to outdated Statistics.

SELECT 
	OBJECT_NAME(id)
	,name
	,STATS_DATE(id, indid)
	,rowmodctr
FROM sys.sysindexes
WHERE STATS_DATE(id, indid)<=DATEADD(DAY,-1,GETDATE()) 
AND rowmodctr>0 
AND id IN (SELECT object_id FROM sys.tables)
GO
