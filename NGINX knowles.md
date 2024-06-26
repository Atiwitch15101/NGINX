# NGINX

> NGINX (อ่านว่า "เอนจิ้นเอ็กซ์") เป็นซอฟต์แวร์ที่ทำหน้าที่เป็นเว็บเซิร์ฟเวอร์และรีเวิร์สพร็อกซี ซึ่งออกแบบมาเพื่อให้มีประสิทธิภาพสูงและสามารถจัดการกับการร้องขอจำนวนมากได้อย่างรวดเร็ว นอกจากนี้ NGINX ยังสามารถทำหน้าที่เป็นพร็อกซีสำหรับอีเมลและเป็นโหลดบาลานเซอร์ในการกระจายโหลดไปยังเซิร์ฟเวอร์หลายเครื่องได้

============================================================================================

## การโหลดบาลานซ์ (Load Balancing) ของ NGINX

> คือการกระจายการรับส่งข้อมูลจากผู้ใช้ไปยังเซิร์ฟเวอร์หลายเครื่องเพื่อให้ระบบสามารถรองรับการเชื่อมต่อและการร้องขอจำนวนมากได้อย่างมีประสิทธิภาพ โดยมีวัตถุประสงค์หลักคือเพื่อเพิ่มประสิทธิภาพ ความเสถียร และความพร้อมใช้งานของบริการ
ตัวอย่างในชีวิตจริง

> [!NOTE]
> ### ตัวอย่างเอาให้เข้าใจง่าย
> 1. ร้านอาหารที่มีหลายเคาน์เตอร์รับออเดอร์
>   - มีลูกค้าหลายคนเข้ามาสั่งอาหารในเวลาเดียวกัน แต่ละเคาน์เตอร์จะมีพนักงานรับออเดอร์หลายคน เมื่อมีลูกค้าเข้ามา ระบบจะกระจายลูกค้าไปยังเคาน์เตอร์ที่ว่าง เพื่อไม่ให้เกิดการรอคิวนานที่เคาน์เตอร์ใดเคาน์เตอร์หนึ่ง
> 2. การจราจรในเมือง
>   - มีหลายทางแยกที่มีสัญญาณไฟจราจรเพื่อจัดการการจราจร ระบบสัญญาณไฟจราจรจะช่วยกระจายการเคลื่อนที่ของรถยนต์ไปยังถนนต่างๆ เพื่อลดการจราจรติดขัดในเส้นทางหลักเส้นทางเดียว
> ### ดังนั้น โหลดบาลานจะทำให้ระบบสามารถจัดการกับการใช้งานที่เพิ่มขึ้นได้อย่างมีประสิทธิภาพและเสถียรภาพ

============================================================================================

## Content Cache ของ NGINX

> การเก็บข้อมูล (content) ไว้ในหน่วยความจำเพื่อลดเวลาที่เซิร์ฟเวอร์ต้องดึงข้อมูลจากแหล่งต้นฉบับของข้อมูล เมื่อมีผู้ใช้ร้องขอข้อมูลเดิมอีกครั้ง หรือมีผู้ใช้ร้องขอข้อมูลที่มีลักษณะเดียวกัน นั่นจะช่วยลดการทำงานของเซิร์ฟเวอร์และเพิ่มประสิทธิภาพในการให้บริการ

> [!NOTE]
> ### ตัวอย่างเอาให้เข้าใจง่าย
> สมมติว่าเรามีเว็บไซต์ข่าวที่มีการประกาศข่าวใหม่ๆ ทุกๆ ชั่วโมง ถ้าเราเปิดใช้งาน NGINX Content Cache ข้อมูลที่แสดงในหน้าเว็บไซต์จะถูกเก็บไว้ในหน่วยความจำ หากมีผู้ใช้เข้ามาอ่านข่าวเดิมที่มีการแสดงผลเหมือนเดิม หรือมีผู้ใช้ร้องขอข่าวที่มีลักษณะเดียวกัน ข้อมูลจะถูกดึงมาจากหน่วยความจำโดยตรง ไม่ต้องไปขอข้อมูลจากเซิร์ฟเวอร์หรือแหล่งข้อมูลต้นฉบับ ซึ่งทำให้เว็บไซต์ทำงานได้เร็วขึ้นและประหยัดทรัพยากรของเซิร์ฟเวอร์
> ### ดังนั้น ในทางปฏิบัติ การใช้ NGINX Content Cache ช่วยลดโหลดการทำงานของเซิร์ฟเวอร์และเพิ่มประสิทธิภาพในการให้บริการเว็บไซต์ให้กับผู้ใช้งานได้มากขึ้น

============================================================================================

## เว็บเซิร์ฟเวอร์ ของ NGINX

