--SQL Server script to take backup of all database 
DECLARE @DatabaseName	NVARCHAR (255); 
DECLARE @SQL NVARCHAR(4000); 
 
DECLARE DBBackupCur 
CURSOR FOR 
    SELECT name FROM sys.databases WITH (NOLOCK) 
    WHERE name NOT IN ('master','model','msdb','tempdb')  
    OPTION (RECOMPILE); 
 
OPEN DBBackupCur;     
FETCH NEXT FROM DBBackupCur INTO @DatabaseName 
WHILE (@@fetch_status <> -1) 
BEGIN 
    IF (@@fetch_status <> -2) 
    BEGIN 
	    -- 'C:\physicalPath\' with your physical path
        SET @SQL = N'BACKUP DATABASE [' + @DatabaseName + N'] TO DISK = ''C:\physicalPath\' + @DatabaseName + N'.bak'''; 
        EXECUTE sp_executesql @SQL 
        PRINT N'Backup completed: ' + @DatabaseName 
    END; 
    FETCH NEXT FROM DBBackupCur INTO @DatabaseName; 
END; 
CLOSE DBBackupCur; 
DEALLOCATE DBBackupCur; 
GO
