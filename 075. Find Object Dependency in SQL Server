-- 075. Find Object Dependency in SQL Server

-- Script - 1  
SELECT DISTINCT 
	SO.Name
	,SO.XType AS ObjectType
	,SC.TEXT AS ObjectDefinition
FROM syscomments AS SC
INNER JOIN sysobjects AS SO ON SC.id=SO.id
WHERE SC.TEXT LIKE '%tablename%'
GO

-- Script - 2 
SELECT OBJECT_NAME(OBJECT_ID)
  FROM sys.sql_modules
 WHERE DEFINITION LIKE '%tablename%'
GO

-- Script - 3 
SELECT 
    referencing_schema_name, referencing_entity_name, referencing_id, 
    referencing_class_desc, is_caller_dependent
FROM 
    sys.dm_sql_referencing_entities ('SchemaName.TableName', 'Object');
GO
