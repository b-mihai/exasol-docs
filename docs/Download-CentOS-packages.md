On the Internet-connected Machine:
1. Install yum-utils
```
sudo yum install yum-utils
```
2. Create a Directory for Downloads
```
mkdir package_downloads
cd package_downloads
```
3. Download the Package and Dependencies
```
repoquery --requires --resolve --recursive package_name | xargs -i yumdownloader {}
```
4. Copy pacakges to the Offline machine
```
rsync -avz --progress /source/directory user@ServerB:/destination/directory
```

On the Offline Machine:
1. Navigate to the Directory Containing the Packages
```
cd /path/to/package_downloads
```
2. Install the Package and Dependencies:
```
sudo yum localinstall *.rpm
sudo dnf install *.rpm
```
