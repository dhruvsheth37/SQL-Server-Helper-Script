SELECT col.name as ColumnName,
       count(*) as Tables,
       cast(100.0 * count(*) / 
       (select count(*) from sys.tables) as numeric(36, 1)) as PercentTables
   FROM sys.tables as tbl
   INNER JOIN sys.columns as col 
   ON tbl.object_id = col.object_id
GROUP BY col.name 
HAVING count(*) > 1
ORDER BY count(*) DESC
