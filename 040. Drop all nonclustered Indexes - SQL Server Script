-- 040. Drop all nonclustered Indexes - SQL Server Script

----------***************************-------------
--               Please note	     			        --
-- This script will not delete unique and clustered indexes	--
---------***************************-------------

DECLARE @SchemaName VARCHAR(256),
        @TableName VARCHAR(256),
        @IndexName VARCHAR(256),
        @TSQLDropIndex VARCHAR(MAX),
		@IsDroppedSuccessfully bit

IF OBJECT_ID('tempdb..#tableDrop') IS NOT NULL DROP TABLE #tableDrop
CREATE table #tableDrop 
(
  TableName VARCHAR(256),
  IndexName VARCHAR(256),
  dropScriptText VARCHAR(MAX),
  IsDroppedSuccessfully bit
)


DECLARE CursorIndexes CURSOR FOR
	 SELECT schema_name(t.schema_id), t.name,  i.name 
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

OPEN CursorIndexes
FETCH NEXT FROM CursorIndexes INTO @SchemaName,@TableName,@IndexName

WHILE @@fetch_status = 0
BEGIN
	  BEGIN TRY     
		 SET @TSQLDropIndex = 'DROP INDEX '+QUOTENAME(@SchemaName)+ '.' + QUOTENAME(@TableName) + '.' +QUOTENAME(@IndexName)
		 SET @IsDroppedSuccessfully=0
		 BEGIN TRY
			 PRINT @TSQLDropIndex
			 EXEC(@TSQLDropIndex)

			 SET @IsDroppedSuccessfully=1
		 END TRY
		 BEGIN CATCH
			SET @IsDroppedSuccessfully=0
		 END CATCH

		 INSERT INTO #tableDrop values(QUOTENAME(@SchemaName)+ '.[' +@TableName+']',@IndexName,@TSQLDropIndex,@IsDroppedSuccessfully)
      END TRY
	  BEGIN CATCH 
	  END CATCH

	 FETCH NEXT FROM CursorIndexes INTO @SchemaName,@TableName,@IndexName
END

CLOSE CursorIndexes
DEALLOCATE CursorIndexes 

SELECT * FROM #tableDrop
IF OBJECT_ID('tempdb..#tableDrop') IS NOT NULL DROP TABLE #tableDrop
