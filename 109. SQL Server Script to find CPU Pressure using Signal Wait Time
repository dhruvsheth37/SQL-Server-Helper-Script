-- 109. SQL Server Script to find CPU Pressure using Signal Wait Time

USE Master
GO
SELECT 
	SUM(signal_wait_time_ms) AS TotalSignalWaitTime 
	,(SUM(CAST(signal_wait_time_ms AS NUMERIC(20, 2)))
	/SUM(CAST(wait_time_ms AS NUMERIC(20, 2))) * 100)
	AS SignalWaitsOfTotalTimeInPercentage
FROM sys.dm_os_wait_stats
GO
