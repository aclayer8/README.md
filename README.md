📘 Network Engineer Initial Config Guide

เอกสารนี้จัดทำขึ้นเพื่อใช้เป็น Reference ในการ Initial Config อุปกรณ์ต่างๆ ที่ใช้งานบ่อยในโปรเจกต์ ทั้ง Switch, Router, Firewall และ Wireless จากหลายยี่ห้ออัปเดตล่าสุด: 2025-04-24ผู้จัดทำ: Anurak Chaiboon - Network Engineer @ SI Company

🔧 Table of Contents

🔥 Firewall Configs

🌐 Router Configs

🔀 Switch Configs

📡 Wireless Controller

🔍 Tools & Tips

📎 Reference Links

🔥 Firewall Configs

FortiGate

# Set Hostname
config system global
set hostname FG-Branch01
end

# Set MGMT IP
config system interface
edit "mgmt"
set ip 192.168.1.1/24
set allowaccess ping https ssh
next
end

Palo Alto

# Basic setup via CLI
configure
set deviceconfig system hostname PA-Branch01
set deviceconfig system ip-address 192.168.1.1 netmask 255.255.255.0
commit
exit

Sophos XG

# ผ่าน Web Admin ได้เลย หรือ CLI (sfcli)

...

🌐 Router Configs

Cisco ISR

hostname ISR-Branch01
interface GigabitEthernet0/0
ip address 10.0.0.1 255.255.255.0
no shutdown

...

🔀 Switch Configs

Cisco Catalyst

hostname SW-Access01
interface vlan1
ip address 192.168.100.2 255.255.255.0
no shutdown

Juniper EX

set system host-name ex-branch01
set interfaces vlan unit 0 family inet address 192.168.100.3/24

...

📡 Wireless Controller

Ruckus ZoneDirector / SmartZone

Note: ใช้ Web UI เป็นหลัก แต่ CLI ใช้สำหรับ Troubleshooting

# ตัวอย่าง basic config CLI
enable
configure
set hostname Ruckus-WLC01

...

🔍 Tools & Tips

NetTools ที่ใช้บ่อย: ping, traceroute, nmap, tcpdump

วิธี Remote: ssh, telnet, console

การเช็ค Routing: show ip route, get router info routing-table all (forti), show route (juniper)

📎 Reference Links

Cisco Config Guide

Fortinet Docs

Juniper TechLibrary

Ruckus Support

Palo Alto Live Community

