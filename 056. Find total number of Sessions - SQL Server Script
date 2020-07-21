-- Find total number of Sessions - SQL Server Script

select
       db_name (resource_database_id) as DatabaseName
       ,count (*) as TotalSessions
from sys.dm_tran_locks
where resource_type = 'DATABASE'
	and db_name (resource_database_id) = 'Database_Name'
group by db_name (resource_database_id)
order by db_name (resource_database_id)
