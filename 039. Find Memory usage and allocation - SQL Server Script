-- 039. Find Memory usage and allocation - SQL Server Script

-- Query-1 
DBCC MEMORYSTATUS 
GO 

-- Query-2 
SELECT
	(physical_memory_in_use_kb/1024) AS Memory_usedby_SQLServer_in_MB
	,(locked_page_allocations_kb/1024) AS Locked_pages_in_MB
	,(total_virtual_address_space_kb/1024) AS Total_Virtual_Address_Space_in_MB
	,memory_utilization_percentage 
	,process_physical_memory_low
	,process_virtual_memory_low
FROM sys.dm_os_process_memory;
