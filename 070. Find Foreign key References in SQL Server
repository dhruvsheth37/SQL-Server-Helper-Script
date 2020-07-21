-- 070. Find Foreign key References in SQL Server
 
SELECT 
	ccu.table_name AS SourceTable
	,ccu.constraint_name AS SourceConstraint
	,ccu.column_name AS SourceColumn
	,kcu.table_name AS TargetTable
	,kcu.column_name AS TargetColumn
FROM INFORMATION_SCHEMA.CONSTRAINT_COLUMN_USAGE ccu
	INNER JOIN INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS rc
		ON ccu.CONSTRAINT_NAME = rc.CONSTRAINT_NAME 
	INNER JOIN INFORMATION_SCHEMA.KEY_COLUMN_USAGE kcu 
		ON kcu.CONSTRAINT_NAME = rc.UNIQUE_CONSTRAINT_NAME  
ORDER BY ccu.table_name
