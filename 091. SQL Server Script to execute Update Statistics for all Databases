--**** 091. SQL Server Script to execute Update Statistics for all Databases

DECLARE @SQL VARCHAR(1000)  
DECLARE @DBName sysname  
 
DECLARE DBcur CURSOR FORWARD_ONLY STATIC FOR  
SELECT [name]  
FROM master..sysdatabases 
WHERE [name] NOT IN ('master','model', 'tempdb') 
ORDER BY [name] 
     
OPEN DBcur  
FETCH NEXT FROM DBcur INTO @DBName  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
       SELECT @SQL = 'USE [' + @DBName +']' + CHAR(13) + 'EXEC sp_updatestats' + CHAR(13)  
       PRINT @SQL  
       FETCH NEXT FROM DBcur INTO @DBName  
   END      
CLOSE DBcur  
DEALLOCATE DBcur
 

--Reference : https://www.sqlskills.com/
