-- 113. SQL Server Script to find Identity Column of a Database


-- Using sys.tables and sys.identity_columns:
SELECT 
	T.Name AS TableName
	,IC.name AS ColumnName
	,IC.is_identity AS IsIdentity
FROM sys.tables AS T 
INNER JOIN sys.identity_columns AS IC 
	ON T.[object_id]=IC.[object_id]
WHERE T.type='U' 
	AND is_identity=1
  
  
-- Using INFORMATION_SCHEMA.COLUMNS:
;With CTE AS 
(
	SELECT 
		Table_Schema+'.'+Table_Name AS TableName
		,[Column_name] AS ColumnName
	FROM INFORMATION_SCHEMA.COLUMNS
)
SELECT
	TableName
	,ColumnName
	,COLUMNPROPERTY(OBJECT_ID(TableName),ColumnName,'IsIdentity') AS IsIdentity
FROM CTE 
WHERE COLUMNPROPERTY(OBJECT_ID(TableName),ColumnName,'IsIdentity')=1  



--Using sys.objects and sys.identity_columns:
SELECT 
	T.Name AS TableName
	,IC.name AS ColumnName
	,IC.is_identity AS IsIdentity
FROM sys.objects AS T 
INNER JOIN sys.identity_columns AS IC 
	ON T.[object_id]=IC.[object_id]
WHERE T.type='U' 
	AND is_identity=1
