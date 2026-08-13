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
