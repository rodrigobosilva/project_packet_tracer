### Router Angra
```
int s0/0/0
no shutdown
ip address 1.0.0.6 255.255.255.252
ip nat outside
exit
```
```
int s0/0/1
no shutdown
ip address 192.168.17.9 255.255.255.252
ip nat inside
exit
```
```
router eigrp 100
network 192.168.17.8 0.0.0.3
no auto-summary
passive-interface s0/0/0
redistribute rip 100 metric 3 1 255 255 10
exit
```
```
ip route 0.0.0.0 0.0.0.0 s0/0/0
```
```
ip route 10.168.17.0 255.255.255.0 10.255.255.1
ip route 10.17.10.0 255.255.255.0 10.255.255.1
ip route 10.17.20.0 255.255.255.0 10.255.255.1
ip route 10.17.30.0 255.255.255.0 10.255.255.1
ip route 10.17.40.0 255.255.255.0 10.255.255.1
ip route 10.17.50.0 255.255.255.0 10.255.255.1
```
```
access-list 1 permit 172.16.17.0 0.0.0.255 
access-list 1 permit 172.17.17.0 0.0.0.255
access-list 1 permit 172.18.17.0 0.0.0.255
access-list 1 permit 172.20.17.0 0.0.0.255
```
```
ip nat inside source list 1 interface s0/0/0 overload
ip nat inside source static tcp 172.18.17.254 80 1.0.0.6 80
ip nat inside source static tcp 172.18.17.254 443 1.0.0.6 443
```
### Router Angra1
```
int s0/0/0
no shutdown
ip address 192.168.17.10 255.255.255.252
exit
```
```
int s0/0/1
no shutdown
ip address 192.168.17.13 255.255.255.252
exit
```
```
int f0/0
no shutdown
ip address 172.16.17.1 255.255.255.0
exit
```
```
router eigrp 100
network 192.168.17.8 0.0.0.3
network 192.168.17.12 0.0.0.3
network 172.16.17.0 0.0.0.255
no auto-summary
passive-interface f0/0
```
### Router Angra2
```
int s0/0/0
no shutdown
ip address 192.168.17.14 255.255.255.252
exit
```
```
int f0/1
no shutdown
ip address 172.18.17.1 255.255.255.0
exit
```
```
int f0/0
no shutdown
exit
```
```
int f0/0.10
encapsulation dot1Q 10
ip address 172.17.17.1 255.255.255.0
description Network Data
ip helper-address 192.168.17.13
exit
```
```
int f0/0.50
encapsulation dot1Q 50
ip address 172.20.17.1 255.255.255.0
description Network VoIP
ip helper-address 192.168.17.13
exit
```
```
router eigrp 100
network 192.168.17.12 0.0.0.3
network 172.17.17.0 0.0.0.255
network 172.18.17.0 0.0.0.255
network 172.20.17.0 0.0.0.255
no auto-summary
passive-interface f0/0.10
passive-interface f0/0.50
passive-interface f0/1
```
 
### Server-PT
* IP Configuration
* Static

| Box  | IP |
| ------------- | ------------- |
| IPv4 Address | `172.18.17.254` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `172.18.17.1` |
| DNS Server | `172.18.17.254` |
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```

