-- 074. Find Cross Database Object Dependency in SQL Server
 
SELECT  
	OBJECT_NAME (referencing_id) AS ReferencedObjects
	,referenced_database_name
	,referenced_schema_name
	,referenced_entity_name
FROM sys.sql_expression_dependencies
WHERE referenced_database_name IS NOT NULL
AND is_ambiguous = 0;
