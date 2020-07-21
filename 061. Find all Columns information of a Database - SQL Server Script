-- 061. Find all Columns information of a Database - SQL Server Script


SELECT 
	OBJECT_SCHEMA_NAME([T].[object_id],DB_ID()) AS SchemaName
        ,[T].[name] AS TableName
        ,[AC].[name] AS ColumnName
        ,[TY].[name] AS DataType
        ,[AC].[max_length] AS MaxLength
        ,[AC].[precision] AS ColumnPrecision
        ,[AC].[scale] AS ColumnScale
        ,[AC].[is_nullable] AS IsColumnNullable        
FROM sys.tables AS T   
INNER JOIN sys.all_columns AS AC 
	ON [T].[object_id] = [AC].[object_id]
INNER JOIN sys.types AS TY ON 
	[AC].[system_type_id] = [TY].[system_type_id] 
	AND [AC].[user_type_id] = [TY].[user_type_id]
WHERE [T].[is_ms_shipped] = 0  
-- AND [T].[name] ='TABLE_NAME'
ORDER BY [T].[name], [AC].[column_id]
