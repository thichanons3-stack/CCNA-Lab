# CCNA Lab: VLAN and Inter-VLAN Routing Configuration

## Lab Overview
แล็บนี้เป็นการศึกษาและฝึกปฏิบัติการแบ่งส่วนเครือข่ายด้วย Virtual Local Area Network (VLAN) และการเชื่อมต่อระหว่างเครือข่ายเสมือนด้วย Inter-VLAN Routing บนอุปกรณ์ Cisco Switches และ Routers โดยครอบคลุม:
- การสร้างและตั้งชื่อ **VLAN (VLAN Database Configuration)** บน Switch
- การกำหนดพอร์ตเป็น **Access Port** และผูกเข้ากับ VLAN แต่ละกลุ่ม
- การตั้งค่า **802.1Q Trunk Port** สำหรับส่งต่อทราฟฟิกรวมระหว่าง Switch และ Router
- การทำ **Inter-VLAN Routing** แบบ Router-on-a-Stick (ROAS) ผ่าน Sub-interfaces หรือ Layer 3 Switch

## Network Topology
![VLAN and Inter-VLAN Routing](./22-1%20VLAN%20and%20Inter-VLAN%20Routing%20Configuration.jpg)

## Key Configuration Steps (สรุปขั้นตอนการตั้งค่าหลัก)

### 1. การสร้าง VLAN บน Switch
```text
SW1(config)# vlan 10
SW1(config-vlan)# name Engineering
SW1(config-vlan)# vlan 20
SW1(config-vlan)# name Sales
```

### 2. การกำหนด Access Ports ให้กับ Client Devices
```text
SW1(config)# interface FastEthernet0/1
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 10

SW1(config)# interface FastEthernet0/2
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 20
```

### 3. การเปิดใช้งาน Trunk Link และการตั้งค่า Router-on-a-Stick
* **บน Switch (Trunk Port):**
  ```text
  SW1(config)# interface GigabitEthernet0/1
  SW1(config-if)# switchport mode trunk
  ```
* **บน Router (Sub-interfaces & 802.1Q Encapsulation):**
  ```text
  R1(config)# interface GigabitEthernet0/0
  R1(config-if)# no shutdown

  R1(config)# interface GigabitEthernet0/0.10
  R1(config-subif)# encapsulation dot1Q 10
  R1(config-subif)# ip address 192.168.10.1 255.255.255.0

  R1(config)# interface GigabitEthernet0/0.20
  R1(config-subif)# encapsulation dot1Q 20
  R1(config-subif)# ip address 192.168.20.1 255.255.255.0
  ```

## Final Verification
1. ตรวจสอบ VLAN และสถานะพอร์ตบน Switch:
   ```text
   SW1# show vlan brief
   SW1# show interfaces trunk
   ```
2. ตรวจสอบสถานะ Sub-interfaces และ Routing Table บน Router:
   ```text
   R1# show ip interface brief
   R1# show ip route
   ```
3. ทดสอบการ Ping ข้าม VLAN จากเครื่องลูกข่ายใน VLAN 10 ไปยัง VLAN 20
