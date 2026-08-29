# CCNA Lab: The Life of a Packet – DNS Client Configuration & ARP Cache Analysis

## Lab Overview
แล็บนี้เป็นการศึกษาและวิเคราะห์กลไกการส่งต่อข้อมูล (Packet Delivery Process) ข้ามเครือข่ายตามแนวคิด **"The Life of a Packet"** บนอุปกรณ์ Cisco Routers (R1, R2, R3) และ DNS Server โดยครอบคลุมหัวข้อสำคัญ:
- การตั้งค่า Cisco Routers ให้ทำงานเป็น **DNS Client** เพื่อทำการ Resolve Hostname เป็น IP Address อัตโนมัติ
- การวิเคราะห์กระบวนการทำงานของ **ARP (Address Resolution Protocol)** และการสร้าง **ARP Cache**
- การทำความเข้าใจขอบเขตของ **Layer 2 Broadcast Domain** และบทบาทของ Next-Hop MAC Address เมื่อแพ็กเก็ตเดินทางข้าม Subnet

## Network  Topology
<img width="auto" height="auto" scr="https://github.com/thichanons3-stack/CCNA-Lab/blob/main/The%20Life%20of%20a%20Packet%20/12%20The%20Life%20of%20a%20Packet.jpg">

## Key Configuration Steps

### 1. การเปิดใช้งาน DNS Lookup และกำหนด Name Server บน Routers
กำหนดให้ R1, R2 และ R3 ใช้งาน DNS Server IP `10.10.10.10` เพื่อแปลง Hostname เป็น IP Address:

* **R1, R2, R3 Configuration:**
  ```text
  การตั้งค่าของ R2 และ R3 เหมือนกับ R1
  R1(config)# ip domain-lookup
  R1(config)# ip name-server 10.10.10.10
  ```
