------------****** Script to find redundant indexes Query-1 starts*********-------

WITH IndexColumns AS
(
    SELECT I.object_id AS TableObjectId, OBJECT_SCHEMA_NAME(I.object_id) + '.' + OBJECT_NAME(I.object_id) AS TableName, I.index_id AS IndexId, I.name AS IndexName
        , (IndexUsage.user_seeks + IndexUsage.user_scans + IndexUsage.user_lookups) AS IndexUsage
        , IndexUsage.user_updates AS IndexUpdates

       , (SELECT CASE is_included_column WHEN 1 THEN NULL ELSE column_id END AS [data()]
        FROM sys.index_columns AS IndexColumns
        WHERE IndexColumns.object_id = I.object_id
          AND IndexColumns.index_id = I.index_id
        ORDER BY index_column_id, column_id
        FOR XML PATH('')
       ) AS ConcIndexColumnNrs

       ,SUBSTRING((SELECT ', ' + CASE is_included_column WHEN 1 THEN NULL ELSE COL_NAME(I.object_id, column_id) END AS [data()]
        FROM sys.index_columns AS IndexColumns
        WHERE IndexColumns.object_id = I.object_id
          AND IndexColumns.index_id = I.index_id
        ORDER BY index_column_id, column_id
        FOR XML PATH('')
       ), 2, 10000) AS ConcIndexColumnNames

       ,(SELECT CASE is_included_column WHEN 1 THEN column_id ELSE NULL END AS [data()]
        FROM sys.index_columns AS IndexColumns
        WHERE IndexColumns.object_id = I.object_id
        AND IndexColumns.index_id = I.index_id
        ORDER BY column_id
        FOR XML PATH('')
       ) AS ConcIncludeColumnNrs

       ,SUBSTRING((SELECT ', ' + CASE is_included_column WHEN 1 THEN COL_NAME(I.object_id, column_id) ELSE NULL END AS [data()]
        FROM sys.index_columns AS IndexColumns
        WHERE IndexColumns.object_id = I.object_id
          AND IndexColumns.index_id = I.index_id
        ORDER BY column_id
        FOR XML PATH('')
       ), 2, 10000) AS ConcIncludeColumnNames
    FROM sys.indexes AS I
       LEFT OUTER JOIN sys.dm_db_index_usage_stats AS IndexUsage
        ON IndexUsage.object_id = I.object_id
          AND IndexUsage.index_id = I.index_id
          AND IndexUsage.Database_id = db_id() 
)
SELECT
  C1.TableName
  , C1.IndexName AS 'Index1'
  , C2.IndexName AS 'Index2'
  , CASE WHEN (C1.ConcIndexColumnNrs = C2.ConcIndexColumnNrs) AND (C1.ConcIncludeColumnNrs = C2.ConcIncludeColumnNrs) THEN 'Exact duplicate'
        WHEN (C1.ConcIndexColumnNrs = C2.ConcIndexColumnNrs) THEN 'Different includes'
        ELSE 'Overlapping columns' END AS StatusOfIndex
--  , C1.ConcIndexColumnNrs
--  , C2.ConcIndexColumnNrs
  , C1.ConcIndexColumnNames 
  , C2.ConcIndexColumnNames 
--  , C1.ConcIncludeColumnNrs
--  , C2.ConcIncludeColumnNrs
  , C1.ConcIncludeColumnNames
  , C2.ConcIncludeColumnNames
  , C1.IndexUsage
  , C2.IndexUsage
  , C1.IndexUpdates
  , C2.IndexUpdates
  , 'DROP INDEX ' + C2.IndexName + ' ON ' + C2.TableName AS Drop2
  , 'DROP INDEX ' + C1.IndexName + ' ON ' + C1.TableName AS Drop1
FROM IndexColumns AS C1
  INNER JOIN IndexColumns AS C2 
    ON (C1.TableObjectId = C2.TableObjectId)
    AND (
         -- exact: show lower IndexId as 1
            (C1.IndexId < C2.IndexId
            AND C1.ConcIndexColumnNrs = C2.ConcIndexColumnNrs
            AND C1.ConcIncludeColumnNrs = C2.ConcIncludeColumnNrs)
         -- different includes: show longer include as 1
         OR (C1.ConcIndexColumnNrs = C2.ConcIndexColumnNrs
            AND LEN(C1.ConcIncludeColumnNrs) > LEN(C2.ConcIncludeColumnNrs))
         -- overlapping: show longer index as 1
         OR (C1.IndexId <> C2.IndexId
            AND C1.ConcIndexColumnNrs <> C2.ConcIndexColumnNrs
            AND C1.ConcIndexColumnNrs like C2.ConcIndexColumnNrs + ' %')
    )
