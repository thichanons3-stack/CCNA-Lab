# CCNA Lab: Cisco Troubleshooting Methodology & DNS Resolution

## Lab Overiew
แล็บนี้เป็นการฝึกปฏิบัติการค้นหาและแก้ไขปัญหาเครือข่ายอย่างเป็นระบบ (Troubleshooting Methodology) บนระบบเครือข่าย Cisco โดยครอบคลุม:
- การตรวจสอบและวิเคราะห์การเชื่อมต่อแบบเป็นลำดับขั้น (Hop-by-Hop Isolation ด้วย Traceroute และ Ping)
- การตรวจสอบสถานะ Physical & Data Link/Network Layer Interfaces บน Cisco IOS
- การตั้งค่าและแก้ไขปัญหาการแปลงชื่อโดเมน (DNS Name Resolution & DNS Client Configuration) บน Router

## Network Topology
<img width="615" height="407" alt="13 The Cisco Troubleshooting Methodology" src="https://github.com/user-attachments/assets/2197a6b6-937c-4933-861b-da109c481d66" />

## Key Configuration Steps (สรุปข้อตั้งค่าและการแก้ไขหลัก)

1. **การเปิดใช้งาน Interface ที่ถูก Shutdown บน R2:**
   ```text
   R2(config)# interface FastEthernet0/0
   R2(config-if)# no shutdown
   ```
2. **การลบ DNS Name Server เดิมที่ตั้งค่า IP ผิดพลาดบน R3:**
   ```text
   R3(config)# no ip name-server 10.10.10.1
   ```
3. **การกำหนด DNS Name Server ที่ถูกต้องบน R3:**
   ```text
   R3(config)# ip name-server 10.10.10.10
   ```

## Troubleshooting Highlights

### ปัญหาที่ 1: ไม่สามารถเชื่อมต่อกับ DNS Server ได้ (Layer 1-3 Connectivity Issue)
* **ปัญหาที่เจอ (Problem):** จาก R3 สั่ง `telnet 10.10.10.10` แล้วขึ้นสถานะ `% Connection timed out; remote host not responding` 
* **การวิเคราะห์ (Analysis):** ใช้คำสั่ง `traceroute 10.10.10.10` จาก R3 พบว่าแพ็กเก็ตเดินทางไปหยุดอยู่ที่ R2 (`10.10.20.2`) และไม่ถูก Forward ต่อไปยัง Subnet ฝั่งปลายทาง
* **สาเหตุ (Root Cause):** เมื่อตรวจสอบ R2 ด้วยคำสั่ง `show ip interface brief` พบว่าพอร์ต `FastEthernet0/0` (ฝั่งที่เชื่อมต่อกับ SW1 และ DNS-Server) มีสถานะเป็น `administratively down`
* **แนวทางแก้ไข (Solution):** เข้าสู่ Interface `FastEthernet0/0` บน R2 แล้วสั่ง `no shutdown` เพื่อเปิดพอร์ตให้พร้อมใช้งาน

### ปัญหาที่ 2: Hostname Resolution ล้มเหลว (Application Layer DNS Misconfiguration)
* **ปัญหาที่เจอ (Problem):** หลังจากเปิดพอร์ตแล้ว สามารถ `ping 10.10.10.10` ผ่าน IP ได้สำเร็จ แต่เมื่อสั่ง `ping r1` จาก R3 ระบบแจ้งเตือน:
  ```text
  Translating "r1"...domain server (10.10.10.1)
  % Unrecognized host or address, or protocol not running.
  ```
* **สาเหตุ (Root Cause):** มีการตั้งค่า `ip name-server` บน R3 ชี้ไปยัง `10.10.10.1` (IP ของ R1) แทนที่จะชี้ไปยังเครื่อง DNS Server จริง (`10.10.10.10`) ทำให้ Router ไม่สามารถขอ Resolve Name Record ได้
* **แนวทางแก้ไข (Solution):** ลบ Name Server ที่ผิดออกด้วยคำสั่ง `no ip name-server 10.10.10.1` และเพิ่ม Name Server ที่ถูกต้องด้วย `ip name-server 10.10.10.10`

* ## Final Verification

1. **ตรวจสอบการเชื่อมต่อระดับ IP ไปยัง DNS Server จาก R3:**
   ```text
   R3# ping 10.10.10.10
   Type escape sequence to abort.
   Sending 5, 100-byte ICMP Echos to 10.10.10.10, timeout is 2 seconds:
   !!!!!
   Success rate is 100 percent (5/5), round-trip min/avg/max = 1/2/4 ms
   ```

2. **ทดสอบการค้นหาชื่อและ Ping ผ่าน Hostname (DNS Resolution & End-to-End Connectivity):**
   คำสั่ง Ping ไปยัง Hostname `r1` จาก R3:
     ```text
     R3# ping r1
     Translating "r1"...domain server (10.10.10.10) [OK]

     Type escape sequence to abort.
     Sending 5, 100-byte ICMP Echos to 10.10.10.1, timeout is 2 seconds:
     !!!!!
     Success rate is 100 percent (5/5), round-trip min/avg/max = 1/2/5 ms
     ```
