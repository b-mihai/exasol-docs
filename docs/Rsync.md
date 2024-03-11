Sync/copy one file from ServerA to ServerB
```
rsync -avz --progress /source/directory user@ServerB:/destination/directory
```
Sync with an SSH key pair
```
rsync -avz --progress -e "ssh -i /path/to/private_key" /source/directory user@ServerB:/destination/directory
```
