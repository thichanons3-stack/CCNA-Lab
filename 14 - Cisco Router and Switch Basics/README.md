# CCNA Lab: Cisco Router and Switch Basics

## Lab Overview
แล็บนี้เป็นการฝึกปฏิบัติการตั้งค่าพื้นฐานบนอุปกรณ์ Cisco Routers และ Switches โดยครอบคลุมหัวข้อสำคัญ:
- การกำหนดชื่ออุปกรณ์ (**Hostname Configuration**)
- การตั้งค่า IP Address และ Subnet Mask ให้กับ Interface และการเปิดใช้งานพอร์ตด้วยคำสั่ง `no shutdown`
- การตั้งค่า Console Line Timeout (`exec-timeout`) เพื่อความสะดวกและปลอดภัยในการเข้าถึง CLI
- การตรวจสอบสถานะการทำงานของ Interface และการทดสอบการเชื่อมต่อระดับ Layer 3 (Ping)

## Network Topology
![14 Cisco Router and Switch Basics](./14%20Cisco%20Router%20and%20Switch%20Basics.jpg)

## Key Configuration Steps (สรุปขั้นตอนการตั้งค่าหลัก)

### 1. การกำหนดชื่ออุปกรณ์และตั้งค่า Interface บน R1
```text
R1# configure terminal
R1(config)# hostname R1
R1(config)# interface FastEthernet0/0
R1(config-if)# ip address 10.10.10.1 255.255.255.0
R1(config-if)# no shutdown
```

### 2. การกำหนดค่า Console Timeout บน R1
ป้องกันไม่ให้หน้าจอ CLI หลุดระหว่างการทำงานเป็นเวลา 30 นาที:
```text
R1(config)# line con 0
R1(config-line)# exec-timeout 30 0
```

### 3. การตั้งค่าบน R2
```text
R2# configure terminal
R2(config)# hostname R2
R2(config)# interface FastEthernet0/0
R2(config-if)# ip address 10.10.10.2 255.255.255.0
R2(config-if)# no shutdown
R2(config-if)# exit
R2(config)# line con 0
R2(config-line)# exec-timeout 30 0
```

## Final Verification
ตรวจสอบสถานะพอร์ตและการเชื่อมต่อด้วยคำสั่งมาตรฐาน:
```text
R1# show ip interface brief
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            10.10.10.1      YES manual up                    up

R1# ping 10.10.10.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.10.10.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5)
```
