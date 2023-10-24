# Other

## DMIDECODE
Print various system information
```
Valid type keywords:
  bios
  system
  baseboard
  chassis
  processor
  memory
  cache
  connector
  slot

dmidecode -t system
dmidecode -t bios
dmidecode -t memory
```
Check if system is barebone/physical or virtualized
```
Valid strings keywords:
  bios-vendor
  bios-version
  bios-release-date
  system-manufacturer
  system-product-name
  system-version
  system-serial-number
  system-uuid
  system-family
  baseboard-manufacturer
  baseboard-product-name
  baseboard-version
  baseboard-serial-number
  baseboard-asset-tag
  chassis-manufacturer
  chassis-type
  chassis-version
  chassis-serial-number
  chassis-asset-tag
  processor-family
  processor-manufacturer
  processor-version
  processor-frequency

dmidecode -s system-manufacturer
dmidecode -s processor-frequency
```

## PROC
Check memory allocation
```
cat /proc/meminfo
```
Check CPU info
```
cat /proc/cpuinfo
```

## TOP
* Cycles through different memory units in 'top' (KiB, MiB, GiB) pressing 'E'

* Check Swap usage 
1. Run the TOP command
2. On your keyboard press the “f” key and scroll down using the [down] arrow key until you have selected “SWAP” then press [Space] to select it. This should add a “*” symbol in front of it.
3. While still selecting “SWAP” press the [right] arrow key, which highlights the entire SWAP line, and using the [top] arrow key move it up to one of the first options (anywhere above “COMMAND”).
4. While still having “SWAP” selected, type the “s” key which will configure top to SORT by the currently selected option, in this case, SWAP. You will not see any changes on the screen when you press “s”, but the setting is saved in the backend.
5. Finally “q” to save the configuration changes and view the results.

## TAR
Open a log file (without extracting) from tar.gz archive
```
tar -Oxvf filename.tar.gz /path/to/file.log | less
```
View contents of a tar.gz archive
```
tar -tf filename.tar.gz | less
```
Extract just one file from a tar.gz archive
```
tar -zxvf filename.tar.gz  /path/to/file_name
```
Extract tar.gz files creating a directory with the same name as the archive and excluding the Sql Sessions and Server logs
```
find . -name "*.tar.gz" -execdir tar --exclude='*Sql*' --one-top-level -xvzf {} \;
```
