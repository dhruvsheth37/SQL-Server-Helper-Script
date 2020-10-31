-- 128. SQL Server Script to find uncontained objects of a Database
 
SELECT 
	O.name
	,O.type_desc
	,DDUE.class_desc
	,DDUE.statement_line_number
	,DDUE.statement_type
	,DDUE.feature_name
	,DDUE.feature_type_name
FROM sys.dm_db_uncontained_entities AS DDUE
LEFT JOIN sys.objects AS O
ON DDUE.major_id = O.object_id
