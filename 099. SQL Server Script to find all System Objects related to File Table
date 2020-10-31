-- 099. SQL Server Script to find all System Objects related to File Table
 
DECLARE @FileTableName VARCHAR(50)
SET @FileTableName='dbo.FileTableName'
 
SELECT 
	OBJECT_NAME(parent_object_id) AS FileTableName
	,OBJECT_NAME(object_id) AS AllRelatedObjects
FROM sys.filetable_system_defined_objects
WHERE parent_object_id = object_id(@FileTableName)
GO
