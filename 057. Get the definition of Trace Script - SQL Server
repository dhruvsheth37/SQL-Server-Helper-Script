-- Step-1
-- Get the default trace_id of instance:
SELECT distinct traceid 
FROM ::fn_trace_getinfo(default)
GO

-- Step-2
-- Pass trace_id in fn_trace_geteventinfo() and get the definition of Trace:
-- pass trace_id by replacing NO_OUTPUT in below query
select
	tg.eventid as EventID
	,te.Name as EventName 
	,tg.columnid as ColumnID
	,cols. name as ColumnName
from :: fn_trace_geteventinfo(NO_OUTPUT) as tg 
INNER JOIN sys.trace_events as te 
	ON tg.eventid = te.trace_event_id
INNER JOIN sys.trace_columns cols 
	ON tg.columnid = cols.trace_column_id
