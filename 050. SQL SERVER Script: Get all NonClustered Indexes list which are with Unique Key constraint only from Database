-- SQL SERVER Script: Get all NonClustered Indexes list which are with Unique Key constraint only from Database
 SELECT QUOTENAME(schema_name(t.schema_id))+ '.[' +t.name+']',
	  i.name,i.* 
	 FROM sys.indexes i
	 INNER JOIN sys.tables t 
	 ON t.object_id= i.object_id
	 WHERE  i.type>0 
	 AND t.is_ms_shipped=0 
	 AND t.name<>'sysdiagrams'
	 

 
