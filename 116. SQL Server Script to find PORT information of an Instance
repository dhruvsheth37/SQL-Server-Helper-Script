-- 116. SQL Server Script to find PORT information of an Instance

SET NOCOUNT ON
DECLARE 
	@Port VARCHAR(30)
	,@Key VARCHAR(150)
IF CHARINDEX('\',@@SERVERNAME,0) <>0
BEGIN 
	SET @Key = 'SOFTWARE\MICROSOFT\Microsoft SQL Server\'
				+@@SERVICENAME+'\MSSQLServer\Supersocketnetlib\TCP'
END
ELSE
BEGIN 
	SET @Key = 'SOFTWARE\MICROSOFT\MSSQLServer\MSSQLServer \Supersocketnetlib\TCP'
END 
EXEC master.sys.xp_regread 
	@Rootkey='HKEY_LOCAL_MACHINE'
	,@Key=@Key,@value_name='Tcpport'
	,@value=@Port OUTPUT
 
SELECT 'SQL Server Name: '+@@SERVERNAME + ' Port # '+CONVERT(VARCHAR(20),@Port)