ORDER BY C1.TableName, C1.ConcIndexColumnNrs

------------****** Script to find redundant indexes Query-1 ends*********-------

GO
------------****** Script to find redundant indexes Query-2 Starts*********-------
;WITH MyDuplicate AS (SELECT
Sch.[name] AS SchemaName,
Obj.[name] AS TableName,
Idx.[name] AS IndexName,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 1) AS Col1,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 2) AS Col2,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 3) AS Col3,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 4) AS Col4,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 5) AS Col5,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 6) AS Col6,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 7) AS Col7,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 8) AS Col8,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 9) AS Col9,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 10) AS Col10,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 11) AS Col11,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 12) AS Col12,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 13) AS Col13,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 14) AS Col14,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 15) AS Col15,
INDEX_COL(Sch.[name] + '.' + Obj.[name], Idx.index_id, 16) AS Col16
FROM sys.indexes Idx
INNER JOIN sys.objects Obj ON Idx.[object_id] = Obj.[object_id] INNER JOIN sys.schemas Sch ON Sch.[schema_id] = Obj.[schema_id] WHERE index_id > 0)
SELECT    MD1.SchemaName, MD1.TableName, MD1.IndexName,
MD2.IndexName AS OverLappingIndex,
MD1.Col1, MD1.Col2, MD1.Col3, MD1.Col4,
MD1.Col5, MD1.Col6, MD1.Col7, MD1.Col8,
MD1.Col9, MD1.Col10, MD1.Col11, MD1.Col12,
MD1.Col13, MD1.Col14, MD1.Col15, MD1.Col16
FROM MyDuplicate MD1
INNER JOIN MyDuplicate MD2 ON MD1.tablename = MD2.tablename
AND MD1.indexname <> MD2.indexname
AND MD1.Col1 = MD2.Col1
AND (MD1.Col2 IS NULL OR MD2.Col2 IS NULL OR MD1.Col2 = MD2.Col2)
AND (MD1.Col3 IS NULL OR MD2.Col3 IS NULL OR MD1.Col3 = MD2.Col3)
AND (MD1.Col4 IS NULL OR MD2.Col4 IS NULL OR MD1.Col4 = MD2.Col4)
AND (MD1.Col5 IS NULL OR MD2.Col5 IS NULL OR MD1.Col5 = MD2.Col5)
AND (MD1.Col6 IS NULL OR MD2.Col6 IS NULL OR MD1.Col6 = MD2.Col6)
AND (MD1.Col7 IS NULL OR MD2.Col7 IS NULL OR MD1.Col7 = MD2.Col7)
AND (MD1.Col8 IS NULL OR MD2.Col8 IS NULL OR MD1.Col8 = MD2.Col8)
AND (MD1.Col9 IS NULL OR MD2.Col9 IS NULL OR MD1.Col9 = MD2.Col9)
AND (MD1.Col10 IS NULL OR MD2.Col10 IS NULL OR MD1.Col10 = MD2.Col10)
AND (MD1.Col11 IS NULL OR MD2.Col11 IS NULL OR MD1.Col11 = MD2.Col11)
AND (MD1.Col12 IS NULL OR MD2.Col12 IS NULL OR MD1.Col12 = MD2.Col12)
AND (MD1.Col13 IS NULL OR MD2.Col13 IS NULL OR MD1.Col13 = MD2.Col13)
AND (MD1.Col14 IS NULL OR MD2.Col14 IS NULL OR MD1.Col14 = MD2.Col14)
AND (MD1.Col15 IS NULL OR MD2.Col15 IS NULL OR MD1.Col15 = MD2.Col15)
AND (MD1.Col16 IS NULL OR MD2.Col16 IS NULL OR MD1.Col16 = MD2.Col16)
ORDER BY MD1.SchemaName,MD1.TableName,MD1.IndexName
------------****** Script to find redundant indexes Query-2 ends*********-------
