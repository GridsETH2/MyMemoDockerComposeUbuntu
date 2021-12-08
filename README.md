# MyMemoDockerComposeUbuntu
Docker Compose คือการจัดการการตั้งค่าที่ซับซ้อนและช่วยให้คุณจดจ่อกับการเขียนโค้ด

**ข้อกำหนดเบื้องต้น**

- Docker Compose อาศัย Docker Engine สำหรับงานที่มีความหมาย ดังนั้นตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Docker Engine ในเครื่องหรือจากระยะไกล ขึ้นอยู่กับการตั้งค่าของคุณ
- บนระบบ Linux ก่อนอื่นให้ติดตั้ง [Docker Engine](https://github.com/GridsETH2/MyMemoDockerEngineUbuntu)
- ในการรัน Compose ในฐานะผู้ใช้ที่ไม่ใช่รูท โปรดดูที่ [Manage Docker ในฐานะผู้ใช้ที่ไม่ใช่รูท](https://docs.docker.com/engine/install/linux-postinstall/)

**ติดตั้ง Docker Compose บนระบบ Linux ในฐานะ Root**

บน Linux คุณสามารถดาวน์โหลด Compose repository บนพื้นที่เก็บข้อมูลใน GitHub Compose repository release page ทำตามคำแนะนำจากลิงค์ ซึ่งเกี่ยวข้องกับการรันคำสั่ง curl ในเทอร์มินัลของคุณ เพื่อดาวน์โหลด

1. เรียกใช้คำสั่งนี้เพื่อดาวน์โหลด Docker Compose รุ่นเสถียรในปัจจุบัน :
~~~
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
~~~
ผลลัพธ์
~~~
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   633  100   633    0     0   6086      0 --:--:-- --:--:-- --:--:--  6086
100 12.1M  100 12.1M    0     0  7813k      0  0:00:01  0:00:01 --:--:-- 14.0M
~~~ 
*หมายเหตุ : หากต้องการติดตั้ง Compose เวอร์ชันอื่น ให้แทนที่ 2.0.1 ด้วยเวอร์ชัน Compose ที่คุณต้องการใช้*

2. กำหนกสิทธิ์ให้ระบบปฏิบัติการกับไบนารี :
~~~
sudo chmod +x /usr/local/bin/docker-compose
~~~
*หมายเหตุ : หากคำสั่ง docker-compose ล้มเหลวหลังการติดตั้ง ให้ตรวจสอบเส้นทางของคุณ คุณยังสามารถสร้างลิงก์สัญลักษณ์ /usr/bin หรือไดเร็กทอรีอื่นในพาธของคุณได้*

ตัวอย่าง :
~~~
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
~~~

3. ทดสอบการติดตั้ง
~~~
docker-compose --version
~~~
ผลลัพธ์
~~~
docker-compose version 1.29.2, build 5becea4c
~~~

เสร็จสิ้นการติดตั้ง docker compose ในฐานะ Root

**กำหนดกลุ่มผู้ใช้** ในการสร้างdockerกลุ่มและเพิ่มผู้ใช้ของคุณ :

1. สร้าง docker กลุ่ม
~~~
sudo groupadd docker
~~~
2. เพิ่มผู้ใช้ของคุณใน docker group
~~~
sudo usermod -aG docker $USER
~~~
3. ออกจากระบบและกลับเข้าสู่ระบบใหม่เพื่อให้สมาชิกกลุ่มของคุณได้รับการประเมินใหม่

หมายเหตุ : บน Linux คุณยังสามารถเรียกใช้คำสั่งต่อไปนี้เพื่อเปิดใช้งานการเปลี่ยนแปลงในกลุ่ม :
~~~
newgrp docker 
~~~
4. ตรวจสอบว่าคุณสามารถรัน `docker` คำสั่งได้โดยไม่ต้องใช้ sudo
~~~
docker run hello-world
~~~

**กำหนดค่า Docker ให้เริ่มทำงานเมื่อบูต**

ลีนุกซ์รุ่นปัจจุบันส่วนใหญ่ (RHEL, CentOS, Fedora, Debian, Ubuntu 16.04 และสูงกว่า) ใช้ systemd เพื่อจัดการบริการที่จะเริ่มทำงานเมื่อระบบบูท บน Debian และ Ubuntu 

บริการ Docker ได้รับการกำหนดค่าให้เริ่มทำงานเมื่อบู๊ตเป็นค่าเริ่มต้น ในการเริ่ม Docker และ Containerd โดยอัตโนมัติ

สำหรับการ เปิดใช้ การเริ่มทำงานอัตโนมัติเมื่อระบบบูท
~~~
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
~~~
สำหรับการ ปิดใช้ การเริ่มทำงานอัตโนมัติเมื่อระบบบูท
~~~
sudo systemctl disable docker.service
sudo systemctl disable containerd.service
~~~
