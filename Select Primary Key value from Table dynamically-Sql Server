
CREATE PROCEDURE [dbo].[select_id_from_tablename]
	-- Add the parameters for the stored procedure here
	@tablename VARCHAR(50),
	@tblcolumnnm VARCHAR(50)='',
	@tblvaluecompare varchar(100)=''	
AS
BEGIN
	-- SET NOCOUNT ON added to prevent extra result sets from
	-- interfering with SELECT statements.
	SET NOCOUNT ON;
	
	DECLARE @CONTRAINTNAME VARCHAR(100);
	DECLARE @QUERY VARCHAR(MAX);
	DECLARE @COLUMNNAME VARCHAR(MAX);
	
	SELECT @CONTRAINTNAME = CONSTRAINT_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE CONSTRAINT_TYPE='PRIMARY KEY'
	AND TABLE_NAME = @tablename
	
	SELECT @COLUMNNAME = COLUMN_NAME FROM INFORMATION_SCHEMA.CONSTRAINT_COLUMN_USAGE WHERE CONSTRAINT_NAME = @CONTRAINTNAME

    SET @QUERY = 'SELECT '+@COLUMNNAME+' FROM '+@tablename +' WHERE '+@tblcolumnnm+' = '+''''+@tblvaluecompare+'''';
    
    print @QUERY
    
    exec(@QUERY)
     
END
