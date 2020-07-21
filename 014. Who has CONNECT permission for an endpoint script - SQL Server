When we install SQL Server, SQL Server requires some of permissions like TSQL Local Machine, TSQL Named Pipes, TSQL Default TCP and TSQL Default VIA, by which other clients could also access SQL Server.

-- 014. Who has CONNECT permission for an endpoint script - SQL Server

SELECT EP.name, SP.STATE,   
   CONVERT(nvarchar(38), suser_name(SP.grantor_principal_id))   
      AS GRANTOR,   
   SP.TYPE AS PERMISSION,  
   CONVERT(nvarchar(46),suser_name(SP.grantee_principal_id))   
      AS GRANTEE   
   FROM sys.server_permissions SP , sys.endpoints EP  
   WHERE SP.major_id = EP.endpoint_id  
   ORDER BY Permission,grantor, grantee;   
GO  
