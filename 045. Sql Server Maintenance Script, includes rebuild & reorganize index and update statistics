
    --- **** Maintenance Script, includes rebuild & reorganize index and update statistics ** --
	-- Make Sure you have write USE <databasename> statement before executing statement.  
	-- USE <databasename>
	SET NOCOUNT ON;  
	DECLARE @objectid int;  
	DECLARE @indexid int;  
	DECLARE @partitioncount bigint;  
	DECLARE @schemaname nvarchar(500);   
	DECLARE @objectname nvarchar(500);   
	DECLARE @indexname nvarchar(500);   
	DECLARE @partitionnum bigint;  
	DECLARE @partitions bigint;  
	DECLARE @frag float;  
	DECLARE @command nvarchar(4000);   
	-- Conditionally select tables and indexes from the sys.dm_db_index_physical_stats function   
	-- and convert object and index IDs to names.  

	-- Drop the temporary table.  
	IF OBJECT_ID('tempdb..#work_to_do') IS NOT NULL DROP TABLE #work_to_do;
	
	SELECT  
		object_id AS objectid,  
		index_id AS indexid,  
		partition_number AS partitionnum,  
		avg_fragmentation_in_percent AS frag  
	INTO #work_to_do  
	FROM sys.dm_db_index_physical_stats (DB_ID(), NULL, NULL , NULL, 'LIMITED')  
	WHERE index_id > 0;  
    
	-- Declare the cursor for the list of partitions to be processed.  
	DECLARE partitions CURSOR FOR SELECT * FROM #work_to_do;  

	-- Open the cursor.  
	OPEN partitions;  

	-- Loop through the partitions.  
	WHILE (1=1)  
		BEGIN;  
			FETCH NEXT  
			   FROM partitions  
			   INTO @objectid, @indexid, @partitionnum, @frag;  
			IF @@FETCH_STATUS < 0 BREAK;  
			
			SELECT @objectname = QUOTENAME(o.name), @schemaname = QUOTENAME(s.name)  
			FROM sys.objects AS o  
			JOIN sys.schemas as s ON s.schema_id = o.schema_id  
			WHERE o.object_id = @objectid AND (o.name<>'QueryNotificationErrorsQueue' AND o.Name<>'EventNotificationErrorsQueue' AND o.Name<>'ServiceBrokerQueue');
			
			SELECT @indexname = QUOTENAME(name)  
			FROM sys.indexes  
			WHERE  object_id = @objectid AND index_id = @indexid;  

			SELECT @partitioncount = count (*)  
			FROM sys.partitions  
			WHERE object_id = @objectid AND index_id = @indexid;  

			-- 30 is an arbitrary decision point at which to switch between reorganizing and rebuilding.  
			IF @frag < 30.0  OR @frag >= 5.0
				SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REORGANIZE';  
			ELSE IF @frag >= 30.0 --OR @frag < 5.0 
				SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REBUILD';  
			IF @partitioncount > 1  
				SET @command = @command + N' PARTITION=' + CAST(@partitionnum AS nvarchar(10));  
			BEGIN TRY
			  IF(ISNULL(LEN(@indexname),0)>0 and ISNULL(LEN(@schemaname),0)>0 and ISNULL(LEN(@objectname),0)>0)
			  BEGIN
			   ----print(@command)
			   EXEC (@command);  
			  END

			 

			END TRY
			BEGIN CATCH
				PRINT  @command +'=====> Failed <======'
				SELECT -1
			   PRINT 'ErrorNumber: ' + CAST(ERROR_NUMBER() as VARCHAR(100)) +CHAR(13) +
			  'ErrorSeverity: '+   CAST(ERROR_SEVERITY() as VARCHAR(100))  +CHAR(13) +
			  'ErrorState: '  +  CAST(ERROR_STATE() as VARCHAR(100)) +CHAR(13) +
			  --'ErrorProcedure: '+ CAST(ERROR_PROCEDURE() as VARCHAR(300)) +CHAR(13) --+
			  'ErrorLine: ' + CAST(ERROR_LINE() as VARCHAR(100)) +CHAR(13) +
			  'ErrorMessage: ' + ERROR_MESSAGE()

			    
			END CATCH
			PRINT N'Executed: ' + @command;  



          -- Update statistics Starts
          DECLARE @sqlQuery VARCHAR(800) 
	      SELECT @sqlQuery= 'UPDATE STATISTICS ['+DB_NAME()+'].'+@schemaname+'.'+@objectname  

		  BEGIN TRY
			  EXEC(@sqlQuery)
			  --PRINT @sqlQuery 
		  END TRY
		  BEGIN CATCH
     		  PRINT @sqlQuery +'=====> Failed <======'+ CAST(ERROR_NUMBER() as VARCHAR(20))
			  PRINT 'ErrorNumber: ' + CAST(ERROR_NUMBER() as VARCHAR(100)) +CHAR(13) +
			  'ErrorSeverity: '+   CAST(ERROR_SEVERITY() as VARCHAR(100))  +CHAR(13) +
			  'ErrorState: '  +  CAST(ERROR_STATE() as VARCHAR(100)) +CHAR(13) +
			  --'ErrorProcedure: '+ CAST(ERROR_PROCEDURE() as VARCHAR(300)) +CHAR(13) --+
			  'ErrorLine: ' + CAST(ERROR_LINE() as VARCHAR(100)) +CHAR(13) +
			  'ErrorMessage: ' + ERROR_MESSAGE()

		   END CATCH
		   -- Update statistics Ends
		END;  

	-- Close and deallocate the cursor.  
	CLOSE partitions;  
	DEALLOCATE partitions;  

	-- Drop the temporary table.  
	IF OBJECT_ID('tempdb..#work_to_do') IS NOT NULL DROP TABLE #work_to_do;
 

--------------- Start Statistics update starts-----------------
 
