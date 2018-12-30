
WITH cte AS 
( 
    SELECT 
        table_name = obj.name,    
        obj.[object_id], 
        ind.index_id, 
        ind.type, 
        ind.type_desc 
    FROM sys.indexes ind 
    INNER JOIN sys.objects obj on ind.[object_id] = obj.[object_id] 
    WHERE obj.type in ('U') 
    AND obj.is_ms_shipped = 0 and ind.is_disabled = 0  and ind.is_hypothetical = 0 
    AND ind.type <= 2 
), cte2 AS 
( 
SELECT * FROM cte c 
PIVOT (count(type) for type_desc in ([HEAP], [CLUSTERED], [NONCLUSTERED])) pv 
) 
SELECT 
    c2.table_name AS 'Table Name', 
    [ROWS] = max(p.rows), 
    IS_HEAP = sum([HEAP]), 
    IS_CLUSTERED = sum([CLUSTERED]), 
    NUM_OF_NONCLUSTERED = sum([NONCLUSTERED]) 
FROM cte2 c2 
INNER JOIN sys.partitions p 
ON c2.[object_id] = p.[object_id] AND c2.index_id = p.index_id 
GROUP BY table_name
