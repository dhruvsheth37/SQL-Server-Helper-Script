--SQL Server Script: Find a Table which has more than N columns
	
 
DECLARE @threshold INT;
SET @threshold = 25;
 
;WITH cte([object_id], [column count]) AS
(
	SELECT [object_id], COUNT(*)
	FROM sys.columns
	GROUP BY [object_id]
	HAVING COUNT(*) > @threshold
)
SELECT 
	[s].[name] + '.' + [t].[name] AS TableName
    ,[cte].[column count]
FROM cte
INNER JOIN sys.tables AS t
	ON [cte].[object_id] = [t].[object_id]
INNER JOIN sys.schemas AS s
	ON [t].[schema_id] = [s].[schema_id]
ORDER BY [cte].[column count] DESC
GO
