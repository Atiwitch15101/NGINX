# NGINX

## ขั้นตอนที่ 1 

> ติดตั้ง NGINX บน centOS

```
yum install nginx
```

หรือ

```
yum install -y nginx
```

============================================================================================

## ขั้นตอนที่ 2 

> start service nginx and reboot start nginx

```
systemctl enable --now nginx
```
คำสั่ง systemctl enable --now nginx จะทำการตั้งค่าให้บริการ NGINX เริ่มทำงานโดยอัตโนมัติเมื่อระบบบูต และยังเริ่มต้นบริการ NGINX ในทันทีในขณะที่คุณเรียกใช้คำสั่งนี้
> แสดงสถานะ nginx

```
systemctl status nginx
```

```
firewall-cmd --permanent --add-service http
```
```
firewall-cmd--reload
```

============================================================================================
