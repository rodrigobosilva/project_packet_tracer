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
ip address 10.168.17.1 255.255.255.252
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
access-list 1 permit 10.168.17.0 0.0.0.255 
access-list 1 permit 10.17.10.0 0.0.0.255
access-list 1 permit 10.17.20.0 0.0.0.255
access-list 1 permit 10.17.30.0 0.0.0.255
access-list 1 permit 10.17.40.0 0.0.0.255
access-list 1 permit 10.17.50.0 0.0.0.255
```
```
ip nat inside source list 1 interface s0/0/0 overload
ip nat inside source static tcp 10.17.40.254 80 1.0.0.6 80
ip nat inside source static tcp 10.168.17.254 443 1.0.0.6 443
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
