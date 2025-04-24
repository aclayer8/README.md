# 🔥 Firewall Configs

## FortiGate
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

## Palo Alto
```bash
configure
set deviceconfig system hostname PA-Branch01
set deviceconfig system ip-address 192.168.1.1 netmask 255.255.255.0
commit
exit
```

## Sophos XG
```bash
# เข้าผ่าน Web Admin หรือ sfcli
```