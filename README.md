# 🧱 Palo Alto Firewall Initial Config

## 🛠️ Interface Setup
```bash
configure
set deviceconfig system hostname PA-FW01
set deviceconfig system ip-address 192.168.1.10 netmask 255.255.255.0 default-gateway 192.168.1.1
set deviceconfig system dns-setting servers primary 8.8.8.8 secondary 1.1.1.1
