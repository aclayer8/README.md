# ขั้นตอนการ Initial อุปกรณ์เครือข่าย (Multi-Vendor)

เอกสารนี้เป็นแนวทางสำหรับ Network Engineer ในการเริ่มต้นใช้งานอุปกรณ์เครือข่ายจากหลากหลายผู้ผลิต รวมถึง Firewall, Switch, และ Router จากแบรนด์ชั้นนำ เพื่อให้มั่นใจว่าการตั้งค่าเริ่มต้นเป็นไปอย่างราบรื่นและมีประสิทธิภาพ

## ขั้นตอนทั่วไป (Common Steps)

ไม่ว่าจะเป็นอุปกรณ์ประเภทใดหรือยี่ห้อใด ขั้นตอนพื้นฐานเหล่านี้มักจะมีความคล้ายคลึงกัน:

1.  **การแกะกล่องและตรวจสอบ:**
    * [ ] ตรวจสอบความเสียหายทางกายภาพของอุปกรณ์และอุปกรณ์เสริม (เช่น สายไฟ, Console Cable)
    * [ ] ตรวจสอบว่าได้รับอุปกรณ์และเอกสารคู่มือครบถ้วนตามรายการสั่งซื้อ
    * [ ] บันทึกหมายเลข Serial ของอุปกรณ์

2.  **การเชื่อมต่อเริ่มต้น:**
    * [ ] เชื่อมต่อแหล่งจ่ายไฟที่ถูกต้องตามสเปคของอุปกรณ์
    * [ ] เชื่อมต่อ Console Cable (Serial หรือ USB) เข้ากับพอร์ต Console ของอุปกรณ์และคอมพิวเตอร์
    * [ ] (ถ้ามี) เชื่อมต่อสาย Ethernet สำหรับการจัดการ Out-of-Band (OOB)

3.  **การเข้าถึง Console:**
    * [ ] เปิดโปรแกรม Terminal บนคอมพิวเตอร์ (เช่น PuTTY, SecureCRT)
    * [ ] กำหนดค่า Serial Port ให้ถูกต้อง (Baud Rate, Data Bits, Parity, Stop Bits, Flow Control) ตามคู่มืออุปกรณ์
    * [ ] เปิดการเชื่อมต่อ Console และตรวจสอบ Boot Sequence ของอุปกรณ์

4.  **การตั้งค่าพื้นฐาน:**
    * [ ] ตั้งค่า Hostname ของอุปกรณ์ให้สื่อความหมาย
    * [ ] ตั้งค่า Password สำหรับ User ระดับ Privilege (Enable/Admin) ที่มีความปลอดภัย
    * [ ] ตั้งค่า IP Address สำหรับ Management Interface (ถ้ามี) และ Gateway
    * [ ] ตั้งค่า DNS Server
    * [ ] ตั้งค่า Timezone และ NTP Server เพื่อให้เวลาของอุปกรณ์ถูกต้อง
    * [ ] บันทึกการตั้งค่าเริ่มต้น

## ขั้นตอนเฉพาะสำหรับแต่ละยี่ห้อและประเภทอุปกรณ์ (Vendor & Device-Specific Steps)

ส่วนนี้จะเน้นขั้นตอนที่อาจแตกต่างกันไปในแต่ละผู้ผลิตและประเภทของอุปกรณ์ (Firewall, Switch, Router):

### Cisco

#### Router (IOS/IOS XE)

* [ ] ตรวจสอบ Version ของ IOS ด้วยคำสั่ง `show version`
* [ ] (ถ้าจำเป็น) อัปเกรด IOS ตามแผน
* [ ] ตั้งค่า Interface ต่างๆ (Physical และ Logical เช่น VLAN Interface) พร้อม IP Address และ Description
* [ ] กำหนด Routing Protocol (เช่น OSPF, BGP, RIP) ตามความต้องการ
* [ ] ตั้งค่า Access Control Lists (ACLs) หากจำเป็น
* [ ] ตั้งค่า Virtual Terminal (VTY) Lines และ Password
* [ ] กำหนดค่า `service password-encryption` เพื่อเข้ารหัส Password ใน Configuration
* [ ] เปิดใช้งาน SSH และปิด Telnet (เพื่อความปลอดภัย)
* [ ] ตั้งค่า Logging (Console, Buffer, Syslog)
* [ ] บันทึก Configuration ด้วยคำสั่ง `write memory` หรือ `copy running-config startup-config`

#### Switch (IOS/IOS XE)

