-- 104. SQL Server Script to find all Running SQL Server Agent JOB
 
SELECT
	SJ.Name
	,SJ.job_ID
	,SJA.run_requested_Date    
FROM msdb.dbo.sysjobs AS SJ 
INNER JOIN msdb.dbo.sysjobactivity AS SJA
	ON SJ.job_id = SJA.job_id
WHERE SJA.run_requested_date IS NOT NULL
	AND SJA.stop_execution_date IS NULL
