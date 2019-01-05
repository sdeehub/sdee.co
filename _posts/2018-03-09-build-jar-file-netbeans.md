---
author: x
layout: post
title: "Build JAR File on Netbeans IDE"
date: 2018-03-09 09:10:10 +0700
description: >
   การ Build JAR File ใน Netbeans IDE
categories: [developer]
tags: [netbeans, x]
comments: true
---
สำหรับวันนี้ ผมจะพูดถึงเรื่องการสร้างไฟล์ JAR ใน Netbeans IDE เผื่อมีคนที่ยังไม่รู้ คือแต่ก่อนผมจะใช้ Eclipse ในการพัฒนา คือ Export ออกมาเป็นไฟล์ .jar ได้เลย แต่พอย้ายมาพัฒนาบน Netbeans ตอนแรกก็งงว่าทำยังไง สำหรับใน Blog นี้ผมจะยกตัวอย่างตั้งแต่สร้าง Porject ใหม่เลย เพื่อให้รู้ขั้นตอนละเอียดขึ้น

- ไปที่เมนู File ‣ New Project แล้วเลือก Java ‣ Java Application กด Next

![Create Project](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:20,w_400/v1520847474/jar_1_2018-03-09.png)

ตั้งชื่อ Project คลิกเลือก Create Main Class แล้วกด Finish ไปได้เลย
![Create Project](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:20,w_400/v1520847485/jar_2_2018-03-09.png)

- จากนั้นก็เขียน โปรแกรมของเราขึ้นมา

- กรณีที่เราต้องมีการเรียกใช้งาน Libraries อื่นหรือ Project เดิมที่เคยเขียนไว้แล้ว
   ให้ คลิกขวา ที่ชื่อ Project แล้วไปที่ Properties จะแสดงหน้าต่าง Project Properties ขึ้นมา
   ให้เลือก Libraries ตรง Compile ให้เรา Add Project, Library หรือ JAR ไฟล์ เข้ามาตามที่เราต้องการเรียกใช้งาน

![Create Project](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:20,w_400/v1520847980/jar_3_2018-03-09.png)

- เมื่อเราเขียนโปรแกรมเสร็จแล้วต้องการสร้างไฟล์ JAR ให้คลิกขาที่ชื่อโปรเจ็ค แล้วคลิก Clean and Build เท่านี้ก็จะได้ JAR File ออกมาให้ ซึ่งจะเก็บไว้ที่โฟลเดอร์ชื่อ dist

![Create Project](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:20,w_200/v1520847500/jar_4_2018-03-09.png)

- จากนั้นให้ไปที่โฟลเดอร์โปรเจ็คที่เราสร้างไว้ เราสามารถ run ไฟล์ jar ได้ โดยเข้าไปที่โฟลเดอร์ dist แล้ว พิมพ์คำสั่ง java -jar ตามด้วยชื่อไฟล์ ตัวอย่างของผมคือ java -jar JavaApplication.jar

![Create Project](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:20,w_400/v1520848226/jar_6_2018-03-09.png)
![Create Project](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:20,w_400/v1520848332/jar_7_2018-03-09.png)

- กรณีที่โปรเจ็คมีการเรียกใช้ไฟล์หรือ config ภายนอก ก็ให้เรา copy เข้ามาไว้ ในโฟลเดอร์ dist นี้นะครับ ไม่เช่นนั้นโปรแกรมจะหาไฟล์ ไม่เจอ

- ในกรณีที่โปรแกรมฟ้องเรื่องหา Libraries ที่เราเพิ่มเข้ามาตอนรันไฟล์ jar สามารถแก้ปัญหาได้โดยตั้งค่า Project Properties ตรง Build ‣ Packing ให้คลิกเลือก Copy Dependent Libraries มาด้วยครับ เวลาเรา build jar file มันก็จะ copy Libraries ที่เราเพิ่มเข้ามาไปไว้ในโฟลเดอร์ dist ให้ด้วย เท่านี้ก็เป็นอันเสร็จสิ้นการสร้าง JAR File แล้วครับ

![Create Project](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:20,w_400/v1520848473/jar_5_2018-03-09.png)
