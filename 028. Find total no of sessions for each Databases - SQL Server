-- 028. Find total no of sessions for each Databases - SQL Server 
select
       db_name (resource_database_id) as DatabaseName
       ,count (*) as TotalSessions
from sys.dm_tran_locks
where resource_type = 'DATABASE'
group by db_name (resource_database_id)
order by db_name (resource_database_id)
