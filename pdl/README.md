### Router PDL
```
int s0/0/0
no shutdown
ip address 1.0.0.2 255.255.255.252
ip nat outside
exit
```
```
int s0/0/1
no shutdown
ip address 192.168.17.6 255.255.255.252
ip nat inside
exit
```
```
int s0/1/0
no shutdown
ip address 192.168.17.18 255.255.255.252
ip nat inside
exit
```
```
int f0/0
no shutdown
ip address 10.168.17.1 255.255.255.0
ip nat inside
exit
```
```
router ospf 100
network 192.168.17.4 0.0.0.3 area 0
network 192.168.17.16 0.0.0.3 area 0
network 10.168.17.0 0.0.0.255 area 0
default-information originate 
passive-interface s0/0/0
passive-interface f0/0
redistribute rip 100 metric 3 
exit
```
```
ip route 0.0.0.0 0.0.0.0 s0/0/0
```
```
access-list 1 permit 10.0.0.0 0.255.255.255 
access-list 1 permit 172.16.0.0 0.15.255.255
access-list 1 permit 192.168.0.0 0.0.255.255
```
```
ip nat inside source list 1 interface s0/0/0 overload
ip nat inside source static tcp 10.17.40.254 80 1.0.0.2 80
ip nat inside source static tcp 10.168.17.254 443 1.0.0.2 443
```
```
do write
```
### Router PDL1
```
int s0/0/0
no shutdown
ip address 192.168.17.2 255.255.255.252
exit
```
```
int s0/0/1
no shutdown
ip address 192.168.17.5 255.255.255.252
exit
```
```
int s0/1/0
no shutdown
ip address 192.168.17.17 255.255.255.252
exit
```
```
int s0/1/1
no shutdown
ip address 192.168.17.22 255.255.255.252
exit
```
```
int f0/0
no shutdown
ip address 10.17.40.2 255.255.255.0
description Network Servers
exit
```
```
int f0/1
no shutdown
exit
```
```
int f0/1.10
encapsulation dot1Q 10
ip address 10.17.10.2 255.255.255.0
description Network GRSI
exit
```
```
int f0/1.20
encapsulation dot1Q 20
ip address 10.17.20.2 255.255.255.0
description Network TGRI
exit
```
```
int f0/1.30
encapsulation dot1Q 30
ip address 10.17.30.2 255.255.255.0
description Network TQA
exit
```
```
int f0/1.50
encapsulation dot1Q 50
ip address 10.17.50.2 255.255.255.0
description Network VoIP
exit
```
```
router ospf 100
network 192.168.17.0 0.0.0.3 area 0
network 192.168.17.4 0.0.0.3 area 0
network 192.168.17.16 0.0.0.3 area 0
network 192.168.17.20 0.0.0.3 area 0
passive-interface f0/0
passive-interface f0/1.10
passive-interface f0/1.20
passive-interface f0/1.30
passive-interface f0/1.50
exit
```
```
do write
```