* [ ] ตรวจสอบ Version ของ IOS ด้วยคำสั่ง `show version`
* [ ] (ถ้าจำเป็น) อัปเกรด IOS ตามแผน
* [ ] ตั้งค่า VLANs และกำหนด Interface Mode (Access/Trunk)
* [ ] กำหนดค่า Spanning Tree Protocol (STP)
* [ ] (ถ้ามี) ตั้งค่า Port Channel/Link Aggregation (EtherChannel/LAG)
* [ ] ตั้งค่า Security Features (เช่น Port Security, DHCP Snooping, Dynamic ARP Inspection)
* [ ] ตั้งค่า Virtual Terminal (VTY) Lines และ Password
* [ ] กำหนดค่า `service password-encryption` เพื่อเข้ารหัส Password ใน Configuration
* [ ] เปิดใช้งาน SSH และปิด Telnet (เพื่อความปลอดภัย)
* [ ] ตั้งค่า Logging (Console, Buffer, Syslog)
* [ ] บันทึก Configuration ด้วยคำสั่ง `write memory` หรือ `copy running-config startup-config`

#### Firewall (ASA/Firepower)

* [ ] **ASA:**
    * [ ] ตรวจสอบ Version ด้วยคำสั่ง `show version`
    * [ ] (ถ้าจำเป็น) อัปเกรด ASA Software ตามแผน
    * [ ] ตั้งค่า Interface ต่างๆ พร้อม Security Level และ IP Address
    * [ ] กำหนด Network Object และ Group Object
    * [ ] ตั้งค่า Access Rules (ACLs) เพื่อควบคุม Traffic
    * [ ] ตั้งค่า NAT/PAT Policies
    * [ ] ตั้งค่า Management Access (HTTP/HTTPS/SSH/ASDM)
    * [ ] ตั้งค่า Password สำหรับ User ระดับ Privilege (Enable)
    * [ ] กำหนดค่า `service password-encryption`
    * [ ] บันทึก Configuration ด้วยคำสั่ง `write memory`

* [ ] **Firepower (FMC/FTD):**
    * [ ] (ส่วนใหญ่ Initial ผ่าน Firepower Management Center - FMC)
    * [ ] เชื่อมต่อ FTD เข้ากับ FMC
    * [ ] กำหนด Interface และ Zone
    * [ ] สร้าง Security Policies (Intrusion Prevention, Malware Protection, File Policy)
    * [ ] สร้าง Access Control Policies
    * [ ] กำหนด NAT Policies
    * [ ] ตรวจสอบ License
    * [ ] Deploy Configuration ไปยัง FTD

### Juniper

#### Router (Junos OS)

* [ ] ตรวจสอบ Version ของ Junos ด้วยคำสั่ง `show version`
* [ ] (ถ้าจำเป็น) อัปเกรด Junos ตามแผน
* [ ] ตั้งค่า Interface ต่างๆ (`ge-0/0/0`, `xe-0/0/0`, `vlan.0`) พร้อม IP Address และ Description
* [ ] กำหนด Routing Protocol (เช่น OSPF, BGP, RIP) ภายใต้ `[edit protocols]`
* [ ] ตั้งค่า Firewall Filters ภายใต้ `[edit firewall]`
* [ ] ตั้งค่า Root Password ภายใต้ `[edit system root-authentication]`
* [ ] กำหนดค่า Management Interface (`fxp0` หรือ `em0`) และ IP Address ภายใต้ `[edit system management]`
* [ ] ตั้งค่า System Hostname ภายใต้ `[edit system host-name]`
* [ ] ตั้งค่า Commit Model (`commit` เพื่อบันทึก)
* [ ] กำหนดค่า SSH Access ภายใต้ `[edit system services ssh]`
* [ ] ตั้งค่า System Logging ภายใต้ `[edit system syslog]`
* [ ] บันทึก Configuration ด้วยคำสั่ง `commit` และ `save`

#### Switch (Junos OS)

