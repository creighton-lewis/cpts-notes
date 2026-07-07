# Active Directory 
## External Enumeration 
## Internal Enumeration 
```
Get-Module 
```

```
Import-Module ActiveDirectory 
Get-Module

```

``` 
Get-ADDomain 
```

```
Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName

```

```
Get-ADTrust -Filter * 

```

```
Get-ADGroup -Filter * | select name 
```


```
Get-ADGroup -Identity "Backup Operators"

```

## Lateral Movement 
## Privilege Escalation 
## Exploitation (from Linux)
## Exploitation (from Windows )