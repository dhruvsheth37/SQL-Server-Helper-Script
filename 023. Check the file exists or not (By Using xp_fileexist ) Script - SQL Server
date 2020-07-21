-- 023. Check the file exists or not (By Using xp_fileexist ) Script - SQL Server
 
DECLARE @IsFileExists INT
EXEC Master.dbo.xp_fileexist 'D:\TechnoThirsty.txt', @IsFileExists OUT 
IF @IsFileExists = 1
BEGIN
	PRINT 'File Exists...'
END
ELSE
BEGIN
	PRINT 'File Does not Exists...'
END
