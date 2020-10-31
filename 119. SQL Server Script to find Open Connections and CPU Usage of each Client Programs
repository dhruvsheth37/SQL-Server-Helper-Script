-- 119. SQL Server Script to find Open Connections and CPU Usage of each Client Programs

SELECT 
    convert(varchar(50), program_name) as ProgramName
    ,count(*) as TotalInstances
    ,sum(cpu) as CPUSum
    ,sum(datediff(second, login_time, getdate())) as SumOfSecond
    ,convert(float, sum(cpu)) / convert(float, sum(datediff(second, login_time, getdate()))) as PerformanceScore
    ,convert(float, sum(cpu)) / convert(float, sum(datediff(second, login_time, getdate()))) / count(*) as ProgramPerformance
FROM master..sysprocesses
WHERE spid > 50
GROUP BY
    convert(varchar(50), program_name)
ORDER BY PerformanceScore DESC
