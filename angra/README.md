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

| Camp  | Value |
| ------------- | ------------- |
| IPv4 Address | `172.18.17.254` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `172.18.17.1` |
| DNS Server | `172.18.17.254` |

### SWANGRA
```
vlan 10
name data
exit
vlan 50
name voip
exit
```
```
int f0/1
switchport mode trunk
exit
```
```
int f0/2
switchport mode access
switchport access vlan 10
exit
```
```
int f0/3
switchport voice vlan 50
exit
```
## DHCP
### ANGRA1
```
ip dhcp pool vlan10
network 172.17.17.0 255.255.255.0
default-router 172.17.17.1
option 150 ip 192.168.17.13
dns-server 172.18.17.254
exit

ip dhcp pool vlan50
network 172.20.17.0 255.255.255.0
default-router 172.20.17.1
option 150 ip 192.168.17.13
dns-server 172.18.17.254
exit
```
```
telephony-service
max-ephones 5
max-dn 5
ip source-address 192.168.17.13 port 2000
auto assign 1 to 5
exit
```
```
ephone-dn 1
number 201
exit
ephone-dn 2
number 202
exit
ephone-dn 3
number 203
exit
ephone-dn 4
number 204
exit
ephone-dn 5
number 205
exit
```
## Wireless
### Server-PT
* Services
* AAA

* Service `On`

* Network configuration

| Camp | Value |
| ------------- | ------------- |
| Client Name | `WiFi` |
| Client IP | `172.16.17.2` |
| Secret | `Passw0rd` |
| ServerType | `Radius` |

* User Setup

| Camp | Value |
| ------------- | ------------- |
| Username | `maria` |
| Password | `Passw0rd` |

### Wireless Router0

* GUI
* Setup
* Basic Setup
* Internet Connection type `Static IP`

| Camp | V1 | V2 | V3 | V4 |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| Internet IP Address | `172` | `16` | `17` | `2` |
| Subnet Mask | `255` | `255` | `255` | `0` |
| Default Gateway | `172` | `16` | `17` | `1` |
| DNS 1 | `172` | `18` | `17` | `254` |

Save Settings

* Network Setup
* Ip Address: `172` `19` `17` `1`
* Subnet Mask: `255.255.255.0`

Save Settings

* DHCP Server: `Enable`
* Start IP Address: `100`
* Maximum number of Users: `100`
* Static DNS1: `172` `18` `17` `254`

Save Settings

* Wireless
* Basic Wireless Settings
* Network Name (SSID): `Angra`

Save Settings

* Wireless Security
* Security Mode: `WPA2 Enterprise`
* RADIUS Server: `172` `18` `17` `254`
* Shared Secret: `Passw0rd`
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

