-- 044. Find a Table which has more than N Indexes - SQL Server Script

--More Indexes on a Table, are creating a performance issue because Indexes also require dedicated CPU I/O for writing it into the Index Pages.
--More Indexes will slow down the insertion or any other DML operation of that particular Table.	
 
DECLARE @thresholdCount INT;
SET @thresholdCount = 5;
 
SELECT
	[s].[name] + '.' + [t].[name] AS TableName
FROM sys.tables AS t
INNER JOIN sys.schemas AS s
	ON [t].[schema_id] = [s].[schema_id]
WHERE EXISTS
(
	SELECT 1 FROM sys.indexes AS i
    WHERE [i].[object_id] = [t].[object_id]
    GROUP BY [i].[object_id]
    HAVING COUNT(*) > @thresholdCount
)
