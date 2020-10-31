-- 107.  SQL Server Script to find the size of Database Files and Log Files

SELECT 
    db_name(database_id) AS DatabaseName
    ,type_desc AS TypeDesc
    ,(size * 8) /1024 AS SizeInMB
    ,(size * 8) /1024/1024 AS SizeInGB
FROM sys.master_files 
ORDER BY name
