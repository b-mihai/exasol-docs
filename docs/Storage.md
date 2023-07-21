# Storage

## CSINFO
Print summary of volume information
```
csinfo
```
Print all volume information
```
csinfo -v
```
Print volume information for a specific vol. id
```
csinfo -v -i {vol_id}
```
Print volume segment information
```
csinfo -v -i {vol_id} -l2
```
Show HDD state
```
csinfo -H
```
Show HDD state
```
csinfo -H
```
Print HDD info
```
csinfo -D
```

## SDFS
List contents of the remote archive volume
```
sdfs list {vol_id}
```
Add one or more files to the volume
```
sdfs add {vol_id} {exp_date} {file}
```
Add data from stdin as new file to SDFS
```
sdfs addraw {vol_id} {exp_date} {file}
``` 
Remove file(s) from volume (or only mark as deleted if there is enough space)
```
sdfs remove {vol_id} -r {file}
```
Copy a file between archive volumes
```
sdfs getraw (vol_id} {file} | sdfs addraw {vol_id} {exp_date} {file}
```
Copy a file between archive volumes
```
sdfs rename (vol_id} {old_file_name} {new_file_name}
```

## CSCTRL
Stop storage services
```
csctrl -d
```
Suspend storage
```
csctrl -u
```
Start storage services on NGA
```
csctrl -s -A -R -n 11,12 -c /exa/etc/cos_storage.conf
```
Start storage services on non-NGA
```
csctrl -s -A -R -n 11,12 -c /usr/opt/EXASuite-7/EXAClusterOS-7.1.21/etc/cos_storage.conf
```

## CSVOL
Drop/delete a volume
```
csvol -d -v {vol_id}
```
Create a volume with specific attributes
```
csvol -c -s 7 -b 4 -S 256 -r 1 -h disk1 -p rwx------ -m 5 -C -H -P 10 -B VERTICAL
```
Rename a volume
```
csvol -v 0 -y -I {vol_name}
```
Set disk permissions to specific user
```
csvol -v 0 -O -U {user} -G {group}
```
Lock a volume
```
csvol -l -v {vol_id}
```
Unlock a volume
```
csvol -L -v {vol_id}
```

## CSREC, CSHDD, CSTOP
View the storage recovery process
```
csrec -s -v {vol_id}
```
Enable an OFFLINE disk
```
cshdd -e -h /dev/mapper/... -n 11
```
Monitor cluster performance
```
cstop
```
