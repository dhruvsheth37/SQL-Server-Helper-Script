-- 042. Find Large Object Data Type Columns - SQL Server Script

SELECT 
	[s].[name] + '.' + [t].[name] AS TableName
FROM [sys].[tables] AS t
INNER JOIN [sys].[schemas] AS s
	ON [t].[schema_id] = [s].[schema_id]
WHERE EXISTS
(
	SELECT 1 FROM [sys].[columns] AS c
	WHERE [c].[object_id] = [t].[object_id]
	AND [c].[max_length] = -1
	AND [c].[system_type_id] IN 
	(
		165, -- VARBINARY
		167, -- VARCHAR
		231  -- NVARCHAR		
	)
);