> NGINX เป็นเว็บเซิร์ฟเวอร์ที่ทำหน้าที่รับและตอบกลับคำร้องขอ (HTTP requests) จากผู้ใช้งานบนเว็บไซต์ ดังนั้น การทำหน้าที่เป็นเว็บเซิร์ฟเวอร์หมายถึงการจัดการกับการเชื่อมต่อที่เกิดขึ้นระหว่างเว็บเบราว์เซอร์ของผู้ใช้และเซิร์ฟเวอร์ที่เก็บข้อมูลของเว็บไซต์

> [!NOTE]
> ### ตัวอย่างเอาให้เข้าใจง่าย
> เว็บเซิร์ฟเวอร์เป็นนักแสดงในโรงละคร ผู้เข้าชม (เว็บบราวเซอร์) มาถึงโรงละคร (เว็บไซต์) เพื่อดูการแสดง (ข้อมูลบนเว็บ) และนักแสดง (เซิร์ฟเวอร์) ก็จะแสดงการแสดง (ข้อมูล) ตามที่ผู้เข้าชมต้องการ และยังตอบสนองต่อคำถามหรือคำร้องขอของผู้เข้าชมด้วย
> ### ดังนั้น เว็บเซิร์ฟเวอร์ (NGINX) จะทำหน้าที่เช่นเดียวกับนักแสดง ซึ่งเป็นบทบาทสำคัญในการให้บริการข้อมูลและเนื้อหาให้กับผู้ใช้งานบนเว็บไซต์

============================================================================================

## Reverse Proxy ของ NGINX

> NGINX เป็นโปรแกรมรีเวิร์สพร็อกซี (Reverse Proxy) ซึ่งหมายถึงการทำหน้าที่แปลงและส่งคำร้องขอ (requests) จากผู้ใช้งานไปยังเซิร์ฟเวอร์ (server) หลังเว็บไซต์ (backend server) ที่เก็บข้อมูลหรือเนื้อหาต่างๆ ซึ่ง NGINX สามารถทำหน้าที่เหล่านี้ได้อย่างมีประสิทธิภาพและมีความเสถียรมาก

> [!NOTE]
> ### ตัวอย่างเอาให้เข้าใจง่าย
> คิดว่า NGINX คือตัวกลางที่เป็นแม่แบบของเว็บไซต์ที่ให้บริการเป็นสองส่วน ส่วนหน้า (Frontend) ที่เป็นหน้าตาของเว็บไซต์ที่ผู้ใช้เห็น และส่วนหลัง (Backend) ที่เป็นที่เก็บข้อมูลและประมวลผลต่างๆ
> เมื่อมีผู้ใช้งานเข้ามายังเว็บไซต์ คำร้องขอจะถูกส่งไปยัง NGINX ก่อน NGINX จะนำคำร้องขอนั้นไปยังเซิร์ฟเวอร์หลัง (backend server) เพื่อให้เซิร์ฟเวอร์ดำเนินการตามคำร้องขอ และเมื่อมีการตอบกลับ (response) จากเซิร์ฟเวอร์ NGINX ก็จะนำข้อมูลนั้นกลับมาส่งให้ผู้ใช้งาน ซึ่งผู้ใช้งานจะไม่รู้ว่าเซิร์ฟเวอร์ที่ตอบกลับเป็นเซิร์ฟเวอร์จริงๆ หรือ NGINX ก็ได้
> ### สรุปได้ว่า NGINX เป็นตัวกลางที่ช่วยป้องกันเซิร์ฟเวอร์จากการโจมตี (เพราะผู้ใช้งานจะไม่สามารถเข้าถึงเซิร์ฟเวอร์โดยตรง) และช่วยแบ่งเบาภาระการทำงานของเซิร์ฟเวอร์โดยส่งคำร้องขอไปยังเซิร์ฟเวอร์หลังที่เหมาะสม

============================================================================================

## Security Controls ของ NGINX

> NGINX Security Controls คือ การตั้งค่าและการใช้งานฟีเจอร์ต่างๆ ของ NGINX เพื่อเพิ่มระดับความปลอดภัยของระบบ เช่น การป้องกันการโจมตี DDoS, การบล็อกการเข้าถึงที่ไม่มีอำนาจ, การเข้ารหัสข้อมูล และอื่นๆ อีกมากมาย ตัวอย่างการใช้งาน NGINX Security Controls เป็นดังนี้

  1. DDoS Protection (การป้องกันการโจมตี DDoS)
    - การใช้งาน NGINX ในการตั้งเป็น Reverse Proxy เพื่อกรองและบล็อกการโจมตี DDoS ก่อนที่จะเข้าถึงเซิร์ฟเวอร์จริงๆ ช่วยลดผลกระทบจากการโจมตีได้อย่างมีประสิทธิภาพ 

  2. Access Control (การควบคุมการเข้าถึง)
    - ใช้ NGINX เพื่อกำหนดเงื่อนไขการเข้าถึงเซิร์ฟเวอร์ เช่น การบล็อก IP Address ที่มีพฤติกรรมที่ไม่ปกติ การใช้งาน HTTP Basic Authentication เพื่อควบคุมการเข้าถึงข้อมูล
  
  3. SSL/TLS Encryption (การเข้ารหัสข้อมูลด้วย SSL/TLS)
    - การใช้งาน NGINX เพื่อเข้ารหัสข้อมูลที่ถ่ายโอนผ่านเครือข่ายด้วย SSL/TLS เพื่อป้องกันการดักจับข้อมูล (Man-in-the-Middle Attack) และการล่วงรหัสข้อมูล
     
  5. Web Application Firewall (WAF)
    - การใช้งาน NGINX เพื่อสร้างกฎและการตรวจสอบแพทเทิร์นของการโจมตีในระดับแอพพลิเคชัน (Web Application Firewall) เพื่อป้องกันการโจมตีต่างๆ เช่น SQL Injection, Cross-Site Scripting (XSS) และอื่นๆ
     
  7. Logging and Monitoring (การบันทึกและการตรวจสอบการใช้งาน)
    - การใช้งาน NGINX เพื่อบันทึกการเข้าถึงและการใช้งานของระบบ และใช้เครื่องมือตรวจสอบ (Monitoring Tools) เพื่อตรวจสอบการดำเนินการของเซิร์ฟเวอร์และค้นหาสัญญาณของการโจมตี

