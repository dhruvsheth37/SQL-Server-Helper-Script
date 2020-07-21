-- 041. Find disable foreign key tables - SQL Server Script


SELECT 
	[s].[name] + '.' + [t].[name] AS TableName
FROM [sys].[tables] AS t
INNER JOIN [sys].[schemas] AS s
	ON [t].[schema_id] = [s].[schema_id]
WHERE EXISTS
(
	SELECT 1 FROM [sys].[foreign_keys] AS fk
	WHERE [fk].[parent_object_id] = [t].[object_id]
		AND [fk].[is_disabled] = 1
);
