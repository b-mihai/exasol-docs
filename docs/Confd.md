# Confd

Get the usage of the confd job
```
confd_client -c help -a {confd_job}
```
List database parameters
```
confd_client -c db_info -a 'db_name: exasol'
```
Stop the database
```
confd_client -c db_stop -a 'db_name: exasol'
```
Start the database
```
confd_client -c db_start -a 'db_name: exasol'
```
Get state of the database
```
confd_client db_state db_name: exasol
```
Add an extra parameter to the database
```
confd_client -c db_configure -a '{db_name: exasol, params:"-forceProtocolEncryption=1"}'
```
Add a remote volume (AWS)
```
confd_client -c remote_volume_add -a '{url: https://bomi-v8.s3.us-east-1.amazonaws.com, vol_type: s3, username: AKIAS........A5Q, password: +CrRV2...........DQJrStUDHZ, owner: [500,500]}'
```
Add a remote volume (SMB)
```
confd_client -c remote_volume_add -a '{"vol_type":"smb","url":"smb:////10.144.35.139/Exasol_UAT","username":"USWIN\\SVC-SCRE_EXA_BKP", "password": "base64_encoded", "owner": [500,500], "options":["timeout=6000,cleanvolume"]}'
```
Start a database backup
```
confd_client -c db_backup_start -a '{db_name: exasol,backup_volume_name: r0001,level: 0}'
```
List database backups
```
confd_client -c db_backup_list -a 'db_name: exasol'
```
Create an archive volume with specific characteristics
```
confd_client st_volume_create -a '{"disk":"disk1","nodes":[11],"redundancy":1,"size":"100 MiB","type":"archive","owner":[500, 500],"name":"test_archive"}'
confd_client st_volume_create -a '{"disk":"disk1","nodes":[11,12,13,14],"redundancy":2,"size":"8 GiB","type":"archive","owner":[500, 500],"name":"archive"}'
```
Delete a volume
```
confd_client -c st_volume_delete –a '{vid: 0}'
```
Configure a backup schedule
```
confd_client -c db_backup_add_schedule -a '{db_name: exasol, backup_name: full backup, backup_volume_name: r0001, enabled: True, level: 0, expire: "1w 3d", minute: 0, hour: 1, day: "*", month: "*", weekday: 6}'
```
Restore a database
```
confd_client -c db_restore -a '{backup_id: 1 exa_db/id_1/level_0/node_0/backup_201811131114 exa_db, db_name: exasol, restore_type: blocking}'
```
Upload a new license
```
cat <license_file> | confd_client license_upload license: "\"{< -}\""
```
