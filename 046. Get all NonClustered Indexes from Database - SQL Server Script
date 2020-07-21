-- 046. Get all NonClustered Indexes from Database - SQL Server Script

 SELECT QUOTENAME(schema_name(t.schema_id))+ '.[' +t.name+']',  i.name 
	 FROM sys.indexes i
	 INNER JOIN sys.tables t 
	 ON t.object_id= i.object_id
	 WHERE i.type>0 
	 AND t.is_ms_shipped=0 
	 AND t.name<>'sysdiagrams'  --
	 AND (
	       is_primary_key=0   -- To discard clustered indexes
		   AND is_unique_constraint=0 -- To discard indexes with unique key constraints 
		 )
