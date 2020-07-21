-- 054. Rename all Tables of a Database - SQL Server Script

-- https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql?view=sql-server-ver15

DECLARE @SQL NVARCHAR(max)=''
 
SELECT @SQL += 'exec sp_rename ' + NAME + ',' + NAME + '_backup '
FROM   sys.tables
WHERE  NAME IN ( 'Table_1', 'Table_2', 'Table_3')

print @sql
 
EXEC sp_executesql @SQL