* [ ] ตรวจสอบ Version ของ Junos ด้วยคำสั่ง `show version`
* [ ] (ถ้าจำเป็น) อัปเกรด Junos ตามแผน
* [ ] ตั้งค่า VLANs ภายใต้ `[edit vlans]` และกำหนด Interface Mode (Access/Trunk) ภายใต้ `[edit interfaces]`
* [ ] กำหนดค่า Spanning Tree Protocol (STP) ภายใต้ `[edit protocols rstp]` หรือ `[edit protocols mstp]`
* [ ] (ถ้ามี) ตั้งค่า Link Aggregation Groups (LAGs) ภายใต้ `[edit interfaces ae0]`
* [ ] ตั้งค่า Security Features (เช่น Port Security, DHCP Snooping, ARP Inspection) ภายใต้ `[edit ethernet-switching-options]`
* [ ] ตั้งค่า Root Password ภายใต้ `[edit system root-authentication]`
* [ ] กำหนดค่า Management Interface (`fxp0` หรือ `em0`) และ IP Address ภายใต้ `[edit system management]`
* [ ] ตั้งค่า System Hostname ภายใต้ `[edit system host-name]`
* [ ] กำหนดค่า SSH Access ภายใต้ `[edit system services ssh]`
* [ ] ตั้งค่า System Logging ภายใต้ `[edit system syslog]`
* [ ] บันทึก Configuration ด้วยคำสั่ง `commit` และ `save`

#### Firewall (SRX Series)

* [ ] ตรวจสอบ Version ของ Junos ด้วยคำสั่ง `show version`
* [ ] (ถ้าจำเป็น) อัปเกรด Junos ตามแผน
* [ ] ตั้งค่า Security Zones ภายใต้ `[edit security zones security-zone]` และกำหนด Interface เข้า Zone
* [ ] กำหนด Security Policies ภายใต้ `[edit security policies from-zone <source-zone> to-zone <destination-zone> policy <policy-name>]`
* [ ] ตั้งค่า NAT Policies (Source NAT, Destination NAT) ภายใต้ `[edit security nat]`
* [ ] ตั้งค่า Root Password ภายใต้ `[edit system root-authentication]`
* [ ] กำหนดค่า Management Interface (`fxp0` หรือ `em0`) และ IP Address ภายใต้ `[edit system management]`
* [ ] ตั้งค่า System Hostname ภายใต้ `[edit system host-name]`
* [ ] กำหนดค่า SSH Access ภายใต้ `[edit system services ssh]`
* [ ] ตั้งค่า System Logging ภายใต้ `[edit system syslog]`
* [ ] บันทึก Configuration ด้วยคำสั่ง `commit` และ `save`

### อื่นๆ (Others)

* [ ] **[ระบุยี่ห้อ] [Router/Switch/Firewall]:**
    * [ ] ตรวจสอบ Version ด้วยคำสั่ง `[ระบุคำสั่ง]`
    * [ ] ขั้นตอนเฉพาะอื่นๆ: `[ระบุขั้นตอน]`

## ขั้นตอนหลังการ Initial

1.  **การทดสอบการเชื่อมต่อ:**
    * [ ] ทดสอบการ Ping ไปยัง Management IP Address ของอุปกรณ์จากเครือข่าย
    * [ ] ทดสอบการเข้าถึงอุปกรณ์ผ่าน SSH
    * [ ] (สำหรับ Firewall) ทดสอบการ Throughput และ Rule ที่ตั้งค่า

2.  **การสำรองข้อมูล Configuration:**
    * [ ] ทำการ Backup Configuration เริ่มต้นของอุปกรณ์

3.  **การจัดทำเอกสาร:**
    * [ ] บันทึกรายละเอียดการตั้งค่าเริ่มต้น (IP Address, Hostname, Password, Version)
    * [ ] เก็บเอกสารคู่มือของอุปกรณ์ไว้ในที่ที่เข้าถึงได้ง่าย
    * [ ] วาด Diagram การเชื่อมต่อเริ่มต้น (ถ้าจำเป็น)

**หมายเหตุ:**

* เอกสารนี้เป็นเพียงแนวทางเบื้องต้น ขั้นตอนที่แท้จริงอาจแตกต่างกันไปขึ้นอยู่กับรุ่นของอุปกรณ์และนโยบายขององค์กร
* ควรอ้างอิงคู่มือการใช้งานของอุปกรณ์แต่ละยี่ห้อและรุ่นเสมอ
* คำสั่งที่แสดงเป็นตัวอย่าง อาจมีการเปลี่ยนแปลงในแต่ละ Version ของ Firmware/OS

หวังว่า Markdown นี้จะช่วยให้คุณเริ่มต้นใช้งานอุปกรณ์เครือข่ายต่างๆ ได้อย่างมีประสิทธิภาพมากยิ่งขึ้นนะครับ! หากมีแบรนด์หรืออุปกรณ์อื่นๆ ที่ต้องการให้เพิ่มเข้าไปอีก บอกได้เลยนะครับ ยินดีปรับปรุงเพิ่มเติมครับ!
