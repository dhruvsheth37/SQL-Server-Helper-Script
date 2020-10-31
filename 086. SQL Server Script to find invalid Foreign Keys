--******* 086. SQL Server Script to find invalid Foreign Keys
SELECT '[' + s.name + '].[' + o.name + '].[' + f.name + ']' AS ForeignKeyName
FROM    sys.foreign_keys f
INNER JOIN sys.objects o 
	ON f.parent_object_id = o.object_id
INNER JOIN sys.schemas s 
	ON o.schema_id = s.schema_id
WHERE   f.is_not_trusted = 1
	AND f.is_not_for_replication = 0
	AND f.is_disabled = 0
