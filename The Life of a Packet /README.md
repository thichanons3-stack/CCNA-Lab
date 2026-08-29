# CCNA Lab: The Life of a Packet – DNS Client Configuration & ARP Cache Analysis

## Lab Overview
แล็บนี้เป็นการศึกษาและวิเคราะห์กลไกการส่งต่อข้อมูล (Packet Delivery Process) ข้ามเครือข่ายตามแนวคิด **"The Life of a Packet"** บนอุปกรณ์ Cisco Routers (R1, R2, R3) และ DNS Server โดยครอบคลุมหัวข้อสำคัญ:
- การตั้งค่า Cisco Routers ให้ทำงานเป็น **DNS Client** เพื่อทำการ Resolve Hostname เป็น IP Address อัตโนมัติ
- การวิเคราะห์กระบวนการทำงานของ **ARP (Address Resolution Protocol)** และการสร้าง **ARP Cache**
- การทำความเข้าใจขอบเขตของ **Layer 2 Broadcast Domain** และบทบาทของ Next-Hop MAC Address เมื่อแพ็กเก็ตเดินทางข้าม Subnet

## Network  Topology
<img scr=>

