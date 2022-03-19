### PDL
```
ip access-list extended OUTSIDE
permit ip any any 
exit
```
```
ip access-list extended INSIDE
permit ip host 1.0.0.6 host 1.0.0.2
permit tcp any host 1.0.0.2 eq 80
permit tcp any host 1.0.0.2 eq 443
permit tcp any host 1.0.0.2 established
permit udp any eq 53 host 1.0.0.2
permit icmp any host 1.0.0.2 echo-reply 
exit
```
```
ip access-list extended HTTPS
permit tcp any host 10.168.17.254 eq 443
exit
```
```
ip access-list extended PDL1
permit ip any any
exit
```
```
int s0/0/0
ip access-group OUTSIDE out
ip access-group INSIDE in
exit
```
```
int s0/0/1
ip access-group PDL1 out
exit
int s0/1/0
ip access-group PDL1 out
exit
```
```
int f0/0
ip access-group HTTPS out
```
### PDL1
```
ip access-list extended HTTP
permit tcp any host 10.17.40.254 eq 80
exit
```
```
int f0/0
ip access-group HTTP out
```
### PDL2
```
ip access-list extended OUTSIDE
permit ip any any 
exit
```
```
ip access-list extended INSIDE
permit tcp any host 1.0.0.10 established
permit udp any eq 53 host 1.0.0.10
permit icmp any host 1.0.0.10 echo-reply 
exit
```
```
ip access-list extended HTTP
permit tcp any host 10.17.40.254 eq 80
exit
```
```
ip access-list extended PDL1
permit ip any any
exit
```
```
int s0/0/0
ip access-group OUTSIDE out
ip access-group INSIDE in
exit
```
```
int s0/0/1
ip access-group PDL1 out
exit
int s0/1/0
ip access-group PDL1 out
exit
```
```
int f0/0
ip access-group HTTP out
```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
```

```
