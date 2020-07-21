https://database.guide/6-ways-to-check-the-size-of-a-database-in-sql-server-using-t-sql/


-- 051. Find database size - SQL Server Script

-- 1) Using sp_spaceused Stored Procedure

EXEC sp_spaceused;
Go

EXEC sp_spaceused N'Table_Name';
GO


-- 2) Using sp_helpdb Stored Procedure

EXEC sp_helpdb N'DATABASE_NAME';



-- 3) Using sp_databases Stored Procedure 

EXEC sp_databases;


-- 4) Using sys.master_files View

SELECT
    name,
    size,
    size * 8/1024 'Size (MB)',
    max_size
FROM sys.master_files
WHERE DB_NAME(database_id) = 'DATABASE_NAME';


-- 5) sys.database_files View

SELECT
    name,
    size,
    size * 8/1024 'Size (MB)',
    max_size
FROM sys.database_files;


-- 6) Using master_files table

SELECT
    d.name AS 'Database',
    m.name AS 'File',
    m.size,
    m.size * 8/1024 'Size (MB)',
    SUM(m.size * 8/1024) OVER (PARTITION BY d.name) AS 'Database Total',
    m.max_size
FROM sys.master_files m
INNER JOIN sys.databases d ON
d.database_id = m.database_id;
