--Whenever we are finding some issues in performance, we are also try to avoid Dynamic Sql in Stored Procedure. 
--To avoid sql injection we should not write dynamic sql.
 
-- Find stored procedures which have used Temporary Table 
SELECT  
	SP_Name
	,error_message
	,error_type_desc 
FROM (SELECT schema_name(schema_id)+'.'+name SP_Name FROM sys.procedures) AS T
CROSS APPLY sys.dm_exec_describe_first_result_set (SP_Name, NULL, 0) 
WHERE error_type =10
