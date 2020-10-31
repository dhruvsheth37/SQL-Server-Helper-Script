--********** 087. SQL Server Script to check the size of Query Plan Cache
-- As a DBA, when you are dealing with huge SQL OLTP system, you should monitor the size of Query Plan Cache otherwise it affects to your query performance.


select 
	name
	,sum(pages_kb) /1024.0 InMBUsed
from sys.dm_os_memory_clerks
where name = 'SQL PLans'
group by name