### การใช้ NGINX Security Controls ช่วยป้องกันระบบและข้อมูลจากการโจมตีและเพิ่มระดับความปลอดภัยให้กับเว็บไซต์และแอพพลิเคชันอย่างมีประสิทธิภาพ

============================================================================================

## Dynamic Modules ของ NGINX

> NGINX Dynamic Modules คือ โมดูลที่สามารถโหลดและเปิดใช้งานได้ใน NGINX โดยไม่ต้องคอมไพล์ NGINX ใหม่ทุกครั้งที่ต้องการเพิ่มหรือเปลี่ยนแปลงฟังก์ชันหรือโมดูลใหม่ๆ ซึ่งช่วยเพิ่มความยืดหยุ่นในการปรับแต่ง NGINX ตามความต้องการของแต่ละโปรเจ็กต์หรือแอปพลิเคชันได้ด้วยง่าย

> [!NOTE]
> ### ตัวอย่างเอาให้เข้าใจง่าย
> คิดว่า NGINX เป็นตึกสำหรับออกแบบและสร้างอาคาร โมดูลต่างๆ ใน NGINX ก็เหมือนเป็นวัสดุสร้างอาคาร เราสามารถเพิ่มโมดูลได้ตามความต้องการของอาคาร เช่น เพิ่มโมดูลสร้างลิฟท์ เพิ่มโมดูลเพลงสำหรับอาคาร หรือเพิ่มโมดูลสร้างป้ายโฆษณา เราไม่ต้องสร้างตึกใหม่ทุกครั้งที่เราต้องการเพิ่มสิ่งเหล่านี้ เราเพียงแค่เพิ่มโมดูลลงไปในตึกที่มีอยู่แล้ว
> ### ใน NGINX Dynamic Modules เราสามารถเพิ่มหรือเปลี่ยนโมดูลได้โดยไม่ต้องคอมไพล์ NGINX ใหม่ นั่นหมายความว่าเราสามารถปรับแต่งหรือเพิ่มฟังก์ชันใหม่ๆ ให้กับ NGINX ได้อย่างสะดวกและรวดเร็ว

============================================================================================

## Streaming Media ของ NGINX

> NGINX Streaming Media หมายถึงการใช้ NGINX เป็นเซิร์ฟเวอร์สำหรับสตรีมสื่อต่างๆ เช่น วิดีโอ ออดิโอ หรือเสียง ไปยังผู้ใช้งาน โดยเฉพาะในกรณีที่ต้องการสตรีมสื่อแบบ real-time หรือที่เรียกว่า Streaming Media นั้นๆ เพื่อให้ผู้ใช้สามารถดูหรือฟังไฟล์สื่อได้ทันทีโดยไม่ต้องรอให้ไฟล์ดาวน์โหลดเสร็จก่อน

> [!NOTE]
> ### ตัวอย่างเอาให้เข้าใจง่าย
> คิดว่า NGINX เป็นตัวกลางที่ถ่ายทอดข้อมูลการสตรีมสื่อ มันเปรียบเสมือนเป็นท่อน้ำที่ส่งน้ำไปยังบ้านของผู้ใช้งาน โดยการใช้ NGINX ในการสตรีมสื่อ สามารถให้บริการการสตรีมวิดีโอสด (live streaming) หรือการสตรีมวิดีโอที่ถูกเรียกดูโดยผู้ใช้งานจากเซิร์ฟเวอร์ได้ทันที โดยผู้ใช้งานไม่ต้องรอให้ไฟล์ดาวน์โหลดเสร็จก่อน การสตรีมสื่อแบบ real-time จะช่วยเพิ่มประสิทธิภาพในการนำเสนอข้อมูลและสร้างประสบการณ์การใช้งานที่ดีขึ้นสำหรับผู้ใช้งาน

============================================================================================
