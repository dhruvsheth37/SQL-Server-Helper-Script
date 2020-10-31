-- 111. SQL Server Script to find Status of all Database Trigger

SELECT
	[T].[name] AS TableName
	,[TR].[name] AS TriggerName
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsTriggerDisabled') =1 
		THEN 'DISABLED' ELSE 'ENABLED' 
	END) AS TriggerStatus
	 
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsInsertTrigger') =1 
		THEN 'No' ELSE 'Yes' 
	END) AS IsInsertTrigger
 
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsFirstInsertTrigger') =1 
		THEN 'No' ELSE 'Yes' 
	END) AS IsFirstInsertTrigger
 
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsLastInsertTrigger') =1 
		THEN 'No' ELSE 'Yes' 
	END) AS IsLAStInsertTrigger
 
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsDeleteTrigger') =1 
		THEN 'No' ELSE 'Yes' 
	END) AS IsDeleteTrigger
 
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsFirstDeleteTrigger') =1 
		THEN 'No' ELSE 'Yes' 
	END) AS IsFirstDeleteTrigger
 
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsLastDeleteTrigger') =1 
		THEN 'No' ELSE 'Yes' 
	END) AS IsLAStDeleteTrigger
 
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsUpdateTrigger') =1 
		THEN 'No' ELSE 'Yes' 
	END) AS IsUpdateTrigger
 
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsFirstUpdateTrigger') =1 
		THEN 'No' ELSE 'Yes' 
	END) AS IsFirstUpdateTrigger
 
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsLastUpdateTrigger') =1 
		THEN 'No' ELSE 'Yes' 
	END) AS IsLAStUpdateTrigger
 
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsAfterTrigger') =1 
		THEN 'No' ELSE 'Yes' 
	END) AS IsAfterTrigger
 
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsInsteadOfTrigger') =1 
		THEN 'No' ELSE 'Yes' 
	END) AS IsInsteadOfTrigger
 
	,(CASE 
		WHEN OBJECTPROPERTY([TR].[object_id], 'ExecIsTriggerNotForRepl') =1 
		THEN 'No' ELSE 'Yes' 
	END) AS IsTriggerNotForReplication 
FROM sys.tables AS T
INNER JOIN sys.triggers AS TR
	ON [T].[object_id]=[TR].[parent_id]
