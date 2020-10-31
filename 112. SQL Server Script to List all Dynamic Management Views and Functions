-- 112. SQL Server Script to List all Dynamic Management Views and Functions

SELECT 
      name
      ,type
      ,type_desc
FROM sys.system_objects
WHERE name LIKE 'dm[_]%'
ORDER BY name
