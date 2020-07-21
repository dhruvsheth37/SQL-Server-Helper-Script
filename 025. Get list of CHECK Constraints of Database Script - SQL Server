 -- 025. Get list of CHECK Constraints of Database Script - SQL Server
 
SELECT 
	S.name + '.' + CC.name AS CheckContraintName 
	,O.name AS ParentObject 
	,O.type_desc AS ParentType 
	,ISNULL(C.name, N'') AS ColumnName 
	,CC.definition AS ContraintDefinition 
	,CC.is_disabled AS IsDisabled 	
FROM sys.check_constraints AS CC 
INNER JOIN sys.schemas AS S 
    ON CC.schema_id = S.schema_id 
INNER JOIN sys.objects AS O 
    ON CC.parent_object_id = O.object_id 
LEFT JOIN sys.columns AS C 
    ON CC.parent_object_id = C.object_id 
    AND CC.parent_column_id = C.column_id 
ORDER BY ParentObject        
        ,ColumnName
GO

 
