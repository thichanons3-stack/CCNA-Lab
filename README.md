# 🌐 CCNA Hands-on Lab Practice & Troubleshooting Journey (Cisco CCNA 200-301)

[![Cisco](https://img.shields.io/badge/Cisco-CCNA%20200--301-blue?style=for-the-badge&logo=cisco&logoColor=white)](https://www.cisco.com/)
[![Packet Tracer](https://img.shields.io/badge/Simulator-Cisco%20Packet%20Tracer-brightgreen?style=for-the-badge)](https://www.netacad.com/courses/packet-tracer)
[![Focus](https://img.shields.io/badge/Focus-Network%20Engineering%20%26%20Troubleshooting-orange?style=for-the-badge)]()
[![Status](https://img.shields.io/badge/Status-Actively%20Updated-success?style=for-the-badge)]()

---

## 📖 เกี่ยวกับคลังความรู้นี้ (About This Repository)

ยินดีต้อนรับสู่คลังรวบรวมแบบฝึกหัดปฏิบัติการ (**Hands-on Labs**), ไฟล์จำลองเครือข่าย (**Packet Tracer Files**), ค่าการตั้งค่าอุปกรณ์จริง (**Running Configs**), และบันทึกการวิเคราะห์แก้ไขปัญหา (**Troubleshooting Documentation**) สำหรับการเตรียมสอบและเสริมสร้างทักษะระดับมืออาชีพตามหลักสูตร **Cisco Certified Network Associate (CCNA 200-301)**

### 🎯 เป้าหมายของโครงการ (Project Objectives)
Repository นี้จัดทำขึ้นเพื่อแสดงทักษะเชิงลึกด้าน Network Engineering และกระบวนการคิดวิเคราะห์อย่างเป็นระบบ:
1. **เข้าใจกลไกของโปรโตคอล (Deep Protocol Understanding):** ทำความเข้าใจเส้นทางการเดินทางของข้อมูล (Packet Flow), กลไก ARP, การทำงานของ DNS, การแบ่ง Broadcast Domain ใน Layer 2 และการส่งต่อแพ็กเก็ตข้ามเครือข่ายใน Layer 3
2. **ฝึกการแก้ไขปัญหาอย่างเป็นระบบ (Systematic Troubleshooting):** ฝึกฝนกระบวนการค้นหาจุดบกพร่องตามแนวคิด Hop-by-Hop Isolation, การวิเคราะห์สถานะ Interface, Routing Table, Name Resolution และการบันทึก Root Cause Analysis (ปัญหา -> สาเหตุ -> การแก้ไข -> ผลการทดสอบ)
3. **ผลงานที่ต่อยอดได้จริง (Practical Practice & Configurations):** บันทึกไฟล์ Topology `.pkt` และไฟล์การตั้งค่าของ Router/Switch เพื่อให้สามารถนำกลับมาเปิดทดสอบ ทบทวน หรือขยายขอบเขตระบบเครือข่ายได้
4. **เอกสารสรุปความรู้ระดับมืออาชีพ (Quality Documentation):** แต่ละโฟลเดอร์แล็บมี `README.md` เฉพาะตัว พร้อมรูป Topology, อธิบายคำสั่งหลัก และขั้นตอนการ Verify ผลลัพธ์

---

## 📂 โครงสร้างภายใน Repository (Repository Structure)

```text
CCNA-Lab/
├── 📄 .gitignore                                             <-- กำหนดละเว้นไฟล์ขยะและสื่อการสอนมีลิขสิทธิ์
├── 📄 README.md                                               <-- เอกสารภาพรวมหลัก (ไฟล์นี้)
├── 📁 12 - The Life of a Packet/                             <-- แล็บการเดินทางของแพ็กเก็ต & ARP Cache
│   ├── README.md
│   ├── 12 The Life of a Packet.pkt
│   ├── 12 The Life of a Packet.jpg
│   └── Configs/ (R1, R2, R3 running-config.txt)
├── 📁 13 - Cisco Troubleshooting Methodology & DNS Resolution/ <-- แล็บเทคนิคการแก้ปัญหาแบบ Hop-by-Hop & DNS
│   ├── README.md
│   ├── 13 The Cisco Troubleshooting Methodology.pkt
│   ├── 13 The Cisco Troubleshooting Methodology.jpg
│   └── Configs/ (R1, R2, R3 running-config.txt)
├── 📁 14 - Cisco Router and Switch Basics/                    <-- พื้นฐานการตั้งค่า Router และ Switch เบื้องต้น
│   ├── README.md
│   ├── 14 Cisco Router and Switch Basics.pkt
│   ├── 14 Cisco Router and Switch Basics.jpg
│   └── Configs/ (r1.txt, r2.txt)
├── 📁 22 - VLAN and Inter-VLAN Routing/                      <-- แล็บการแบ่ง VLAN และการ Routing ข้าม VLAN
│   ├── README.md
│   ├── 22-1 VLAN and Inter-VLAN Routing Configuration.pkt
│   └── 22-1 VLAN and Inter-VLAN Routing Configuration.jpg
├── 📁 29 - NAT Configuration/                                <-- แล็บ Network Address Translation (Static, Dynamic, PAT)
│   ├── README.md
│   ├── 29-1 NAT Configuration.pkt
│   ├── 29-1 NAT Configuration.JPG
│   └── Configs/ (R1.txt, SP1.txt)
├── 📁 30 - IPv6 Addressing and Routing/                       <-- แล็บ IPv6, EUI-64 และ Static Routing
│   ├── README.md
│   ├── 30-1 IPv6 Configuration Completed.pkt
│   ├── 30-1 IPv6 Configuration.JPG
│   └── Configs/ (R1, R2, R3 running-config.txt)
└── 📁 33 - Cisco Device Security/                             <-- แล็บการรักษาความปลอดภัยอุปกรณ์ & SSH
    ├── README.md
    ├── 33-1 Cisco Device Security Configuration.pkt
    ├── 33-1 Cisco Device Security Configuration.jpg
    └── Configs/ (R1.txt)
```

---

## 📑 สารบัญและสถานะแล็บ (Lab Directory & Roadmap)

| โฟลเดอร์แล็บ | หัวข้อหลัก (Core Topic) | เทคโนโลยี / โปรโตคอลสำคัญ | สิ่งที่มีใน Repository |
|---|---|---|---|
| [12 - The Life of a Packet](./12%20-%20The%20Life%20of%20a%20Packet/) | Packet Delivery Process & ARP Analysis | DNS Client, ARP Flow, Next-Hop MAC Address, Broadcast Domain | ✅ README, .pkt, Configs, Topology |
| [13 - Cisco Troubleshooting Methodology](./13%20-%20Cisco%20Troubleshooting%20Methodology%20%26%20DNS%20Resolution/) | การวิเคราะห์ปัญหาเครือข่ายเป็นลำดับขั้น | Hop-by-Hop Isolation, Interface Status, DNS Name Resolution | ✅ README, .pkt, Configs, Topology |
| [14 - Cisco Router and Switch Basics](./14%20-%20Cisco%20Router%20and%20Switch%20Basics/) | พื้นฐานการบริหารจัดการอุปกรณ์ Cisco | Hostname, Interface IP, Exec-timeout, CLI Navigation | ✅ README, .pkt, Configs, Topology |
| [22 - VLAN and Inter-VLAN Routing](./22%20-%20VLAN%20and%20Inter-VLAN%20Routing/) | การแบ่งส่วนเครือข่ายและการเราต์ติ้งข้าม VLAN | 802.1Q Trunking, Access Ports, Router-on-a-Stick (ROAS) | ✅ README, .pkt, Topology |
| [29 - NAT Configuration](./29%20-%20NAT%20Configuration/) | Network Address Translation | Static NAT, Dynamic NAT, Port Address Translation (PAT) | ✅ README, .pkt, Configs, Topology |
| [30 - IPv6 Addressing and Routing](./30%20-%20IPv6%20Addressing%20and%20Routing/) | การกำหนดแอดเดรสและการเราต์ติ้ง IPv6 | Global Unicast (GUA), Link-Local (LLA), EUI-64, Static Route | ✅ README, .pkt, Configs, Topology |
| [33 - Cisco Device Security](./33%20-%20Cisco%20Device%20Security/) | การรักษาความปลอดภัยอุปกรณ์และการเข้าถึง | Enable Secret, Local User, SSH v2, Login Block, Password Encryption | ✅ README, .pkt, Configs, Topology |

---

## 🧠 สาระสำคัญและทักษะที่ครอบคลุม (Key Networking Skills)

1. **Network Fundamentals & Protocols:**
   - การทำงานของ TCP/IP Model, Encapsulation, De-encapsulation
   - การแปลงชื่อโดเมนด้วย DNS (`ip domain-lookup`, `ip name-server`)
   - กลไกการจับคู่ IP และ MAC Address ผ่าน ARP และการอ่าน ARP Table (`show arp`)
   - การทำงานของ IPv6: การคำนวณ EUI-64 จาก MAC Address และการใช้ Link-Local (`fe80::/10`)

2. **IP Routing & Switching Technologies:**
   - การคอนฟิกและวิเคราะห์ Static Routing, Default Routing ทั้งบน IPv4 และ IPv6
   - การเปิดใช้งาน IPv6 Unicast Routing (`ipv6 unicast-routing`)
   - การจัดการ VLAN, Inter-VLAN Routing (Router-on-a-Stick) และ 802.1Q Trunking
   - แนวคิดการทำงานของ Dynamic Routing Protocols (OSPF, IGP Fundamentals)

3. **Network Services & Optimization:**
   - การตั้งค่า NAT / PAT เพื่อแปลงที่อยู่ระหว่าง Private IP และ Public IP
   - การแจกจ่าย IP ผ่านบริการ DHCP Server / Relay Agent

4. **Hands-on Troubleshooting Framework:**
   - **Layer 1 - Layer 3 Connectivity:** การใช้ `show ip interface brief`, ตรวจสอบพอร์ต `administratively down`, และการทดสอบเส้นทางด้วย `traceroute`
   - **Application / Services Verification:** ตรวจสอบ DNS Configuration บน Router และการ Ping ด้วย Hostname แทน IP

---

## 🛠️ เครื่องมือและสิ่งจำเป็น (Prerequisites & Tools)

- **[Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer)** (แนะนำเวอร์ชัน 8.0 ขึ้นไป เพื่อความเข้ากันได้ของไฟล์ `.pkt`)
- โปรแกรม Text Editor (เช่น VS Code, Cursor หรือ Notepad++) สำหรับเปิดดูไฟล์ `running-config.txt`
- Git สำหรับการ Clone และติดตามความเปลี่ยนแปลงของโปรเจกต์

---

## 🚀 วิธีการนำไปใช้งาน (How to Use)

### 1. โคลนคลังข้อมูล (Clone Repository)
```bash
git clone https://github.com/thichanons3-stack/CCNA-Lab.git
cd CCNA-Lab
```

### 2. เปิดและทดลองทำแล็บ (Open Lab)
1. เลือกหัวข้อแล็บที่สนใจจากสารบัญ
2. ดับเบิลคลิกไฟล์ `.pkt` ในโฟลเดอร์นั้นเพื่อเปิดใน **Cisco Packet Tracer**
3. อ่านเอกสาร `README.md` ประจำแล็บเพื่อดูภาพรวม ขั้นตอนคำสั่ง และกรณีศึกษาการ Troubleshooting
4. ตรวจสอบผลลัพธ์และการตั้งค่าจริงได้จากไฟล์ในโฟลเดอร์ `Configs/`

### 3. ตรวจสอบการทำงานและทดสอบผล (Verify & Test)
ใช้คำสั่งตรวจสอบมาตรฐานบน Cisco CLI เช่น:
```text
Router# show ip interface brief
Router# show ip route
Router# show arp
Router# ping <destination_ip>
Router# traceroute <destination_ip>
```

---

## 📝 รูปแบบของเอกสารในแต่ละแล็บ (Per-Lab Documentation Standard)

ในแต่ละโฟลเดอร์ย่อย เอกสารประกอบจะถูกจัดทำโดยมีโครงสร้างที่เป็นมาตรฐาน สอดคล้องกับแนวทางสากล:
- **Lab Overview:** สรุปสาระสำคัญและวัตถุประสงค์ของการทดลอง
- **Network Topology:** ผังการเชื่อมต่ออุปกรณ์และ IP Addressing Table
- **Key Configuration Steps:** ขั้นตอนและคำสั่งสำคัญที่ใช้ในการตั้งค่า
- **Troubleshooting Highlights:** กรณีศึกษาปัญหาที่เกิดขึ้นจริง (Problem), การวิเคราะห์ (Analysis), สาเหตุที่แท้จริง (Root Cause), และวิธีการแก้ไข (Solution)
- **Final Verification:** ตัวอย่าง Output จากคำสั่งตรวจสอบที่ยืนยันว่าระบบทำงานถูกต้อง 100%

---

## 📜 การอ้างอิงและคำชี้แจงลิขสิทธิ์ (Attribution & Disclaimer)

- คลังข้อมูลนี้จัดทำขึ้นเพื่อการศึกษา บันทึกการฝึกฝนทักษะเชิงปฏิบัติการ (Hands-on Practice) และทบทวนความรู้สำหรับการเตรียมสอบ **Cisco Certified Network Associate (CCNA 200-301)**
- สถานการณ์จำลองและโครงสร้างแล็บบางส่วนได้รับแรงบันดาลใจจากหลักสูตรการสอนเครือข่ายชั้นนำ อาทิ **CCNA Gold Bootcamp โดย Neil Anderson (FlackBox)** และ **Cisco Networking Academy**
- **การคุ้มครองทรัพย์สินทางปัญญา:** เอกสารแบบฝึกหัดลิขสิทธิ์ต้นฉบับ (Proprietary Lab Manuals), สไลด์บรรยาย (Slides), และเฉลยต้นฉบับ (Answer Keys) ทั้งหมดของผู้สอน **ถูกคัดแยกออกและไม่ได้มีการเผยแพร่บนคลังสาธารณะนี้**
- เนื้อหาและบทวิเคราะห์ทั้งหมดที่ปรากฏใน Repository นี้ (คำอธิบายทางเทคนิค, การวิเคราะห์หาสาเหตุของปัญหา, Topology Simulation และ Configuration Files) จัดทำขึ้นโดยผู้เขียนเองเพื่อส่งเสริมการเรียนรู้เชิงลึก

---

## 👨‍💻 ผู้จัดทำ (Author)

- **GitHub:** [@thichanons3-stack](https://github.com/thichanons3-stack)
- **เป้าหมาย:** บันทึกเส้นทางการเรียนรู้ ทบทวนความรู้ด้าน Network Engineering และการเตรียมตัวสอบใบรับรอง **Cisco Certified Network Associate (CCNA 200-301)**

---
*หากมีข้อเสนอแนะหรือพบจุดที่ต้องการปรับปรุง สามารถเปิด Issue หรือส่ง Pull Request เข้ามาแลกเปลี่ยนความรู้กันได้ครับ!* 🚀
