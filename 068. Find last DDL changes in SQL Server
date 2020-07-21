-- 068. Find last DDL changes in SQL Server

-- sys.fn_trace_getinfo(NULL) will fetch default trace file.
SELECT 
	te.name AS eventtype
	,t.loginname
	,t.spid
	,t.starttime
	,t.objectname
	,t.databasename
	,t.hostname
	,t.ntusername
	,t.ntdomainname
	,t.clientprocessid
	,t.applicationname	
FROM sys.fn_trace_gettable
(
	CONVERT
	(VARCHAR(150)
	,(
		SELECT TOP 1 
			value
		FROM sys.fn_trace_getinfo(NULL)  
		WHERE property = 2
	)),DEFAULT
) T 
INNER JOIN sys.trace_events as te 
	ON t.eventclass = te.trace_event_id 
WHERE eventclass=164
