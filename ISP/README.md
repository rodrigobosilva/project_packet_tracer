### Router ISP
```
int s0/0/0
no shutdown
ip address 1.0.0.1 255.255.255.252
exit
```
```
int s0/0/1
no shutdown
ip address 1.0.0.5 255.255.255.252
exit
```
```
int f0/0
no shutdown
ip address 8.8.8.1 255.255.255.0
exit
```
```
int f0/1
no shutdown
ip address 4.4.4.1 255.255.255.0
exit
```

### Server0
* IP Configuration
* Static

| Box  | IP |
| ------------- | ------------- |
| IPv4 Address | `8.8.8.8` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `8.8.8.1` |
| DNS Server | `8.8.8.8` |

### PC0
* IP Configuration
* Static

| Box  | IP |
| ------------- | ------------- |
| IPv4 Address | `4.4.4.4` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `4.4.4.1` |
| DNS Server | `8.8.8.8` |
