-- 135. Remove Cross duplicate rows in SQL Server

IF OBJECT_ID('tempdb..#temp') IS NOT NULL DROP TABLE #TEMP
GO
CREATE TABLE #TEMP
(ID1 INT, ID2 INT)
GO
INSERT INTO #TEMP
VALUES (2,1)
, (2,1)
, (1,2)
, (3,1)
, (5,2)
, (2,5)
, (4,3)
, (3,4)
, (6,2)
, (2,6)
, (2,7)
 
select * from #TEMP

select Id1,Id2 from(
SELECT ROW_NUMBER() OVER (PARTITION BY (A.ID1 * A.ID2) + (A.ID1 + A.ID2) ORDER BY A.ID1,A.ID2) AS ID, * FROM #TEMP A)as B
where id = 1
