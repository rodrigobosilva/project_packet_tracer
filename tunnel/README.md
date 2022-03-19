## Base
### PDL
```
int tun100
ip address 10.255.255.1 255.255.255.252
tunnel source s0/0/0
tunnel destination 1.0.0.6
```
### ANGRA
```
int tun100
ip address 10.255.255.2 255.255.255.252
tunnel source s0/0/0
tunnel destination 1.0.0.2
```
## Encrypted
### PDL
```
access-list 100 permit gre host 1.0.0.2 host 1.0.0.6
```
```
crypto ipsec transform-set TRANS ah-sha-hmac esp-aes 256 esp-sha-hmac
```
```
crypto isakmp policy 10
encr aes 256
authentication pre-share
group 5
lifetime 3600
exit
```
```
crypto isakmp key Passw0rd address 1.0.0.6
```
```
crypto map OMAPA 10 ipsec-isakmp 
set peer 1.0.0.6
set transform-set TRANS
match address 100
exit
```
```
int s0/0/0
crypto map OMAPA
exit
```
### ANGRA
```
access-list 100 permit gre host 1.0.0.6 host 1.0.0.2
```
```
crypto ipsec transform-set TRANS ah-sha-hmac esp-aes 256 esp-sha-hmac
```
```
crypto isakmp policy 10
encr aes 256
authentication pre-share
group 5
lifetime 3600
exit
```
```
crypto isakmp key Passw0rd address 1.0.0.2
```
```
crypto map OMAPA 10 ipsec-isakmp 
set peer 1.0.0.2
set transform-set TRANS
match address 100
exit
```
```
int s0/0/0
crypto map OMAPA
exit
```
