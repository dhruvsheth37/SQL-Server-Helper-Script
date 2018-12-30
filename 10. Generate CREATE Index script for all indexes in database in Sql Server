--Generate CREATE Index script for all indexes in database in Sql Server

--*******************************---
--Generate CREATE Index script for all indexes Script-1: ----
--*******************************--

--------------------------------------------------------------
--------Developer: Technothirsty.com -------------------------
--------Date:      16-06-2017---------------------------------    
--------Purpose:   Get all existing indexes,------------------ 
--------           but NOT the primary and unique keys--------
--------------------------------------------------------------
--------------------------------------------------------------

 DECLARE
    @IncludeFileGroup  bit = 1,
    @IncludeDrop       bit = 1,
    @IncludeFillFactor bit = 1
 
    -- Get all existing indexes, but NOT the primary and unique keys
    DECLARE Indexes_cursor CURSOR
        FOR SELECT 
               SC.Name         AS   SchemaName
               , SO.Name         AS   TableName
                    , SI.Object_Id     AS   TableId
               , SI.[Name]         AS   IndexName
               , SI.Index_ID       AS   IndexId
               , FG.[Name]       AS FileGroupName
               , CASE WHEN SI.Fill_Factor = 0 THEN 100 ELSE SI.Fill_Factor END  Fill_Factor
              FROM sys.indexes SI
              LEFT JOIN sys.filegroups FG
                     ON SI.data_space_id = FG.data_space_id
              INNER JOIN sys.objects SO
               ON SI.object_id = SO.object_id
           INNER JOIN sys.schemas SC
               ON SC.schema_id = SO.schema_id
             WHERE ObjectProperty(SI.Object_Id, 'IsUserTable') = 1
               AND SI.[Name] IS NOT NULL
               AND SI.is_primary_key = 0
               AND SI.is_unique_constraint = 0
               AND IndexProperty(SI.Object_Id, SI.[Name], 'IsStatistics') = 0
             ORDER BY Object_name(SI.Object_Id), SI.Index_ID

    DECLARE @SchemaName      sysname
    DECLARE @TableName         sysname
    DECLARE @TableId               int
    DECLARE @IndexName            sysname
    DECLARE @FileGroupName   sysname
    DECLARE @IndexId               int
    DECLARE @FillFactor            int

    DECLARE @NewLine nvarchar(4000)     SET @NewLine = CHAR(13) + CHAR(10)
    DECLARE @Tab         nvarchar(4000)     SET @Tab = Space(4)

    -- Loop through all indexes
    OPEN Indexes_cursor

    FETCH NEXT
     FROM Indexes_cursor
     INTO @SchemaName, @TableName, @TableId, @IndexName, @IndexId, @FileGroupName, @FillFactor

    WHILE (@@Fetch_Status = 0)
        BEGIN

            DECLARE @sIndexDesc   nvarchar(4000)
            DECLARE @sCreateSql   nvarchar(4000)
            DECLARE @sDropSql      nvarchar(4000)

            SET @sIndexDesc = '-- Index ' + @IndexName + ' on table ' + @TableName
            SET @sDropSql = 'IF NOT EXISTS(SELECT 1' + @NewLine
                          + '            FROM sysindexes si' + @NewLine
                          + '            INNER JOIN sysobjects so' + @NewLine
                          + '                   ON so.id = si.id' + @NewLine
                          + '           WHERE si.[Name] = N''' + @IndexName + ''' -- Index Name' + @NewLine
                          + '             AND so.[Name] = N''' + @TableName + ''')  -- Table Name' + @NewLine
                          + 'BEGIN' + @NewLine
                          --+ '    DROP INDEX [' + @IndexName + '] ON [' + @SchemaName + '].[' + @TableName + ']' + @NewLine
                          

            SET @sCreateSql = 'CREATE '

            -- Check if the index is unique
            IF (IndexProperty(@TableId, @IndexName, 'IsUnique') = 1)
                BEGIN
                    SET @sCreateSql = @sCreateSql + 'UNIQUE '
                END
            --END IF
            -- Check if the index is clustered
            IF (IndexProperty(@TableId, @IndexName, 'IsClustered') = 1)
                BEGIN
                    SET @sCreateSql = @sCreateSql + 'CLUSTERED '
                END
            --END IF

            SET @sCreateSql = @sCreateSql + 'INDEX [' + @IndexName + '] ON [' + @SchemaName + '].[' + @TableName + ']' + @NewLine + '(' + @NewLine

            -- Get all columns of the index
            DECLARE IndexColumns_cursor CURSOR
                FOR SELECT SC.[Name],
                           IC.[is_included_column],
                           IC.is_descending_key
                      FROM sys.index_columns IC
                     INNER JOIN sys.columns SC
                             ON IC.Object_Id = SC.Object_Id
                            AND IC.Column_ID = SC.Column_ID
                     WHERE IC.Object_Id = @TableId
                       AND Index_ID = @IndexId
                     ORDER BY IC.[is_included_column],IC.key_ordinal

            DECLARE @IxColumn         sysname
            DECLARE @IxIncl               bit
            DECLARE @Desc               bit
            DECLARE @IxIsIncl               bit     SET @IxIsIncl = 0
            DECLARE @IxFirstColumn      bit     SET @IxFirstColumn = 1

            -- Loop through all columns of the index and append them to the CREATE statement
            OPEN IndexColumns_cursor
            FETCH NEXT
             FROM IndexColumns_cursor
             INTO @IxColumn, @IxIncl, @Desc

            WHILE (@@Fetch_Status = 0)
                BEGIN
                    IF (@IxFirstColumn = 1)
                        BEGIN
                            SET @IxFirstColumn = 0
                        END
                    ELSE
                        BEGIN
                            --check to see if it's an included column
                            IF (@IxIsIncl = 0) AND (@IxIncl = 1)
                                BEGIN
                                    SET @IxIsIncl = 1
                                    SET @sCreateSql = @sCreateSql + @NewLine + ')' + @NewLine + 'INCLUDE' + @NewLine + '(' + @NewLine
                                END
                            ELSE
                                BEGIN
                                    SET @sCreateSql = @sCreateSql + ',' + @NewLine
                                END
                            --END IF
                        END
                    --END IF

                    SET @sCreateSql = @sCreateSql + @Tab + '[' + @IxColumn + ']'
                    -- check if ASC or DESC
                    IF @IxIsIncl = 0
                        BEGIN
                            IF @Desc = 1
                                BEGIN
                                    SET @sCreateSql = @sCreateSql + ' DESC'
                                END
                            ELSE
                                BEGIN
                                    SET @sCreateSql = @sCreateSql + ' ASC'
                                END
                            --END IF
                        END
                    --END IF
                    FETCH NEXT
                     FROM IndexColumns_cursor
                     INTO @IxColumn, @IxIncl, @Desc
                END
            --END WHILE
            CLOSE IndexColumns_cursor
            DEALLOCATE IndexColumns_cursor

            SET @sCreateSql = @sCreateSql + @NewLine + ') '

            IF @IncludeFillFactor = 1
                BEGIN
                    SET @sCreateSql = @sCreateSql + @NewLine + 'WITH (FillFactor = ' + Cast(@FillFactor as varchar(13)) + ')' + @NewLine
                END
            --END IF

            IF @IncludeFileGroup = 1
                BEGIN
                    SET @sCreateSql = @sCreateSql + 'ON ['+ @FileGroupName + ']' + @NewLine
                END
            ELSE
                BEGIN
                    SET @sCreateSql = @sCreateSql + @NewLine
                END
            --END IF
			
            PRINT '-- **********************************************************************'
            PRINT @sIndexDesc
            PRINT '-- **********************************************************************'

            IF @IncludeDrop = 1
                BEGIN
                    PRINT @sDropSql
                    --PRINT 'GO'
                END
            --END IF

            PRINT @sCreateSql
			PRINT 'PRINT ''EXECUTED: '+ @sIndexDesc+''''
			PRINT 'END' + @NewLine
            PRINT 'GO' + @NewLine  + @NewLine

            FETCH NEXT
             FROM Indexes_cursor
             INTO @SchemaName, @TableName, @TableId, @IndexName, @IndexId, @FileGroupName, @FillFactor
        END
    --END WHILE
    CLOSE Indexes_cursor
    DEALLOCATE Indexes_cursor
    
    
