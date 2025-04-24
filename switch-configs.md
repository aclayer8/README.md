# 🔀 Switch Configs

## Cisco Catalyst
```bash
hostname SW-Access01
interface vlan1
ip address 192.168.100.2 255.255.255.0
no shutdown
```

## Juniper EX
```bash
set system host-name ex-branch01
set interfaces vlan unit 0 family inet address 192.168.100.3/24
```