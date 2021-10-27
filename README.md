# MyMemoDockerComposeUbuntu
Docker Compose คือการจัดการการตั้งค่าที่ซับซ้อนและช่วยให้คุณจดจ่อกับการเขียนโค้ด

**ข้อกำหนดเบื้องต้น**

- Docker Compose อาศัย Docker Engine สำหรับงานที่มีความหมาย ดังนั้นตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Docker Engine ในเครื่องหรือจากระยะไกล ขึ้นอยู่กับการตั้งค่าของคุณ
- บนระบบ Linux ก่อนอื่นให้ติดตั้ง [Docker Engine](https://github.com/GridsETH2/MyMemoDockerEngineUbuntu)
- ในการรัน Compose ในฐานะผู้ใช้ที่ไม่ใช่รูท โปรดดูที่ [Manage Docker ในฐานะผู้ใช้ที่ไม่ใช่รูท](https://docs.docker.com/engine/install/linux-postinstall/)

**ติดตั้ง Docker Compose บนระบบ Linux**

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

เสร็จสิ้นการติดตั้ง docker compose
