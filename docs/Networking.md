# Networking

## Use OMNI calculator if needed
https://www.omnicalculator.com/other/bandwidth

## IPERF3
Start `iperf` on 'destination' server
```
iperf3 -s -p 60000
```
Test the connection from 'source' server
```
iperf3 -c {dest_ip} -p 60000
```

## NCAT
### Start `ncat` on 'destination' server
```
nc -l 60000
```
### Create a dummy file and the connection from 'source' server
```
dd if=/dev/zero bs=1M count=1024 | nc {dest_ip} 60000
```

### 
