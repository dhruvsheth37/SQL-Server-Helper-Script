-- 124. SQL Server Script to check all Database Autogrowth Settings
 
SET STATISTICS TIME ON
exec sp_MSforeachdb 'use [?]; EXEC sp_helpfile'
