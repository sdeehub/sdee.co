---
author: reallife
layout: post
title: "อัพเกรดมาใช้ Ubutu 18.04 กัน"
date: 2018-06-06 13:21:00 +0700
description: >
    วันนี้ใครพอมีเวลาลองมานั่งอัพเกรด Ubuntu ให้เป็น Ubuntu 18.04 กัน
categories: [developer]
tags: [ubuntu, sdeesreallife]
comments: true
---
![Upgrade to Ubuntu 18.04](https://res.cloudinary.com/sdees-reallife/image/upload/v1528266842/Screenshot_from_2018-06-06_13-30-14.png)

หลังจากที่พวกเราได้เปลี่ยนมาฝักใฝ่กับเส้นทางสาย Open Source ด้วยการหันมาใช้ Ubuntu 17.10 เป็น OS หลักอย่างเต็มตัว ในวันนี้ 06.06.2018 คือวันสำคัญ เพราะว่าเลขสวยด้วย [เป็นวันพระอัฏฐมีบูชาด้วย](https://www.sdee.co/sdees/2018/01/24/buddhist-holy-days-2018/) แล้วเราก็พอมีเวลาว่างพอด้วย ว่างพอสัก 15 นาที พอที่จะมาอัพเกรด Ubuntu บนเครื่องของพวกเราให้เป็น Ubuntu 18.04 LTS กัน - มีอะไรใหม่บ้างใน Version นี้นอกจากที่เป็น LTS ‣ ใช้เวลาประมาณ 3 นาที คลิ๊กดู YouTube ข้างล่างนี้ของ [OMG! UBUNTU!](https://www.youtube.com/user/omgubuntu) ได้เลย

<div style="position:relative;width:100%;height:0;padding-bottom:56.25%;">
<iframe style="width:100%;height:100%;position:absolute;top:0;left:0;" src="https://www.youtube.com/embed/ONXfL6evR0Q" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen>
</iframe>
</div><br/>

สำหรับการอัพเกรดจะใช้เวลาประมาณ 10 นาที ทั้งนี้ขึ้นอยู่กับ Download Speed ของเราด้วย ขั้นตอนทุกอย่างเป็นไปเองด้วยตัวของ OS คือหลังจากที่ Ubuntu 18.04 LTS ได้ถูก Release ออกมาเมื่อวันที่ 26.04.2018 ทุกครั้งหลังจากที่มีการอัพเดทโน่นนี่นั่น ตัว Software Updater จะแนะนำให้เราอัพเกรด OS เป็น 18.04 ด้วย และเพื่อไม่ให้เป็นการเสียเวลา ‣ ตอบตกลงที่จะอัพเกรดไป รอให้ระบบจัดการโน่นนี่นั่นไป เมื่อเสร็จเรียบร้อยต้อง Restart 1 ครั้ง

![Restart after upgrade](https://res.cloudinary.com/sdees-reallife/image/upload/c_crop,x_2000,y_50,w_1000,h_750/w_400,c_scale/Screenshot_from_2018-06-06_12-12-10.png)

เมื่อเครื่องบูทกลับมาอีกครั้งพวกเราก็จะเข้ามาพบกับหน้าจอแนะนำตัว ที่พร้อมแนะนำเรื่องใหม่ๆ ของ Ubuntu 18.04 LTS

![What's new in Ubuntu](https://res.cloudinary.com/sdees-reallife/image/upload/c_crop,x_180,y_50,w_1000,h_750/w_400,c_scale/Screenshot_from_2018-06-06_12-14-43.png)

ถัดมาคือหน้าจอการติดตั้ง Livepatch ที่เราต้องใช้ Account ของ Ubuntu One ร่วมด้วย ถ้าไม่มี Account ก็ให้ทำการ Sign Up ซะเลย

![Livepatch](https://res.cloudinary.com/sdees-reallife/image/upload/c_crop,x_180,y_50,w_1000,h_750/w_400,c_scale/Screenshot_from_2018-06-06_12-21-26.png)

การเปิด Livepatch ไม่ได้มีขั้นตอนอะไรมาก คลิก `Set Up Livepatch...` ทำตามหน้าจอ ถัดมาระบบขอ `sudo` เราก็ให้ไป แล้วพอใส่ Ubuntu One Account ก็เรียบร้อย ‣ ผลลัพธ์จากการ Set Up Livepatch อันนี้จะมีผลดีมากกับเครื่องของเรา และโดยเฉพาะเครื่อง Ubuntu ที่เราเอามาทำเป็น Server เพราะเวลามีอัพเดทที่เกี่ยวกับ Kernel หรือ Security ต่างๆ ระบบจะทำอัพเดทให้ในแบบที่ไม่ต้องมีการ Reboot เครื่อง ขอย้ำตรงที่ "ไม่ต้องมีการ Reboot เครื่อง"

ถัดจากนี้ก็ไม่มีอะไรที่เป็น Big Deal ล่ะ สรุปได้ว่าอัพเกรด Ubuntu ไป 18.04 เรื่องนี้ As easy as pie!

เนื้อหาเพิ่มเติมเกี่ยวกับ Livepatch อ่านได้จากที่นี่: [OMG! UBUNTU!](https://www.omgubuntu.co.uk/2018/04/enable-live-patch-kernel-updates-in-ubuntu-18-04) และ [TechRepublic](https://www.techrepublic.com/article/how-to-set-up-livepatch-and-the-information-gathering-tool-in-ubuntu-18-04/)
