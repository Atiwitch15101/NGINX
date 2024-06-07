# NGINX Configuration

-  NGINX Configuration ที่ประกอบด้วย directive ต่างๆ ที่ใช้ในการกำหนดค่าและการทำงานของเซิร์ฟเวอร์ NGINX สามารถเป็นดังนี้:

```
server {
    listen 80;
    server_name example.com;

    location / {
        root /var/www/html;
        index index.html;
    }

    location /images/ {
        alias /var/www/images/;
    }

    location /admin/ {
        proxy_pass http://admin-backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    error_page 404 /404.html;
    error_page 500 502 503 504 /50x.html;
}
```

### ในตัวอย่างข้างบน
  - `server` directive ใช้กำหนดการตั้งค่าสำหรับเซิร์ฟเวอร์นั้นๆ
  - `listen` directive ใช้กำหนดพอร์ตที่เซิร์ฟเวอร์จะเปิดให้รองรับการเชื่อมต่อ
  - `server_name` directive ใช้กำหนดชื่อโดเมนของเซิร์ฟเวอร์
  - `location` directive ใช้กำหนดการตั้งค่าสำหรับเส้นทาง URL หรือโฟลเดอร์ต่างๆ
  - `root` directive ใช้กำหนดไดเร็กทอรีหลักของเว็บไซต์
  - `index` directive ใช้กำหนดไฟล์ index ที่จะใช้ในกรณีที่ไม่มีไฟล์ index ที่ระบุมา
  - `alias` directive ใช้กำหนดพาธสำหรับโฟลเดอร์ในการเรียกใช้งานภายในเซิร์ฟเวอร์
  - `proxy_pass`, `proxy_set_header` directive ใช้กำหนดการตั้งค่าสำหรับการส่งคำขอไปยังเซิร์ฟเวอร์หลัง (backend server) ในกรณีที่ใช้ Reverse Proxy
  - `error_page` directive ใช้กำหนดหน้าเว็บที่จะแสดงในกรณีเกิดข้อผิดพลาดบางประการ

### ทุกๆ directive ใน NGINX Configuration จะมีหน้าที่และการใช้งานต่างๆ โดยต้องปรับเปลี่ยนตามความต้องการของเซิร์ฟเวอร์และแอปพลิเคชันของคุณ

> [!NOTE]
> ### ตัวอย่างง่ายๆ
> คิดว่า NGINX เป็นร้านอาหาร
>   - Master Process เป็นผู้จัดการร้านที่ดูแลการทำงานของพนักงานทั้งหมด ควบคุมดูแลการทำงานและแก้ปัญหาต่างๆ
>   - Worker Processes เป็นพนักงานเสิร์ฟที่คอยรับออร์เดอร์จากลูกค้า นำออร์เดอร์ไปให้เชฟ และนำอาหารมาเสิร์ฟให้ลูกค้า
> ผู้จัดการร้าน (Master Process) จะดูแลและสั่งการพนักงาน (Worker Processes) เพื่อให้การบริการลูกค้าเป็นไปอย่างราบรื่นและมีประสิทธิภาพ
