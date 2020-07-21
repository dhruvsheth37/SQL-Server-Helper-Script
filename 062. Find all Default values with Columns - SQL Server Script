--062. Find all Default values with Columns - SQL Server Script

SELECT 
	SO.NAME AS TableName
	,SC.NAME AS ColumnName
	,SSM.TEXT AS DefaultValue
FROM dbo.sysobjects AS SO 
INNER JOIN dbo.syscolumns AS SC 
	ON SO.id = SC.id 
INNER JOIN dbo.syscomments AS SSM 
	ON SC.cdefault = SSM.id  
WHERE SO.xtype = 'U' 
ORDER BY SO.NAME,SC.colid
