-- 022. Find the list of Triggers script - SQL Server
SELECT 
	sysobjects.name AS TriggerName 
	,USER_NAME(sysobjects.uid) AS TriggerOwner 
	,s.name AS TableSchema 
	,OBJECT_NAME(parent_obj) AS TableName 
	,OBJECTPROPERTY( id, 'ExecIsUpdateTrigger') AS Isupdate 
	,OBJECTPROPERTY( id, 'ExecIsDeleteTrigger') AS Isdelete 
	,OBJECTPROPERTY( id, 'ExecIsInsertTrigger') AS Isinsert 
	,OBJECTPROPERTY( id, 'ExecIsAfterTrigger') AS Isafter 
	,OBJECTPROPERTY( id, 'ExecIsInsteadOfTrigger') AS Isinsteadof
	,OBJECTPROPERTY(id, 'ExecIsTriggerDisabled') AS Isdisabled
FROM sysobjects 
INNER JOIN sysusers 
    ON sysobjects.uid = sysusers.uid 
INNER JOIN sys.tables t 
    ON sysobjects.parent_obj = t.object_id 
INNER JOIN sys.schemas s 
    ON t.schema_id = s.schema_id 
WHERE sysobjects.type = 'TR'
