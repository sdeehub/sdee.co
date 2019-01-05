---
author: reallife
layout: post
title: "ติดตั้ง Nvidia Driver บน Ubutu 18.04"
date: 2018-06-06 18:54:00 +0700
description: >
    หลังจากติดตั้ง Ubuntu 18.04 (หรืออัพเกรดมาก็ได้) หากเรามีความจำเป็นต้องติดตั้ง VGA Driver ของ Nvidia จะมีขั้นตอนยังไง มาดูกันได้เลย
categories: [developer]
tags: [ubuntu, nvidia, sdeesreallife]
comments: true
---
ขั้นตอนแรกคือเปิด Terminal ด้วย `Ctrl-Alt-t` แล้วพิมพ์คำสั่งนี้ลงไป `ubuntu-drivers devices`

~~~
$ ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0 ==
modalias : pci:v000010DEd00000DF5sv00001028sd000004CAbc03sc00i00
vendor   : NVIDIA Corporation
model    : GF108M [GeForce GT 525M]
driver   : nvidia-340 - distro non-free
driver   : nvidia-driver-390 - distro non-free recommended
driver   : xserver-xorg-video-nouveau - distro free builtin
~~~

ผลลัพธ์ที่ได้จะมีความหมายบอกว่าเครื่องของเราใช้การ์ดจอจากผู้ขาย (vendor) คือ `NVIDIA Corporation` และในตัวอย่างนี้จะบอกว่ารุ่นที่ใช้ (model) คือ `GF108M [GeForce GT 525M]` ‣ ในบรรทัดที่เขียนว่า `driver   : nvidia-driver-390 - distro non-free recommended` หมายถึง Driver ที่แนะนำให้ใช้

พอได้ข้อมูลมาแบบนี้แล้ว เราก็จะใช้คำสั่ง `sudo ubuntu-drivers autoinstall` เพื่อติดตั้ง Driver ตามที่แนะนำว่าเราต้องใช้ หลังจากการติดตั้งผ่านไปเรียบร้อย Reboot เครื่อง และกลับเข้ามากดที่ Apps Button หรือปุ่ม Show Applications เรียก NVIDIA X Server Settings ขึ้นมาดู ถือว่าเป็นอันเสร็จพิธี

![NVIDIA X Server Settings](https://res.cloudinary.com/sdees-reallife/image/upload/c_crop,x_2000,y_50,w_1000,h_750/w_400,c_scale/Screenshot_from_2018-06-06_19-12-47.png)

*หมายเหตุ:* การติดตั้ง Driver นี้จะช่วยทำให้การแสดงผลทางหน้าจอต่างๆ ดีขึ้น และยังช่วยให้การกำหนดคุณสมบัติของ Display Devices ถูกต้องมากขึ้นด้วย
