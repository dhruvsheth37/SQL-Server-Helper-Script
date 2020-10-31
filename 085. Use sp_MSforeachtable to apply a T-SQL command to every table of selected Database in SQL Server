--********** 085. Use sp_MSforeachtable to apply a T-SQL command to every table of selected Database in SQL Server
--When we require executing same T-SQL command for all the tables, we can use this stored procedure.
--Many times we need to run drop/truncate command for all tables or REINDEX all tables, at that point instead of the manual script we can use this stored procedure.

-- 1. Truncate all tables of current database:
EXEC sp_MSforeachtable 'TRUNCATE TABLE ?'

-- 2. Check the count of all tables:
EXEC sp_MSforeachtable 'TRUNCATE TABLE ?'

-- 3. Drop all tables of current database:
EXEC sp_MSforeachtable 'DROP TABLE ?'

-- 4. REINDEX all tables of current database:
EXEC sp_MSforeachtable 'DBCC DBREINDEX(''?'')'
