# OTHER

## DMIDECODE
Print various system information
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
```
dmidecode -t system
dmidecode -t bios
dmidecode -t memory
```
Check if system is barebone/physical or virtualized
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
```
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
