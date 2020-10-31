-- 114. SQL Server Script to find all the Tables without having a Primary Key

-- Script-1 : 

SELECT
	SCHEMA_NAME(schema_id) AS SchemaName
	,Name AS TableName
FROM sys.objects
WHERE [type]='U' 
	AND object_id NOT IN 
	(
		SELECT parent_object_id FROM sys.objects
		WHERE [type]='PK'
	)
GO

-- Script-2 :

SELECT
	SCHEMA_NAME(schema_id) AS SchemaName
	,Name AS TableName
FROM sys.tables
WHERE OBJECTPROPERTY(object_id,'TableHasPrimaryKey') = 0
GO
