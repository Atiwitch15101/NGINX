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
    
    ```
    user  nginx;
    worker_processes  auto;
    ```

2. http

    - ส่วนนี้ใช้ในการกำหนดการตั้งค่าสำหรับการประมวลผล HTTP requests รวมถึงการตั้งค่าเซิร์ฟเวอร์เสมือน (virtual servers), การตั้งค่า location blocks, การตั้งค่าเกี่ยวกับ proxy, caching และการรักษาความปลอดภัย
     
    ```
    http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    keepalive_timeout  65;

        server {
            listen       80;
            server_name  localhost;
    
            location / {
                root   /usr/share/nginx/html;
                index  index.html index.htm;
            }
    
            error_page   500 502 503 504  /50x.html;
            location = /50x.html {
                root   /usr/share/nginx/html;
            }
        }
    }

    ```

3. mail

   -  ส่วนนี้ใช้สำหรับการกำหนดการตั้งค่าบริการอีเมลพร็อกซี (mail proxy) ซึ่ง NGINX สามารถใช้ในการส่งต่อการเชื่อมต่อ SMTP, IMAP, และ POP3
     
    ```
    mail {
        server {
            listen     143;
            protocol   imap;
            proxy      on;
        }
    }
    ```

4. stream

    - ส่วนนี้ใช้สำหรับการกำหนดการตั้งค่าบริการสตรีมมิ่ง TCP/UDP เช่น การตั้งค่า proxy สำหรับโปรโตคอล TCP หรือ UDP
  
    ```
    stream {
        upstream backend {
            server backend1.example.com:12345;
            server backend2.example.com:12345;
        }
        
        server {
            listen 12345;
            proxy_pass backend;
        }
    }
    ```
    
5. events

    - events ในไฟล์ nginx.conf มีบทบาทสำคัญในการกำหนดการจัดการการเชื่อมต่อและเหตุการณ์ต่างๆ ของ NGINX ซึ่งช่วยเพิ่มประสิทธิภาพและความเสถียรในการให้บริการเว็บหรือแอปพลิเคชันที่มีการเชื่อมต่อเข้ามาจำนวนมากๆ

    ```
   events {
        worker_connections 1024;
        multi_accept on;
        use epoll;
    }
    ```
