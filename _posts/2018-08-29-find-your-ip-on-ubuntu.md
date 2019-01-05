---
author: reallife
layout: post
title: "บน Ubutu เราดูค่า IP กันตรงไหน?"
date: 2018-08-29 11:18:00 +0700
description: >
    ปกติถ้าเป็นบน Windows พวกเราก็จะเข้า Dos แล้วใช้คำสั่งว่า `ipconfig` เพื่อดูค่า IP, ค่า Subnet อะไรต่างๆ แต่พอมาอยู่บน Ubuntu (หรือคำสั่งของ Unix) ต้องใช้คำสั่งอะไร ดูตรงไหนได้บ้าง?
categories: [developer]
tags: [ubuntu, sdeesreallife]
comments: true
---
![ipconfig](https://res.cloudinary.com/sdees-reallife/image/upload/w_200,h_200,r_max,x_45,y_35,c_crop/v1535516845/ipconfig-command.gif)

*วิธีที่ 1 แบบที่เป็น GUI* - เข้าไปที่ `Settings` ‣ `Network` หรือ `Wi-Fi` แล้วแต่ว่าเครื่องของเราตอนนั้นต่อด้วยสาย หรือไร้สาย แล้วคลิกที่ไอคอนรูปเกียร์ จะได้ข้อมูลที่เราต้องการ

![network settings](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_400/v1535523799/Screenshot_from_2018-08-29_12-18-21.png)

![wi-fi settings](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_400/v1535523800/Screenshot_from_2018-08-29_12-18-40.png)

ถัดมาจากวิธีที่ 1 ที่เป็น GUI ก็เหลือแต่ที่จะต้องใช้คำสั่ง ‣ เริ่มจากการเปิด Terminal ด้วย `Ctrl - Alt - t`

- `hostname -I` - อันนี้ดูจะง่ายสุด ผลลัพธ์ที่ได้ก็เรียบง่ายด้วยเช่นกัน คือบอกค่า IP ที่เราต้องการรู้
- `ip addr` - แบบนี้คือใช้คำสั่ง ip แล้วบอกให้แสดง address หรือจะดูค่าอย่างอื่นก็ได้ด้วย เช่น `ip route`, `ip neigh` แบบนี้เป็นต้น สำหรับรายละเอียดทั้งหมดของคำสั่งก็ดูด้วย `man ip` ได้เลย
- `ifconfig -a` - คำสั่งนี้เขียนและให้ความรู้สึกคล้ายๆ กับ `ipconfig /all` ‣ ifconfig ย่อมาจาก Interface configuration เป็นคำสั่งที่ทำอะไรได้มากมายกับ Network interface ยกตัวอย่างจากเว็บนี้ [HowtoForge](https://www.howtoforge.com/linux-ifconfig-command/) ใช้ `ifconfig` ทำอะไรไป 7 อย่างพร้อมคำอธิบายด้วย

จากทั้งหมดนี้คิดว่าได้ทำให้พวกเราหาค่า IP กันได้แล้วนะ แต่ว่ามีหมายเหตุเล็กๆ 2 อย่างก่อนจบ
- ถ้าเรียกคำสั่งไม่ได้ก็อย่าลืม `sudo apt install net-tools` ให้เรียบร้อยซะก่อน
- ใน Browser สามารถ Google ลงไปว่า `ip` แต่อันนี้จะได้ผลลัพธ์เป็น ip จริงของเรา เอาล่ะ! จบแค่นี้นะครับ
