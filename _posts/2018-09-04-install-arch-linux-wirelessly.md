---
author: reallife
layout: post
title: "ติดตั้ง Arch Linux แต่มีแค่ Wi-Fi นะครับ"
date: 2018-09-04 13:19:00 +0700
description: >
    วันนี้เราจะมาดูกันว่าการติดตั้ง Arch Linux ในแบบที่เราไม่สามารถต่อสาย LAN ได้ จะมีให้ใช้แค่ Wireless บนเครื่อง แล้วเราต้องทำอะไรเพิ่มเติมจากการติดตั้งแบบปกติกันบ้าง
categories: [developer]
tags: [Arch Linux, sdeesreallife]
comments: true
---
![Arch Linux](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,w_400/v1536042431/archlinux-logo-dark-90dpi.ebdee92a15b3.png)

ปกติการติดตั้ง Arch Linux จะมีขั้นตอนให้อย่างละเอียดโดยข้อมูลที่ดีที่สุด ให้ดูได้ที่ [ArchWiki หน้านี้](https://wiki.archlinux.org/index.php/Installation_guide) และสิ่งที่จำเป็นสำหรับการติดตั้งอย่างแรกคือ Live USB ของ Arch Linux ต่อมาเมื่อทำการ boot ด้วย Live USB ขึ้นมาแล้วระบบจะจัดการรัน daemon อย่าง dhcpcd ให้เพื่อเชื่อมต่อเข้า Internet ด้วย LAN แล้วก็ดาวน์โหลดสิ่งต่างๆ มาติดตั้ง โจทย์ของเราในวันนี้คือเมื่อไม่สามารถเอาเครื่องไปต่อ LAN ได้ แล้วจะต้องจัดการตัวเองยังไง?

*ขั้นที่ 0* - ซึ่งถือเป็นขั้นแรกก็คือทำเนียน ทำทุกอย่างตามปกติของการติดตั้ง Arch Linux ซึ่งจะมีขั้นตอนให้อย่างละเอียดโดยข้อมูลที่ดีที่สุด ให้ดูได้ที่ [ArchWiki หน้านี้](https://wiki.archlinux.org/index.php/Installation_guide) หรือที่ [It's Foss หน้านี้ก็ได้](https://itsfoss.com/install-arch-linux/) - แล้วพอก่อนที่เราจะทำการ  `pacstrap /mnt base base-devel`

*ขั้นที่ 1* - ก่อน `pacstrap` ให้เราใช้คำสั่ง `iw dev`
```
$ iw dev
phy#0
	Interface wlp9s0
		ifindex 3
		wdev 0x1
		addr bc:77:37:75:97:1b
		ssid true_home2G_b88
		type managed
		channel 11 (2462 MHz), width: 20 MHz, center1: 2462 MHz
		txpower 15.00 dBm
```
ผลลัพธ์จะได้ออกมาประมาณอย่างที่เห็น (ในตัวอย่างนี้คือหลังจากที่เชื่อมต่อแล้ว จะเห็นค่า ssid ด้วย) นั่นคือเรามี Wireless ให้ใช้ได้อยู่ และปกติ Live USB พอ boot แล้วก็จะมี driver ของ Wireless มาให้เราพร้อมแล้ว การที่เราจะใช้ Wireless เพื่อเชื่อมต่อก็ด้วยการใช้คำสั่ง `wifi-menu` หลังจากสั่งคำสั่งนี้แล้วเครื่องจะค้นหา ssid ที่เจอทั้งหมด แล้วเราก็เห็นผลลัพธ์จะเป็นหน้าจอประมาณนี้ นั่นคือเราก็เลือก Wi-Fi ของเรา ใส่รหัสแล้วทำการเชื่อมต่อเข้าไปเพื่อจะออกเนทในทันที

![wifi-menu](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,w_400/v1536045151/Screenshot_from_2018-09-04_14-08-09.png)

แล้วทีนี้พอเรา `pacstrap` ก็จะไปได้เรื่อยๆ ล่ะ เพราะระบบสามารถดาวน์โหลดทุกอย่างที่ต้องติดตั้งมาได้เรียบร้อย ตรงนี้จะใช้เวลาสักหน่อย ปล่อยเครื่องทำงานไปเรื่อยๆ พอเสร็จจากนี้เราก็ไปทำตามขั้นตอนการติดตั้งอันถัดไป คือ `genfstab` เสร็จแล้วก็มาถึงตอนที่เรา `arch-chroot /mnt`

*ขั้นที่ 2* - อันนี้คือพอเรา `arch-chroot /mnt` เสร็จ เพื่อให้เราสามารถเอา Wireless มาใช้ได้เวลาที่เรา boot กลับขึ้นมาด้วยเครื่องเราเอง (ไม่ใช้ Live USB แล้ว) เราก็ต้องสั่งคำสั่งชุดนี้ คือ
- `pacman -S iw`
- `pacman -S dialog`
- `pacman -S wpa_supplicant`

คำสั่งชุดนี้จะติดตั้งทุกอย่างให้ครบเพื่อที่จะทำให้เรา boot เครื่องด้วย Arch Linux ของเราเองแล้วสามารถที่จะเรียก `wifi-menu` ขึ้นมาเพื่อเชื่อมต่อเข้ากับ Internet ด้วย Wireless ได้อีกครั้ง

*จุดที่ยุ่งยาก:*
1. มีเรื่องที่อาจจะเกิดขึ้นนิดหน่อยตอนที่พอเรา boot ด้วย Arch Linux ของเราเอง แล้วใช้คำสั่ง `iw dev` แต่ไม่มีผลลัพธ์อะไรแสดงขึ้นมาเลย ถ้าเป็นแบบนี้คือให้รู้ว่าถึงตอนนั้นระบบไม่ได้มี driver ไว้ให้แล้ว (เพราะนี่ไม่ใช่ Live USB) เราต้องทำการติดตั้ง driver ให้กับตัว Wireless ของเราเพิ่ม ตัวอย่างเช่นติดตั้ง `pacman -S broadcom-wl` อันนี้เป็น driver ของ Broadcom - สำหรับวิธีการติดตั้งก็อาจจะทำได้โดยให้ boot เอา Live USB กลับมาก่อน จากนั้นทำการ mount แล้วก็ arch-chroot ให้เรียบร้อยแล้วค่อยลง driver
2. ถ้าหลังจากที่ login เข้า GNOME ไปแล้ว แต่ Wi-Fi ยังไม่มีขึ้นมา ให้เราจัดการกับตัว Network Manager ด้วยคำสั่งนี้
- `systemctl enable NetworkManager.service` และ
- `systemctl start NetworkManager.service`

และแล้วเราก็จะได้ Arch Linux มาเป็นของเรา พร้อมกับความรู้ Linux อีกมากมายในระหว่างทาง
