-- 106. SQL Server script to Find the total row count and size of the Tables


-- SQL Script for all tables:
SELECT 
	O.name AS TableName
	,P.rows AS TotalRows
	,SUM(AU.used_pages)*8 AS SizeInKB
FROM sys.objects AS O
JOIN sys.indexes AS I 
	ON O.object_id = I.object_id
JOIN sys.partitions AS P 
	ON O.object_id = P.object_id
JOIN sys.allocation_units AS AU 
	ON AU.container_id = P.partition_id
WHERE O.type = 'U' 
	AND I.index_id IN (0,1)
GROUP BY O.name, P.rows
ORDER BY 3 DESC


-- Using sp_spaceused
sp_spaceused 'Table_Name'
GO

-- Using DBCC SHOWCONTG
DBCC SHOWCONTIG ('Table_Name') WITH tableresults
GO
