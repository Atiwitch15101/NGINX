# NGINX Configuration

> ไฟล์คอนฟิกหลักของ NGINX คือ nginx.conf ซึ่งเป็นไฟล์ที่ใช้ในการตั้งค่าต่างๆ ของ NGINX คุณสามารถหาไฟล์ nginx.conf ได้ที่ตำแหน่งต่างๆ ขึ้นอยู่กับระบบปฏิบัติการที่คุณใช้งาน ต่อไปนี้เป็นตำแหน่งที่พบไฟล์ nginx.conf บ่อยๆ ในระบบปฏิบัติการต่างๆ

1. Ubuntu/Debian

```
/etc/nginx/nginx.conf
```

2. CentOS/RHEL/Fedora

```
/etc/nginx/nginx.conf
```

3. MacOS (Homebrew Installation)

```
/usr/local/etc/nginx/nginx.conf
```

5. Windows ถ้าติดตั้ง NGINX ใน Windows โดยใช้ binary package ตำแหน่งไฟล์จะอยู่ในโฟลเดอร์ที่ติดตั้ง NGINX เช่น

```
C:\nginx\conf\nginx.conf
```

> ไฟล์การตั้งค่า `nginx.conf` ของ NGINX มีส่วนประกอบหลักๆ ที่ใช้ในการกำหนดการทำงานของ NGINX โดยทั่วไปจะแบ่งออกเป็นบล็อกการตั้งค่าต่างๆ ดังนี้

1.Directives

    - คำสั่งที่อยู่ในระดับบนสุดของไฟล์และมีผลกับการทำงานของ NGINX ทั้งหมด เช่น การตั้งค่าผู้ใช้และกลุ่มที่ NGINX ทำงานภายใต้, การตั้งค่า worker process เป็นต้น

    - ตัวอย่าง
    
```
user  nginx;
worker_processes  auto;
```

2. http

   - ส่วนนี้ใช้ในการตั้งค่าพารามิเตอร์ที่เกี่ยวข้องกับการจัดการเหตุการณ์ (events) เช่น จำนวนการเชื่อมต่อที่อนุญาตต่อการเชื่อมต่อหนึ่งๆ