### Router PDL2
```
int s0/0/0
no shutdown
ip address 1.0.0.10 255.255.255.252
ip nat outside 
exit
```
```
int s0/0/1
no shutdown
ip address 192.168.17.1 255.255.255.252
ip nat inside
exit
```
```
int s0/1/0
no shutdown
ip address 192.168.17.21 255.255.255.252
ip nat inside
exit
```
```
int f0/0
no shutdown
ip address 10.17.40.1 255.255.255.0
description Network Servers
ip nat inside
ip helper-address 192.168.17.22
exit
```
```
int f0/1
no shutdown
exit
```
```
int f0/1.10
encapsulation dot1Q 10
ip address 10.17.10.1 255.255.255.0
description Network GRSI
ip nat inside
ip helper-address 192.168.17.22
exit
```
```
int f0/1.20
encapsulation dot1Q 20
ip address 10.17.20.1 255.255.255.0
description Network TGRI
ip nat inside
ip helper-address 192.168.17.22
exit
```
```
int f0/1.30
encapsulation dot1Q 30
ip address 10.17.30.1 255.255.255.0
description Network TQA
ip nat inside
ip helper-address 192.168.17.22
exit
```
```
int f0/1.50
encapsulation dot1Q 50
ip address 10.17.50.1 255.255.255.0
description Network VoIP
ip nat inside
ip helper-address 192.168.17.22
exit
```
```
router ospf 100
network 192.168.17.0 0.0.0.3 area 0
network 192.168.17.20 0.0.0.3 area 0
network 10.17.10.0 0.0.0.3 area 0
network 10.17.20.0 0.0.0.3 area 0
network 10.17.30.0 0.0.0.3 area 0
network 10.17.40.0 0.0.0.3 area 0
network 10.17.50.0 0.0.0.3 area 0
default-information originate 
passive-interface s0/0/0
passive-interface f0/0
passive-interface f0/1.10
passive-interface f0/1.20
passive-interface f0/1.30
passive-interface f0/1.50
exit
```
```
ip route 0.0.0.0 0.0.0.0 s0/0/0
```
```
access-list 1 permit 10.0.0.0 0.255.255.255 
access-list 1 permit 172.16.0.0 0.15.255.255
access-list 1 permit 192.168.0.0 0.0.255.255
```
```
ip nat inside source list 1 interface s0/0/0 overload
```
```
do write
```
### Server-PT HTTPS
* IP Configuration
* Static

| Camp  | Value |
| ------------- | ------------- |
| IPv4 Address | `10.168.17.254` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `10.168.17.1` |
| DNS Server | `10.168.17.254` |

### Server-PT V40 HTTP
* IP Configuration
* Static

| Camp  | Value |
| ------------- | ------------- |
| IPv4 Address | `10.17.40.254` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `10.17.40.253` |
| DNS Server | `10.168.17.254` |

## VLANS
### SWPDL2 & SWPDL3
```
vtp mode server
vtp domain pdl.pt
vtp password Passw0rd
```
### SWPDL1, SWPDL4 & SWPDL5
```
vtp mode client
vtp domain pdl.pt
vtp password Passw0rd
```
### SWPDL2
```
vlan 10
name grsi
exit
vlan 20
name tgri
exit
vlan 30
name tqa
exit
vlan 40
name servers
exit
vlan 50
name voip
exit
```
```
int range f0/1-3
switchport mode trunk
exit
int f0/4
switchport mode access
switchport access vlan 10
exit
int f0/5
switchport mode access
switchport access vlan 20
exit
int f0/6
switchport mode access
switchport access vlan 30
exit
```
```
spanning-tree vlan 20 root secondary
spanning-tree vlan 30 root primary
```
### SWPDL1
```
int range f0/1-3
switchport mode trunk
exit
int f0/4
switchport mode trunk
switchport trunk allowed vlan 10
switchport trunk allowed vlan add 20
switchport trunk allowed vlan add 30
switchport trunk allowed vlan add 50
exit
int f0/5
switchport mode access
switchport access vlan 40
exit
```
```
spanning-tree vlan 10 root secondary
spanning-tree vlan 20 root primary
```
### SWPDL3
```
int range f0/1-3
switchport mode trunk
exit
int f0/4
switchport mode access
switchport access vlan 10
exit
int f0/5
switchport mode access
switchport access vlan 20
exit
int f0/6
switchport voice vlan 50
exit
```
```
spanning-tree vlan 30 root secondary
spanning-tree vlan 40 root primary
```
### SWPDL5
```
int f0/1
switchport mode trunk
switchport trunk allowed vlan 10
switchport trunk allowed vlan add 20
switchport trunk allowed vlan add 30
switchport trunk allowed vlan add 50
exit
int f0/4
switchport mode access
switchport access vlan 40
exit
int f0/5
switchport mode access
switchport access vlan 40
exit
int f0/8
switchport voice vlan 50
int range f0/2-3
switchport mode trunk
channel-protocol lacp
channel-group 1 mode active
int range f0/6-7
switchport mode trunk
channel-protocol lacp
channel-group 1 mode active
exit
```
```
spanning-tree vlan 50 root secondary
spanning-tree vlan 10 root primary
```
### SWPDL4
```
int range f0/1-3
switchport mode trunk
exit
int f0/4
switchport mode access
switchport access vlan 20
exit
int f0/5
switchport mode access
switchport access vlan 30
exit
int range f0/6-9
switchport mode trunk
channel-protocol lacp
channel-group 1 mode active
exit
```
```
spanning-tree vlan 40 root secondary
spanning-tree vlan 50 root primary
```

