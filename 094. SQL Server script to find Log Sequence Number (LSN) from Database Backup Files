--******* 094. SQL Server script to find Log Sequence Number (LSN) from Database Backup Files



--When we have different transaction backup data, sometimes it is required to check LastLSN and FirstLSN of those files.
--If LSN sequence is not proper, then we cannot restore all database files in the series, and it generates an error like, LSN doesn’t match with the previous file.

--1. Using backupset table:
SELECT	 
	database_name
	,backup_size
	,first_lsn
	,last_lsn
	,checkpoint_lsn
	,database_backup_lsn
	,database_creation_date
	,backup_start_date
	,backup_finish_date	
FROM msdb.dbo.backupset


-- 2. Using sys.database_recovery_status:

SELECT 
	last_log_backup_lsn
FROM sys.database_recovery_status
WHERE database_id = DB_ID()


-- 3. Using fn_dblog():
--It returns all information about the log data, and it contains two parameters, first is starting LSN and the second is ending LSN.
--You can pass NULL for all the records.

SELECT 
	last_log_backup_lsn
FROM sys.database_recovery_status
WHERE database_id = DB_ID()

-- 4. Using Restore with HeaderOnly option:
--You can specify file name and path of the backup files, and it returns all information related to that backup file.

RESTORE HEADERONLY FROM DISK = 'C:\Temp\FullBackupFileNname.bak'
RESTORE HEADERONLY FROM DISK = 'C:\Temp\TranFilePath.trn'
