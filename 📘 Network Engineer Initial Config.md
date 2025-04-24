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