## HRSP
### PDL2
```
int f0/0
standby version 2
standby 40 ip 10.17.40.253
standby 40 priority 105
standby 40 preempt
exit
```
```
int f0/1.10
standby 10 ip 10.17.10.253
standby 10 priority 105
standby 10 preempt
exit
```
```
int f0/1.20
standby 20 ip 10.17.20.253
standby 20 priority 105
standby 20 preempt
exit
```
```
int f0/1.30
standby 30 ip 10.17.30.253
standby 30 priority 105
standby 30 preempt
exit
```
```
int f0/1.50
standby 50 ip 10.17.50.253
standby 50 priority 105
standby 50 preempt
exit
```
### PDL1
```
int f0/0
standby version 2
standby 40 ip 10.17.40.253
standby 40 priority 100
standby 40 preempt
exit
```
```
int f0/1.10
standby 10 ip 10.17.10.253
standby 10 priority 100
standby 10 preempt
exit
```
```
int f0/1.20
standby 20 ip 10.17.20.253
standby 20 priority 100
standby 20 preempt
exit
```
```
int f0/1.30
standby 30 ip 10.17.30.253
standby 30 priority 100
standby 30 preempt
exit
```
```
int f0/1.50
standby 50 ip 10.17.50.253
standby 50 priority 100
standby 50 preempt
exit
```
## DHCP
### PDL1
```
ip dhcp excluded-address 10.17.10.1 10.17.10.2
ip dhcp excluded-address 10.17.10.253 10.17.10.254
ip dhcp excluded-address 10.17.20.1 10.17.20.2
ip dhcp excluded-address 10.17.20.253 10.17.20.254
ip dhcp excluded-address 10.17.30.1 10.17.30.2
ip dhcp excluded-address 10.17.30.253 10.17.30.254
ip dhcp excluded-address 10.17.50.1 10.17.50.2
ip dhcp excluded-address 10.17.50.253 10.17.50.254
```
```
ip dhcp pool vlan10
network 10.17.10.0 255.255.255.0
default-router 10.17.10.253
option 150 ip 192.168.17.22
dns-server 10.168.17.254
exit
ip dhcp pool vlan20
network 10.17.20.0 255.255.255.0
default-router 10.17.20.253
option 150 ip 192.168.17.22
dns-server 10.168.17.254
exit
ip dhcp pool vlan30
network 10.17.30.0 255.255.255.0
default-router 10.17.30.253
option 150 ip 192.168.17.22
dns-server 10.168.17.254
exit
ip dhcp pool vlan50
network 10.17.50.0 255.255.255.0
default-router 10.17.50.253
option 150 ip 192.168.17.22
dns-server 10.168.17.254
exit
```
```
telephony-service
max-ephones 10
max-dn 10
ip source-address 192.168.17.22 port 2000
auto assign 1 to 10
exit
```
```
ephone-dn 1
number 101
exit
ephone-dn 2
number 102
exit
ephone-dn 3
number 111
exit
ephone-dn 4
number 112
exit
ephone-dn 5
number 121
exit
ephone-dn 6
number 122
exit
ephone-dn 7
number 123
exit
ephone-dn 8
number 131
exit
ephone-dn 9
number 132
exit
```
