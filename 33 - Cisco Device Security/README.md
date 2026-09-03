# CCNA Lab: Cisco Device Security Configuration

## Lab Overview
แล็บนี้เป็นการฝึกปฏิบัติการรักษาความปลอดภัยขั้นพื้นฐานบนอุปกรณ์ Cisco Router และ Switch เพื่อป้องกันการเข้าถึงอุปกรณ์โดยไม่ได้รับอนุญาต (Unauthorized Access Hardening) โดยครอบคลุมหัวข้อสำคัญ:
- การตั้งรหัสผ่านสำหรับเข้าสู่โหมด Privileged EXEC ด้วย **`enable secret`** (เข้ารหัสแบบ Strong Hash)
- การเข้ารหัสรหัสผ่านที่แสดงผลใน Running-Config ด้วย **`service password-encryption`**
- การสร้างบัญชีผู้ใช้เฉพาะบุคคล (**Local Usernames**) พร้อมกำหนดระดับสิทธิ์ (**Privilege Levels**)
- การเปิดใช้งานและการตั้งค่าการเชื่อมต่อระยะไกลแบบปลอดภัยด้วย **SSH Version 2** (แทนที่ Telnet ที่ส่งข้อมูลเป็น Plaintext)
- การกำหนดค่า Security Best Practices เช่น Login Banners, Login Block (ป้องกัน Brute-force Attack), และ Console/VTY Exec Timeout

## Network Topology
![Cisco Device Security](./33-1%20Cisco%20Device%20Security%20Configuration.jpg)

## Key Configuration Steps (สรุปขั้นตอนการตั้งค่าหลัก)

### 1. การกำหนดรหัสผ่าน Enable Secret และการเข้ารหัสรหัสผ่านทั้งระบบ
```text
R1(config)# enable secret cisco
R1(config)# service password-encryption
```

### 2. การสร้างบัญชี Local User และระดับสิทธิ์ (Privilege Level 15)
```text
R1(config)# username admin privilege 15 secret cisco123
```

### 3. การกำหนด Domain Name และสร้างคีย์สำหรับ SSH (RSA Keys)
```text
R1(config)# ip domain-name lab.local
R1(config)# crypto key generate rsa modulus 1024
R1(config)# ip ssh version 2
```

### 4. การตั้งค่า Line VTY ให้รับเฉพาะการเชื่อมต่อผ่าน SSH เท่านั้น
```text
R1(config)# line vty 0 4
R1(config-line)# transport input ssh
R1(config-line)# login local
R1(config-line)# exec-timeout 15 0
```

### 5. การป้องกัน Brute-Force Attacks (Login Block)
บล็อกการล็อกอินเป็นเวลา 60 วินาที หากมีการล็อกอินล้มเหลว 3 ครั้งภายใน 30 วินาที:
```text
R1(config)# login block-for 60 attempts 3 within 30
```

## Final Verification
1. **ตรวจสอบสถานะการทำงานของ SSH บน Router:**
   ```text
   R1# show ip ssh
   SSH Enabled - version 2.0
   Authentication timeout: 120 secs; Authentication retries: 3
   ```
2. **ทดสอบการเชื่อมต่อผ่าน SSH จากเครื่อง Client:**
   ```text
   PC> ssh -l admin 10.0.0.1
   Open
   Password: [cisco123]
   R1#
   ```
3. **ตรวจสอบว่า Telnet ถูกปิดการใช้งาน (Connection Refused):**
   ```text
   PC> telnet 10.0.0.1
   % Connection refused by remote host
   ```
