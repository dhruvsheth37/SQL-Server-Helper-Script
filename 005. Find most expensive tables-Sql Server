
----- ************ Find most expensive tables Starts ****** --------------
Select Object_Name(ix.[object_id]) as objectName 
        , Sum(ddius.user_seeks) As 'table_seeks' 
        , Sum(ddius.user_scans) As 'table_scans' 
        , Sum(ddius.user_lookups) As 'table_lookups' 
        , Sum(ddius.user_updates) As 'table_updates' 
        , Sum(ddius.user_seeks + ddius.user_scans) As 'query_activity' 
From sys.indexes As ix 
Left Join sys.dm_db_index_usage_stats ddius 
    On ix.object_id = ddius.object_id 
        And ix.index_id = ddius.index_id 
Where ddius.database_id = DB_ID() 
Group By Object_Name(ix.[object_id]) 
Order By query_activity Desc;

----- ************ Find most expensive tables  Ends ****** --------------


