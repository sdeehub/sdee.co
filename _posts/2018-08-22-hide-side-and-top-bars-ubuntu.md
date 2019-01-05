---
author: reallife
layout: post
title: "ทำยังไงถึงจะซ่อนแถบด้านซ้ายและแถบด้านบนของ Ubutu 18.04 ได้?"
date: 2018-08-22 21:47:00 +0700
description: >
    จะซ่อนแถบด้านซ้าย กับแถบด้านบน ของ Ubuntu จะต้องทำยังไง? เพราะเวลาที่ใช้ Notebook หน้าจอไม่ได้มีเนื้อที่มาก อยากจะซ่อนแถบพวกนี้เหลือเกิน
categories: [developer]
tags: [ubuntu, sdeesreallife]
comments: true
---
จากคำถามนี้ วันนี้พวกเราจะพามาดูคำตอบด้วยวิธีง่ายๆ กันนะครับ ถ้าพร้อมแล้วมาลงมือซ่อนแถบด้านข้างกันก่อนเลย

เข้าไปที่ `Settings` โดยการคลิกที่ปุ่ม `Apps Button` แล้วเลือก `Settings`

![Ubuntu Welcome Screen](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_400/v1535038452/Screenshot_from_2018-08-23_22-10-10.png)

![Apps Button](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_400/v1535038636/Screenshot_from_2018-08-23_22-00-53.png)

หรือคลิกที่แถบด้านบนตรง `System Menu` แล้วคลิกที่ `Settings`

![System Menu ‣ Settings](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_400/v1535038744/Screenshot_from_2018-08-23_21-59-52.png)

ในส่วนของ `Dock` ให้เลือก `Auto-hide the Dock` เป็น `ON`

![Dock ‣ Auto-hide](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_400/v1535038831/Screenshot_from_2018-08-23_21-56-13.png)

แค่นี้แถบด้านข้างก็จะซ่อนเองอัตโนมัติเวลาที่มีหน้าจออื่นเลื่อนมาบังแล้วนะครับ คราวนี้มาถึงแถบด้านบนกันบ้าง

ให้เราคลิกเข้าไปที่ `Apps Button` ‣ `Ubuntu Software` แล้ว `Search` คำว่า `Hide Top Bar` (เป็น Add-ons ในพวก Shell Extensions) แล้วคลิก `Install`

![Ubuntu ‣ Software Hide Top Bar](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_400/v1535039118/Screenshot_from_2018-08-23_22-22-18.png)

แค่นี้แถบด้านบนก็จะซ่อนเองอัตโนมัติเวลาที่มีหน้าจออื่นเลื่อนมาบังแล้วนะครับ สรุปว่าถ้าต้องใช้เครื่องที่หน้าจอไม่ใหญ่มาก เราก็รู้แล้วว่าจะสามารถซ่อนแถบด้านข้าง กับด้านบนได้ยังไง ถึงจะได้เนื้อที่เพิ่มมาไม่มากแต่บางทีการเปลี่ยนแปลงเล็กๆ แบบนี้ก็ช่วยให้พวกเราทำงานได้ง่ายขึ้นมากเหมือนกันนะครับ

และเพราะว่าเมื่อมีเล็กก็ต้องมีใหญ่ ใช่แล้วครับ! ในทางกลับกันสำหรับใครที่เวลาเราไปใช้เครื่อง Desktop แล้วต้องการต่อจอเพิ่มหลายๆ จอ ลองอ่านเรื่องนี้ดูครับ [บน Ubuntu 18.04 จะใช้การ์ดจอที่ต่อเพิ่มพร้อมกันกับ VGA Onboard จะต้องทำยังไง?](https://www.sdee.co/developer/2018/07/20/multiple-vga-cards-on-ubuntu-18-04/) ‣ และแล้วก็สำเร็จเรียบร้อย สำหรับวันนี้บ๊ายบาย ขอตัวไปเข้านอนก่อน ราตรีสวัสดิ์นะครับ ทุกๆ คน
