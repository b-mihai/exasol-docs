Extract a tar.gz file in one step
```
gunzip -c file.tar.gz | tar xvf –
```

List the contents of a tar.gz file
```
tar -ztvf file.tar.gz
```

Check available disk space
```
df -Pm |sort -n -k 5 |tail -5
```
```
df -gMI | sort -n +3 | egrep '9.%|100%'
```
```
df -h | sort -k 5 | egrep '9.%|100%'
```

Check what services are running
```
systemctl list-units --type=service | grep running
systemctl list-units --type=service --state=running
systemctl list-units --type=service | grep failed
systemctl list-units --type=service --all
journalctl -b -u systemd-logind
systemctl --failed 
systemctl --all --failed
systemctl list-unit-files | grep enabled
systemctl | grep running
systemctl enable httpd
```
Resize a filesystem
```
lvresize -L +100M -r /dev/mapper/rootvg-varvol
```
Create a new LV
```
lvcreate -n lvname -L 500M vgname
```
Various 'find' commands
```
find / -type f -size +100M -exec ls -lh {} \; | sort -k 5 -rh | head -n 10
du -sh /var/* | sort -rh | head -n 20
find . -xdev -type f -exec du -sm '{}' \; | sort -n | tail -20
find . -xdev -type f -mtime +90 -exec ls -l {} \;
find . -xdev -type d -mtime +90 -exec ls -ld {} \;
find . -xdev -type f -name "*log*" -mtime +90 -exec ls -l {} \;
find . -xdev -type f -name "*log*" -mtime +90 -exec gzip -9 {} \;
find . -xdev -name "file_type_or_name" -type f -mtime +90 -exec ls -l {} \; > log_file 2>&1
find . -xdev -name "file_type_or_name" -type f -mtime +90 -exec rm -f {} \; > log_file 2>&1
find . -xdev -name "file_type_or_name" -type f -mtime +90 -exec ls -l {} \; -exec rm -f {} \; > log_file 2>&1
find . -xdev -type f -ls | sort +6n | tail -n 10
find . -type f -size 0 -ls
find . -print | sed -e 's;[^/]*/;|;g;s;|; |;g'
find . -type d -print | sed -e 's;[^/]*/;|;g;s;|; |;g'
find . -user username
find . -user username -exec rm -r {} \;
find . -size +2048 -mtime +30 -exec ls -l {} \;
find . -exec ls -la {} \; | awk '{ if ( $8==2016) printf $0"\n" }'
```
Create dummy files
```
dd if=/dev/zero of=/tmp/zero.file bs=1M count=10
dd if=/dev/random of=/tmp/zero.file bs=1M count=10
dd if=/dev/urandom of=/tmp/zero.file bs=1M count=10
dd if=/dev/zero of=/tmp/zero.file
```
Archive a log file
```
LOG=WHATEVER_YOU_WANT
cat ${LOG} | gzip -9 > /tmp/${LOG}_$(date +%Y%m%d).gz && cat /dev/null > ${LOG} && mv /tmp/${LOG}_$(date +%Y%m%d).gz .
```
Forward a port
```
ssh root@license-prod -L 8443:10.6.252.31:443 -L 17990:10.6.252.31:17990
https://localhost:8443/
```
List all installed packages
```
dpkg -l
```
List details about a package
```
dpkg -s <package_name>
```