--**********************************************************************
-- Generate CREATE Index script for all indexes Script-2:
--**********************************************************************


declare @SchemaName varchar(100)
declare @TableName varchar(256)
declare @IndexName varchar(256)
declare @ColumnName varchar(100)
declare @is_unique varchar(100)
declare @IndexTypeDesc varchar(100)
declare @FileGroupName varchar(100)
declare @is_disabled varchar(100)
declare @IndexOptions varchar(max)
declare @IndexColumnId int
declare @IsDescendingKey int 
declare @IsIncludedColumn int
declare @TSQLScripCreationIndex varchar(max)
declare @TSQLScripDisableIndex varchar(max)

declare CursorIndex cursor for
 select schema_name(t.schema_id) [schema_name], t.name, ix.name,
 case when ix.is_unique = 1 then 'UNIQUE ' else '' END 
 , ix.type_desc,
 case when ix.is_padded=1 then 'PAD_INDEX = ON, ' else 'PAD_INDEX = OFF, ' end
 + case when ix.allow_page_locks=1 then 'ALLOW_PAGE_LOCKS = ON, ' else 'ALLOW_PAGE_LOCKS = OFF, ' end
 + case when ix.allow_row_locks=1 then  'ALLOW_ROW_LOCKS = ON, ' else 'ALLOW_ROW_LOCKS = OFF, ' end
 + case when INDEXPROPERTY(t.object_id, ix.name, 'IsStatistics') = 1 then 'STATISTICS_NORECOMPUTE = ON, ' else 'STATISTICS_NORECOMPUTE = OFF, ' end
 + case when ix.ignore_dup_key=1 then 'IGNORE_DUP_KEY = ON, ' else 'IGNORE_DUP_KEY = OFF, ' end
 + 'SORT_IN_TEMPDB = OFF, FILLFACTOR =' + CAST(ix.fill_factor AS VARCHAR(3)) AS IndexOptions
 , ix.is_disabled , FILEGROUP_NAME(ix.data_space_id) FileGroupName
 from sys.tables t 
 inner join sys.indexes ix on t.object_id=ix.object_id
 where ix.type>0 and ix.is_primary_key=0 and ix.is_unique_constraint=0 --and schema_name(tb.schema_id)= @SchemaName and tb.name=@TableName
 and t.is_ms_shipped=0 and t.name<>'sysdiagrams'
 order by schema_name(t.schema_id), t.name, ix.name

