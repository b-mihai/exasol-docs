# iDRAC

## IPMITOOL
Restart (Warm) the iDRAC
```
ipmitool mc reset warm
```
List System Event Log
```
ipmitool sel list
```
Clear System Event Log
```
ipmitool sel clear
```
Check status of IPMI remotely
```
ipmitool -I lanplus -U {user} -P {pass} -H {idrac_IP} chassis power status
```

## RACADM
Reset - This reboots the iDRAC without changing any iDRAC configuration settings.
```
racadm racreset
```
Get the System Event Log
```
racadm getsel
```
Display all the available records from the active Lifecycle log.
```
racadm lclog view
```
Display the number of records present in the Lifecycle log.
```
racadm lclog view -i
```
Display the iDRAC agent idrac records, under the storage category and storage physical disk drive subcategory, with severity set to warning.
````
racadm lclog view -a idrac -c storage -b pdr -s warning
````
Display the records under storage and system categories with severities set to warning or critical.
```
racadm lclog view -c storage,system -s warning,critical
```
Display the records having severities set to warning or critical, starting from sequence number 4.
```
racadm lclog view -s warning,critical -q 4
```
Display 5 records starting from sequence number 20.
```
racadm lclog view -q 20 -n 5
```
Display all records of events that have occurred between 2011-01-02 23:33:40 and 2011-01-03 00:32:15.
```
racadm lclog view -r "2023-02-09 00:00:00" -e "2023-02-10 16:00:00"
```
Get Power profile from BIOS
```
racadm get BIOS.SysProfileSettings
```
Rollback an iDRAC firmware update
```
racadm rollback iDRAC.Embedded.1-1
```
