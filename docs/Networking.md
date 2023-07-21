# Networking

## IP LINK
Set interface state to 'down'
```
ip link set dev {intf_name} down
```
Set interface state to 'up'
```
ip link set dev {intf_name} up
```
Rename an interface
```
ip link set {OLD_intf_name} name {NEW_intf_name}
```
Change the active slave on an active-backup bond
```
ip link set dev {bond_name} type bond active_slave {intf_name}
```

## BONDS
Create an active-backup bond interface
```
ip link add name bond0 type bond mode active-backup
ip link set master bond0 dev eth1
ip link set master bond0 dev eth0
ip link set up dev bond0
ip address add 192.168.100.1/24 dev bond0
```
Check detailed info and statistics of bond0
```
ip -s -s -d link ls dev bond0
```
Check the state of ALL under-laying interfaces
```
ip -s -s -d link ls master bond0
```

## IFTOP
Monitor the network traffic to a specific destination address
```
iftop -i {intf_name} -F {ip_address/24} -B
```

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
Start `ncat` on 'destination' server
```
nc -l 60000
```
Create a dummy file and the connection from 'source' server
```
dd if=/dev/zero bs=1M count=1024 | nc {dest_ip} 60000
```
## Check if a port is listening 
Using 'nc'
```
nc -zv {ip} {port}
```
Using 'ss'
```
ss -antp | grep {port}
```
Using 'netstat'
```
netstat -anp | grep {port}
```

## Download files using 'curl'
```
curl -k -X GET  https://{link} --output {file_name}
```
