# Linux Capabilities 
- Capabilities granted to specific programs that may occassionally contain excessive privileges
**Enumeration**
  
```
find /usr/bin /usr/sbin /usr/local/bin /usr/local/sbin -type f -exec getcap {} \;
```
Linux Capabilities that can be abused: 
- cap_dac_override
- cap_sys_admin
- cap_audit_control
- cap_audit_write
- cap_chown
# Cron Jobs 
# Containers 
## Docker 
## Polki 
## Kubernates 
## Logrotate 
## Misc 
