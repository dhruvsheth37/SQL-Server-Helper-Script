-- 048. Get all Clustered Indexes from Database - SQL Server Script

 SELECT QUOTENAME(schema_name(t.schema_id))+ '.[' +t.name+']',
	  i.name,i.* 
	 FROM sys.indexes i
	 INNER JOIN sys.tables t 
	 ON t.object_id= i.object_id
	 WHERE  i.type>0 
	 AND t.is_ms_shipped=0 
	 AND t.name<>'sysdiagrams'  --
	 AND i.index_id=1
     AND i.type_desc='CLUSTERED'
