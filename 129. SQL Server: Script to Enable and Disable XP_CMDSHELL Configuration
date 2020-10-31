-- 129. SQL Server: Script to Enable and Disable XP_CMDSHELL Configuration

-- First, Check XP_CMDSHELL is enabled on the server:
SELECT CONVERT(INT, ISNULL(value, value_in_use)) AS ConfigValue
FROM sys.configurations
WHERE name = 'xp_cmdshell' ;


-- Script to enable and disable XP_CMDSHELL:
 
-- Enable advanced options to be changed.
EXEC SP_CONFIGURE 'show advanced options', 1
GO
RECONFIGURE
GO
-- Enable xp_cmdshell option.
EXEC SP_CONFIGURE N'xp_cmdshell', 1
GO
RECONFIGURE
GO
-- Disable xp_cmdshell option. 
EXEC SP_CONFIGURE 'xp_cmdshell', 0
GO
RECONFIGURE
GO
-- Disable advanced options to be changed.
EXEC SP_CONFIGURE 'show advanced options', 0
GO
RECONFIGURE
GO
