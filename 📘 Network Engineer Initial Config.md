# 📘 Network Engineer Initial Config Guide

> เอกสารนี้จัดทำขึ้นเพื่อใช้เป็น **Reference ในการ Initial Config** อุปกรณ์ต่างๆ ที่ใช้งานบ่อยในโปรเจกต์ ทั้ง Switch, Router, Firewall และ Wireless จากหลายยี่ห้อ  
> 📅 อัปเดตล่าสุด: 2025-04-24  
> 👨‍💻 ผู้จัดทำ: [Anurak Chaiboon](https://github.com/) - Network Engineer (SI)

---

## 📑 Table of Contents

- [🔥 Firewall Configs](#-firewall-configs)
- [🌐 Router Configs](#-router-configs)
- [🔀 Switch Configs](#-switch-configs)
- [📡 Wireless Controller](#-wireless-controller)
- [🔧 Tools & Tips](#-tools--tips)
- [📎 Reference Links](#-reference-links)

---

## 🔥 Firewall Configs

### FortiGate
```bash
config system global
set hostname FG-Branch01
end

config system interface
edit "mgmt"
set ip 192.168.1.1/24
set allowaccess ping https ssh
next
end
```

### Palo Alto
```bash
configure
set deviceconfig system hostname PA-Branch01
set deviceconfig system ip-address 192.168.1.1 netmask 255.255.255.0
commit
exit
```

### Sophos XG
```bash
# เข้าผ่าน Web Admin หรือ sfcli
```

---

## 🌐 Router Configs

### Cisco ISR
```bash
hostname ISR-Branch01
interface GigabitEthernet0/0
ip address 10.0.0.1 255.255.255.0
no shutdown
```

---

## 🔀 Switch Configs

### Cisco Catalyst
```bash
hostname SW-Access01
interface vlan1
ip address 192.168.100.2 255.255.255.0
no shutdown
```

### Juniper EX
```bash
set system host-name ex-branch01
set interfaces vlan unit 0 family inet address 192.168.100.3/24
```

---

## 📡 Wireless Controller

### Ruckus SmartZone / ZoneDirector
```bash
enable
configure
set hostname Ruckus-WLC01
```

---

## 🔧 Tools & Tips

- 🧪 NetTools: `ping`, `traceroute`, `nmap`, `tcpdump`
- 💻 Remote Access: `ssh`, `telnet`, `console`
- 📊 Routing Table:
  - FortiGate: `get router info routing-table all`
  - Cisco: `show ip route`
  - Juniper: `show route`

---

## 📎 Reference Links

- 🔗 [Cisco Config Guide](https://www.cisco.com/c/en/us/support/index.html)
- 🔗 [Fortinet Documentation](https://docs.fortinet.com/)
- 🔗 [Juniper TechLibrary](https://www.juniper.net/documentation/)
- 🔗 [Ruckus Support Portal](https://support.ruckuswireless.com/)
- 🔗 [Palo Alto Live Community](https://live.paloaltonetworks.com/)

---