open CursorIndex
fetch next from CursorIndex into  @SchemaName, @TableName, @IndexName, @is_unique, @IndexTypeDesc, @IndexOptions,@is_disabled, @FileGroupName

while (@@fetch_status=0)
begin
 declare @IndexColumns varchar(max)
 declare @IncludedColumns varchar(max)
 
 set @IndexColumns=''
 set @IncludedColumns=''
 
 declare CursorIndexColumn cursor for 
  select col.name, ixc.is_descending_key, ixc.is_included_column
  from sys.tables tb 
  inner join sys.indexes ix on tb.object_id=ix.object_id
  inner join sys.index_columns ixc on ix.object_id=ixc.object_id and ix.index_id= ixc.index_id
  inner join sys.columns col on ixc.object_id =col.object_id  and ixc.column_id=col.column_id
  where ix.type>0 and (ix.is_primary_key=0 or ix.is_unique_constraint=0)
  and schema_name(tb.schema_id)=@SchemaName and tb.name=@TableName and ix.name=@IndexName
  order by ixc.index_column_id
 
 open CursorIndexColumn 
 fetch next from CursorIndexColumn into  @ColumnName, @IsDescendingKey, @IsIncludedColumn
 
 while (@@fetch_status=0)
 begin
  if @IsIncludedColumn=0 
   set @IndexColumns=@IndexColumns + @ColumnName  + case when @IsDescendingKey=1  then ' DESC, ' else  ' ASC, ' end
  else 
   set @IncludedColumns=@IncludedColumns  + @ColumnName  +', ' 

  fetch next from CursorIndexColumn into @ColumnName, @IsDescendingKey, @IsIncludedColumn
 end

 close CursorIndexColumn
 deallocate CursorIndexColumn

 set @IndexColumns = substring(@IndexColumns, 1, len(@IndexColumns)-1)
 set @IncludedColumns = case when len(@IncludedColumns) >0 then substring(@IncludedColumns, 1, len(@IncludedColumns)-1) else '' end
 --  print @IndexColumns
 --  print @IncludedColumns

 set @TSQLScripCreationIndex =''
 set @TSQLScripDisableIndex =''
 set @TSQLScripCreationIndex='CREATE '+ @is_unique  +@IndexTypeDesc + ' INDEX ' +QUOTENAME(@IndexName)+' ON ' + QUOTENAME(@SchemaName) +'.'+ QUOTENAME(@TableName)+ '('+@IndexColumns+') '+ 
  case when len(@IncludedColumns)>0 then CHAR(13) +'INCLUDE (' + @IncludedColumns+ ')' else '' end + CHAR(13)+'WITH (' + @IndexOptions+ ') ON ' + QUOTENAME(@FileGroupName) + ';'  

 if @is_disabled=1 
  set  @TSQLScripDisableIndex=  CHAR(13) +'ALTER INDEX ' +QUOTENAME(@IndexName) + ' ON ' + QUOTENAME(@SchemaName) +'.'+ QUOTENAME(@TableName) + ' DISABLE;' + CHAR(13) 

 print @TSQLScripCreationIndex
 print @TSQLScripDisableIndex

 fetch next from CursorIndex into  @SchemaName, @TableName, @IndexName, @is_unique, @IndexTypeDesc, @IndexOptions,@is_disabled, @FileGroupName

end
close CursorIndex
deallocate CursorIndex
