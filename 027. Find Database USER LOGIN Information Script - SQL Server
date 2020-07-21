-- 027. Find Database USER LOGIN Information Script - SQL Server 

SELECT 
	SL.name AS LoginName 
	,LOGINPROPERTY (SL.name, 'PasswordLastSetTime') AS PasswordLastSetTime 
	,LOGINPROPERTY (SL.name, 'DaysUntilExpiration') AS DaysUntilExpiration 
	,DATEADD(dd, CONVERT(int, LOGINPROPERTY (SL.name, 'DaysUntilExpiration')) 
				, CONVERT(datetime, LOGINPROPERTY (SL.name, 'PasswordLastSetTime'))) AS PasswordExpiration 
	,SL.is_policy_checked AS IsPolicyChecked 
	,LOGINPROPERTY (SL.name, 'IsExpired') AS IsExpired 
	,LOGINPROPERTY (SL.name, 'IsMustChange') AS IsMustChange 
	,LOGINPROPERTY (SL.name, 'IsLocked') AS IsLocked 
	,LOGINPROPERTY (SL.name, 'LockoutTime') AS LockoutTime 
	,LOGINPROPERTY (SL.name, 'BadPasswordCount') AS BadPasswordCount 
	,LOGINPROPERTY (SL.name, 'BadPasswordTime') AS BadPasswordTime 
	,LOGINPROPERTY (SL.name, 'HistoryLength') AS HistoryLength 
FROM sys.sql_logins AS SL 
WHERE is_expiration_checked = 1 
ORDER BY LOGINPROPERTY (SL.name, 'PasswordLastSetTime') DESC
