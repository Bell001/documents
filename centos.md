# CENTOS
## INSTALLATION  

Setting by USB Storage (Centos 7)

Set ประเทศ

Set network
* กรณีแรก m1
	* f0
      ```
      IP: 192.168.50.1
      ```
    * f1
      ```
      IP: 158.108.32.160
      Gateway: 158.108.32.129
      DNS 158.108.0.2, 158.108.32.3
      ```
* กรณี 2 m2,m3,m4
  * f1
    ```
    IP 192.168.50.*
    Gateway: 192.168.50.1
    ```
  
Set disk
	Reclaim อันที่เคยใช้ - เอา free space เพิ่ม
	เลือกอันเดิม แต่ click ที่ i will configure partitioning
Disable KDUMP
Set แบบ minimal -  เลือก lib กับอะไรสักอย่าง 

ไปหน้าถัดไป configure
	Root password - maekarootserroom (เอาไว้แปลงกันเอง)
	Create User - สร้างคนนึงเก็บไว้ใน home เลือก admin ด้วย


ปัญหา&ข้อควรระวัง
หลังกด reboot ห้ามดึง usb ทันที เดี๋ยวพัง ดึงตอนเข้าหน้าจอดำๆที่มีข้อความขาวๆข้างบน
Boot failed ไปในหน้าที่ต้องกด F12 เลือกแก้พวกลำดับการ boot เลือกอะไรสักอย่างที่ชื่อนำหน้าด้วย V* มาบูทบนๆ
*มีกรณีแปลกๆ เพิ่ม harddisk ที่ไม่ได้ใข้ boot ด้วย อันที่เพิ่ม fail แต่อัน V* จะใช้ได้ ?? [case m3]

### Testing
```
nmtui
systemctl restart network
ping 8.8.8.8 (DNS server)
ping ku.ac.th
```

### Config hostname /etc/hosts
```
158.108.32.160 hpc
192.168.50.1	m1
192.168.50.2	m2
192.168.50.3	m3
192.168.50.4	m4
```

### Basic library installation
```
yum install wget
yum install epel-release
yum install vim bash-completion net-tools
ifconfig
yum install parted tmux screen
```

### Create user
```
useradd username
gpasswd -a username wheel (คำสั่งลากเข้า root คือเป็น sudo ได้)
passwd username
```

### Passwordless
เข้ามาที่ m1 ก่อน
สร้าง secret key public key ด้วย protocol rsa  
copy public key ไปให้เครื่องอื่น
```
ssh-keygen -t rsa
ssh-copy-id -i .ssh/id_rsa.pub your__host__name
```

### กรณี ssh เข้า m1 ไม่ได้
เอาอันที่เป็น 158.108.32.160 ออก เพราะมันยังลิ้งกับอันเก่าอยู่
```
cd .ssh
vim known_hosts
```

