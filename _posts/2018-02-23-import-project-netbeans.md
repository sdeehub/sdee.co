---
author: x
layout: post
title: "Import Eclipse Project to Netbeans"
date: 2018-02-23 09:10:10 +0700
description: >
    การ Import Project ของ Eclipse ใน Netbeans
categories: [developer]
tags: [netbeans, x]
comments: true
---
เมื่อไม่นานมานี้ มีเหตุต้องเปลี่ยน OS จาก Windows มาใช้ Ubuntu แทน ทำให้งานที่ทำอยู่ มีปัญหาเรื่องโปรแกรม คือเดิมใช้ Eclipse ในการพัฒนาโปรแกรมด้วยจาวาอยู่ แล้วมีโปรเจ็คที่ต้องใช้ SWT ซึ่งเป็น GUI Toolkit ตัวหนึ่ง

ทีนี้เจ้าตัว Plugin ที่ใช้คือ WindowBuilder ของ Eclipse ดันมี Bug ซะนี่ ทำให้งานที่ทำต้องสะดุดไป ทำไงดีล่ะทีนี้ ผมก็เลยไปพิจารณาดูว่ามี GUI Toolkit ตัวอื่นที่ใช้แทนได้ไหมใน Eclipse แล้วไม่ต้องใช้ WindowBuilder ผมหาอยู่นานไม่เจอแฮะ ชักเริ่มเสียเวลาแล้ว

จึงตัดสินใจลองเปลี่ยนวิธีดู ใน Netbeans ก็มีเจ้าตัว Swing ที่มาพร้อมกับ Netbeans เลยน่าจะใช้ได้และไม่มีปัญหา เลยลองไปเล่นตัว Swing บน Netbeans ดู ผลปรากฎว่าผมชอบกว่าตัว SWT ซะอีก เลยตัดสินใจที่จะเปลี่ยน จาก Eclipse ไปใช้ Netbeans เพื่อที่จะได้ใช้เจ้า Swing ได้เต็มที่

สำหรับการ Import โปรเจ็คเดิมที่ทำบน Eclipse ให้ไปอยู่ใน Netbeans ก็มีขั้นตอนง่ายๆ ต่อไปนี้
1. ไปที่เมนู `File` ‣ `Import Project` ‣ `Eclipse Project...`
![Import Eclipse Project to Netbeans](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:20,w_400/v1519483012/import.png)

2. เลือก `Import Project ignoring Project Dependencies`

   - ที่ `Project to Import:` ให้ `Browse...` ไปที่โฟลเดอร์โปรเจคของ Eclipse ที่ต้องการ Import
   - ที่ `Destination Folder:` ให้ `Browse...` ไปที่โฟลเดอร์ที่ต้องการบันทึกโปรเจ็คใหม่
   แล้วคลิก `Finish`  
![Import Project ignoring Project Dependencies](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:20,w_400/v1519482689/project_des.png)

3. กรณีที่เกิด Import issues ขึ้น ให้ Close ก่อน แล้วจะมี Popup แสดง Project Problems ให้ คลิก `Resolve Problems` เพื่อแก้ปัญหา

   - ที่ Resolve Project Problems ให้คลิก `Resolve...` จะแสดงหน้าต่างให้เลือกไฟล์ หาไฟล์นั้น แล้วคลิก `OK` ทำจนครบทุกไฟล์ แล้วคลิก `Close` ปิดหน้าต่างนั้น
![Resolve Project Problems](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:20,w_400/v1519481280/resolve.png)
![Resolve File](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:20,w_400/v1519483264/resolve_file.png)
เท่านี้ก็เป็นอันเสร็จสิ้นขั้นตอนการ Import Project ที่พัฒนาบน Eclipse เข้ามาพัฒนาต่อที่ Netbeans แล้ว
