---
author: reallife
layout: post
title: "อ้าวเหรอ!? เรื่องใหม่จากกูเกิ้ลเหรอ!?"
date: 2018-06-20 12:53:00 +0700
description: >
    2 วันนี้มี 2 เรื่องใหม่จากกูเกิ้ลที่เพิ่งเคยใช้ คือ Android Messages ที่เป็น Web Client (อันนี้เพิ่งจะ Roll Out ออกมาให้ได้ใช้กัน เมื่อสักวัน สองวันนี้ - 19/06/2018) กับ Chrome Remote Desktop (อันนี้มีมาสักพักล่ะ แต่เราเพิ่งจะมาลองใช้กัน) ‣ มาดูกันว่าการใช้งานจะเป็นประโยชน์ยังไงกันบ้างนะครับ
categories: [developer]
tags: [tool, sdeesreallife]
comments: true
---
เริ่มจากเรื่องที่ 1 คือ Android Messages ที่เป็น Web Client - ด้วยสิ่งนี้จะทำให้เราสามารถใช้งานรับ-ส่ง SMS จากหน้าเว็บได้ สิ่งที่ต้องมีก็คือ Android Phone และ Browser ของเรา (เหมือนกับที่เราใช้ Apple's iMessages + Mac) การจะใช้งานนั้นง่ายมากๆ คือเปิด browser บนเครื่อง PC หรือเครื่อง Mac ของเราแล้วไปที่ [https://messages.android.com/](https://messages.android.com/)

![messages.android.com](/assets/img/authors/reallife/2018-06-20/Screenshot_from_2018-06-20_13-40-58.png)

หยิบมือถือที่เป็น Android ของเราขึ้นมาแล้วทำตามขั้นตอน 1 2 3 คือเปิดแอปที่ใช้รับ-ส่ง SMS อันนี้จะต้องเป็น [Android Messages](https://play.google.com/store/apps/details?id=com.google.android.apps.messaging&hl=en)

![Messages on Phone](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_280/v1529480266/Screenshot_20180620-125709.png)

แล้วจิ้มที่ปุ่มเมนูอันที่มีจุด 3 จุด

![Menu button](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_280/v1529480271/Screenshot_20180620-135148.png)

เลือก "Messages for web" แล้วทำการ Scan QR Code ที่เห็นบนหน้าเว็บเป็นอันเสร็จพิธี

![Scan QR Code](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_280/v1529480269/Screenshot_20180620-125723.png)

หลังจากนี้ก็รับ-ส่ง SMS จากบนหน้าเว็บแทนการใช้มือถือได้เลย

เหลืออีกเรื่องคือ Chrome Remote Desktop - อันนี้ก็ติดตั้งและใช้งานได้ง่ายๆ เช่นกัน สำหรับบน PC หรือ Mac จะติดตั้งเป็น Extension อยู่บน Google Chrome (บวกกับลงโปรแกรมอีกนิดหน่อย ตามที่มีหน้าจอให้เราติดตั้งเวลาที่จะใช้งาน)

![Chrome Remote Desktop Extension](/assets/img/authors/reallife/2018-06-20/Screenshot_from_2018-06-19_11-47-35.png)

ส่วนบนมือถือก็ติดตั้ง Chrome Remote Desktop จาก Play Store หรือ App Store

![Chrome Remote Desktop App](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_280/v1529480263/Screenshot_20180619-112219.png)

การตั้งค่าบนเครื่องของเราตรงไป-ตรงมาครับ มี 2 Mode ให้เลือก แต่ละแบบมีการใช้ Key และ Pin สำหรับให้อีกฝั่งเอาไปกรอกตอนที่จะเชื่อมต่อเข้ามา

![Chrome Remote Desktop](/assets/img/authors/reallife/2018-06-20/Screenshot_from_2018-06-19_11-21-33.png)

แล้วในการใช้งานก็จะทำให้เราสามารถ Remote เข้ามาใช้งานบนเครื่องของเราได้จากทุกที่ ที่มีเนทและจากมือถือก็ได้

![Remote Desktop on Android](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_280/v1529480261/Screenshot_20180619-112212.png)

บนมือถือจะมี mode ของการใช้ mouse (เวลาคลิกคือลากเอา mouse pointer ไปวางแล้วจิ้มที่หน้าจอ แต่ถ้าจิ้มด้วย 2 นิ้วก็จะเป็นการคลิกขวา) นอกจากนี้ยังมี mode การใช้ pointer และก็ keyboard อีกด้วย

![Ubuntu on Remote](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_280/v1529916514/Screenshot_20180625-114834.png)

*หมายเหตุ:* เรื่องที่สำคัญมีติดอยู่นิดนึงตรงที่ว่า ถ้าจะใช้บน Ubuntu 18.04 จะคล้ายๆ ว่ามีประเด็นการติดตั้งให้ระวังอยู่นิดหน่อย เพื่อไม่ให้เกิด Bug ‣ ส่วนรายละเอียดเป็นยังไงอ่านได้จาก [Post นี้บน Medium เลยครับ](https://medium.com/@vsimon/how-to-install-chrome-remote-desktop-on-ubuntu-18-04-52d99980d83e)

สำหรับ Chrome Remote Desktop บน Mac High Sierra [อ่านจากตรงนี้สักนิดนึงครับ](https://productforums.google.com/forum/#!msg/chrome/74-SmPsADbI/Lixe_9_GAQAJ)
