-- 071. Find out most recently modified Stored Procedure and Table in SQL Server
 
SELECT 
	SO.Name
	,SS.name 
	,SO.type_desc 
	,SO.create_date
	,SO.modify_date	
 FROM sys.objects AS SO
INNER JOIN sys.schemas AS SS 
	ON SS.schema_id = SO.schema_id 
WHERE DATEDIFF(D,modify_date, GETDATE()) < 50
AND TYPE IN ('P','U')
