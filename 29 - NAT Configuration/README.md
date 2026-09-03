# CCNA Lab: NAT (Network Address Translation) Configuration

## Lab Overview
แล็บนี้เป็นการฝึกปฏิบัติการตั้งค่าและวิเคราะห์การทำงานของระบบแปลงที่อยู่เครือข่าย (**Network Address Translation - NAT**) บนเราเตอร์ Cisco เพื่อให้เครื่องลูกข่ายในระบบเครือข่ายภายใน (Private Network) สามารถสื่อสารออกสู่อินเทอร์เน็ต (Public Network) ได้ โดยครอบคลุม:
- การกำหนด Interface ฝั่งภายในและภายนอก (**`ip nat inside`** และ **`ip nat outside`**)
- การตั้งค่า **Static NAT** (การจับคู่ IP แบบ 1-to-1 สำหรับ Server)
- การตั้งค่า **Dynamic NAT** (การจัดสรร IP จาก NAT Pool ชั่วคราว)
- การตั้งค่า **PAT (Port Address Translation / NAT Overload)** สำหรับการแชร์ Public IP เดียวกันโดยใช้ Port Number
- การตรวจสอบตารางการแปลงที่อยู่ด้วยคำสั่ง `show ip nat translations`

## Network Topology
![NAT Configuration](./29-1%20NAT%20Configuration.JPG)

## Key Configuration Steps (สรุปขั้นตอนการตั้งค่าหลัก)

### 1. การกำหนด NAT Inside และ Outside Interfaces
```text
R1(config)# interface FastEthernet0/0
R1(config-if)# ip nat outside

R1(config)# interface FastEthernet0/1
R1(config-if)# ip nat inside

R1(config)# interface FastEthernet1/0
R1(config-if)# ip nat inside
```

### 2. การตั้งค่า Static NAT (1-to-1 Mapping)
ตัวอย่างการจับคู่ Internal Web Server IP `10.0.1.10` ให้เป็น Public IP `203.0.113.10`:
```text
R1(config)# ip nat inside source static 10.0.1.10 203.0.113.10
```

### 3. การตั้งค่า Dynamic NAT With Overload (PAT)
การใช้ Standard Access-List เพื่อระบุกลุ่ม Private IP และแปลงออกผ่าน Interface ภายนอกด้วยพารามิเตอร์ `overload`:
```text
R1(config)# access-list 1 permit 10.0.1.0 0.0.0.255
R1(config)# access-list 1 permit 10.0.2.0 0.0.0.255
R1(config)# ip nat inside source list 1 interface FastEthernet0/0 overload
```

## Final Verification
1. **ตรวจสอบตารางการแปลงที่อยู่ของ NAT:**
   ```text
   R1# show ip nat translations
   Pro  Inside global         Inside local          Outside local         Outside global
   tcp  203.0.113.2:1025      10.0.1.100:1025       203.0.113.1:80        203.0.113.1:80
   ---  203.0.113.10          10.0.1.10             ---                   ---
   ```
2. **ตรวจสอบสถิติการแปลงที่อยู่ (NAT Statistics):**
   ```text
   R1# show ip nat statistics
   ```
3. **ทดสอบล้างตาราง Translation หากต้องการรีเซ็ต:**
   ```text
   R1# clear ip nat translation *
   ```
