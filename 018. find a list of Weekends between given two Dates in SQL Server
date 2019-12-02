--find a list of Weekends between given two Dates in SQL Server

--This script helps to DBA for finding available weekends between the dates so they can set auto-schedule for database maintenance.


DECLARE @startDate DATE = '20191201'
DECLARE @endDate DATE = '20191210'  
 
DECLARE @Weekend TABLE
(
	Weekend DATE PRIMARY KEY
	,IsWeekend BIT
)
 
WHILE @startDate <= @endDate 
BEGIN 
INSERT INTO @Weekend 
SELECT 
	@startDate AS Weekend 
	,(CASE WHEN DATEPART(WEEKDAY, @startDate) In (7, 1) THEN 1 ELSE 0 END) AS IsWeekend 
	SET @startDate = DateAdd(Day, 1, @startDate) 
END
 
SELECT Weekend FROM @Weekend WHERE IsWeekend = 1
