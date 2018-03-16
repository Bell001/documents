# CENTOS 7
## INSTALLATION  

เสียบ USB หากไฟที่หน้าเครื่อง (สีเหลือง) ไม่กระพริ๊บแสดงว่าทำงานอยู่ ให้ กด reboot
ทางตรง - กดที่ปุ่มหน้าเครื่อง
ทางอ้อม - ให้ใส่ cmd ว่า reboot แต่กรณีนี้ต้องทราบรหัส root ไม่งั้นทำไม่ได้ 

เข้าหน้า GUI ของ centos ที่เป็นหน้าขาวๆฟ้าๆ ก่อนเข้าหน้า boot ของระบบ
	ให้กด F12 เพื่อเข้าหน้า setting

หน้า Setting --> Boot ด้วย??
ให้เลือกตามนี้
	Setting by USB Storage (Centos 7) --> Enter
	
เข้าหน้า GUI สำหรับ Install OS Centos 7
สิ่งที่ต้อง Set มีดังนี้
1.Set ประเทศ
	click เลือกประเทศไทย --> Done ที่ซ้ายบน

2.Set network
	* กรณีแรก m1
		* f0
	      ```
	      IP: 192.168.50.1
	      Subnet:
	      ```
	    * f1
	      ```
	      IP: 158.108.32.160
	      Subnet:
	      Gateway: 158.108.32.129
	      DNS 158.108.0.2, 158.108.0.3
      ```
	* กรณี 2 m2,m3,m4
	  * f1
	    ```
	    IP 192.168.50.*
	    Subnet:
	    Gateway: 192.168.50.1
	    DNS 158.108.0.2, 158.108.0.3
	    ```
	select enable network after install ด้วย
  
3.Set disk
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
ตามลำดับนะเพราะว่า net-tools ต้อง install หลัง epel-release ทดสอบโดยใช้ ipconfig
```
yum install wget
yum install epel-release
yum install vim bash-completion net-tools
ifconfig
yum install parted tmux screen
yum group install "Development Tools"
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
ไปแก้ที่ 
(ในเครื่องเราเองนะ คือเข้าไปแก้ไฟล์ลบอันที่เกี่ยวข้องกับ IP นี้ออกให้หมด)
```
.ssh/known_hosts
```

