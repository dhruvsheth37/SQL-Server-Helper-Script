-- 029. Find total number of Sessions of a Database - SQL Server

select
       db_name (resource_database_id) as DatabaseName
       ,count (*) as TotalSessions
from sys.dm_tran_locks
where resource_type = 'DATABASE'
    and db_name (resource_database_id) = 'Your_Database_Name' 
group by db_name (resource_database_id)
order by db_name (resource_database_id) 
