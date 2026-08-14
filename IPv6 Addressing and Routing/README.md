# CCNA Lab: IPv6 Addressing, EUI-64 & Static Routing

## Lab Overview
แล็บนี้เป็นการตั้งค่าระบบเครือข่าย IPv6 แบบ Dual-Stack บน Cisco Routers (R1, R2, R3) และ End Hosts (PC1, PC2) โดยครอบคลุมการตั้งค่า:
- Global Unicast Address (GUA) และ Link-Local Address (LLA)
- การสร้าง IPv6 แบบ EUI-64
- การตั้งค่า IPv6 Static Routes และ Default Routes

## Network Topology
<img width="657" height="366" alt="30-1 IPv6 Configuration" src="https://github.com/user-attachments/assets/30ff3fa9-24ad-498f-9682-f043254c623e" />

## Key Configuration Steps (สรุปข้อตั้งค่าหลัก)

1. **การตั้งค่า IPv6 และ EUI-64 บน Host (PC1/PC2):**
  ```text
  PC1(config-if)# ipv6 address 2001:db8::/64 eui-64
  ```
2. **การตั้งค่า Link-Local Address แบบแมนนวล:**
  ```text
  R1(config-if)# ipv6 address fe80::1 link-local
  ```
3. **การเปิดใช้งาน IPv6 Routing บน Routers (Crucial Step):**
  ```text
  R1(config)# ipv6 unicast-routing
  ```
4. **การตั้งค่า Static Routes บน R2 (ตัวอย่าง):**
  ```text
  R2(config)# ipv6 route 2001:db8::/64 2001:db8:0:1::1
  R2(config)# ipv6 route 2001:db8:0:3::/64 2001:db8:0:2::1
  ```
## Troubleshooting Highlights
* **ปัญหาที่เจอ (Problem):** ในตอนแรกตั้งค่า IP และ Static Route ถูกต้องแล้ว แต่ PC1 ไม่สามารถ Ping ไปหา R2 (2001:db8:0:1::2) ได้
* **สาเหตุ (Root Cause):** Router ของ Cisco โดยค่าเริ่มต้นจะยังไม่ทำการ Forward แพ็กเก็ต IPv6 จนกว่าจะเปิดใช้งาน IPv6 Routing
* **แนวทางแก้ไข (Solution):** พิมพ์คำสั่ง ipv6 unicast-routing ใน Global Configuration Mode บน R1, R2 และ R3

## Final Verification
1. **ตรวจสอบตารางการจัดเส้นทางบน R1 (show ipv6 route):**
  ```text
  S   2001:DB8:0:2::/64 [1/0] via 2001:DB8:0:1::2
  S   2001:DB8:0:3::/64 [1/0] via 2001:DB8:0:1::2
  ```
2. **ทดสอบการเชื่อมต่อแบบ End-to-End (Ping PC1 -> PC2):**
   * **พิมพ์สั่ง Ping จาก PC1 ไปยัง EUI-64 IPv6 Address ของ PC2:**
    
   ```text
   PC1#ping 2001:DB8:0:3:201:C7FF:FE50:8E8A
   ```
   * **ผลลัพธ์:**
   ```text
   Type escape sequence to abort.
   Sending 5, 100-byte ICMP Echos to 2001:DB8:0:3:201:C7FF:FE50:8E8A, timeout is 2 seconds:
   !!!!!
   Success rate is 100 percent (5/5), round-trip min/avg/max = 0/1/4 ms
   ```
