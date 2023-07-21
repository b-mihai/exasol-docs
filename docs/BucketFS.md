# BucketFS

## Restart BucketFS in NGA
Restart bucketfsd, using 'cosrst' (Recommended)
```
cosrst {PID} {NID}
```
Restart bucketfsd, using 'coskillall'. This method is not the best, but it will do the trick, having the same PID, FLAGS, and COMMAND name.
```
coskillall -9 bucketfsd-bfsdefault
```
Restart bucketfsd, removing the PID. This method will start bucketfsd with the correct UID/GID, name, and other parameters.
```
cosrm -a {PID}
exaconf commit
```
## Restart BucketFS on an EXAopeartion deployment
```
coskillall appserverd
```

## Upload files from OUTSIDE the container
The default path for JDBC drivers is `/default/drivers/jdbc/jdbcNN/`

Get the read password of the bucketfs
```
readp=$(echo $(grep ReadPasswd /opt/exa/etc/EXAConf|awk '{print $3}')|base64 -d)
```
Get the read password of the bucketfs
```
writep=$(echo $(grep WritePasswd /opt/exa/etc/EXAConf|awk '{print $3}')|base64 -d)
```
Get the bucketfs HTTP port
```
http_port="$(grep HttpPort /opt/exa/etc/EXAConf | awk '{print $3}')"
https_port="$(grep HttpsPort /opt/exa/etc/EXAConf | awk '{print $3}')"
```

## Upload files from INSIDE the container
Verify in which bucketfs (eg. bfsdefault) you want to copy the file
```
confd_client -c bucketfs_list
```
Check the bucketfs info
```
confd_client -c bucketfs_info -a 'bucketfs_name: bfsdefault'
```
Get the read password of the bucketfs
```
readp=$(echo $(confd_client -c bucketfs_info -a 'bucketfs_name: bfsdefault' | grep read_passwd | awk '{print $2}') | base64 -d)
```
Get the read password of the bucketfs
```
writep=$(echo $(confd_client -c bucketfs_info -a 'bucketfs_name: bfsdefault' | grep write_passwd | awk '{print $2}') | base64 -d)
```
Get the bucketfs port
```
http_port=$(confd_client -c bucketfs_info -a 'bucketfs_name: bfsdefault' | grep http_port | awk '{print $2}')
https_port=$(confd_client -c bucketfs_info -a 'bucketfs_name: bfsdefault' | grep https_port | awk '{print $2}')
```
Read the contents of the bucket (bfsdefault)
```
curl http://r:$readp@localhost:$http_port/default
```
Upload files to the bucket (bfsdefault) using HTTP port
```
file=standard-EXASOL-7.1.0_release.tar.gz
curl -v -X PUT -T $file http://w:$writep@localhost:$http_port/default/EXAClusterOS/$file
```
Upload files to the bucket (bfsdefault) using HTTPS port
```
file=standard-EXASOL-7.1.0_release.tar.gz
curl -kv -X PUT -T $file http://w:$writep@localhost:$http_port/default/EXAClusterOS/$file
```
If you got issues, check the bucketfs log
```
less $(ls /exa/logs/cored/*bucketfsd*|grep bucketfsd|tail -1)
```
Check if the file got synced to the rest of the nodes
```
psh 'ls -lh /exa/data/bucketfs/bfsdefault/default/EXAClusterOS*'
```
