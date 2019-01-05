---
author: reallife
layout: post
title: "บน Ubuntu 18.04 จะใช้การ์ดจอที่ต่อเพิ่มพร้อมกันกับ VGA Onboard จะต้องทำยังไง?"
date: 2018-07-20 11:47:00 +0700
description: >
    หลายคนอาจจะคุ้นเคยกับการใส่การ์ดจอเพิ่มบนเครื่อง PC แล้วก็หันไปใช้งานจากการ์ดจอนั้นแทนการ์ดจอที่มาเป็นแบบ Onboard ‣ แต่คราวนี้ถ้าบังเอิญเราเกิดจะต้องใช้งานทั้ง 2 สิ่งนั้นพร้อมๆ กันล่ะ - ต้องทำยังไง?
categories: [developer]
tags: [ubuntu, sdeesreallife]
comments: true
---
![Dual Screens Ubuntu](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_400/v1532061257/2018-07-20_11-32-59.png)

จริงๆ แล้วเรามีขั้นตอนแรกแค่ขั้นตอนเดียวที่เราต้องทำก็คือเข้า BIOS ไปจัดการตั้งค่าก่อนว่าเราจะใช้งานการ์ดจอทั้ง 2 อันคือทั้ง Onboard และที่ใส่เพิ่มเข้าไปพร้อมๆ กัน หลักการและขั้นตอนมีอยู่แค่นั้นจริงๆ

คราวนี้ในส่วนของรายละเอียด เอาเป็นว่ามาดูจากเครื่องตัวอย่างที่ใช้ Mainboard ของ ASUS ก็แล้วกันนะครับ ‣ ตอนบูทเครื่องให้กด `F2` หรือ [จากเนื้อหานี้ของ ASUS](https://www.asus.com/support/FAQ/1017796/) ให้กด `Delete` ซึ่งจริงๆ ก็คือเอาเป็นว่ากดคีย์ให้ถูกและกดให้ทัน เป้าหมายก็คือกดเข้า BIOS ให้ได้ก็แล้วกัน

จากนั้นไปที่ `Advanced Mode` ‣ `Advanced` ‣ `System Agent Configuration` ‣ `Graphics Configuration` ถึงตรงนี้ต้องทำการตั้งค่าให้

- `Primary Display` คือการ์ดจอหลักที่จะให้แสดงผลซึ่งสามารถเลือกได้ทั้ง `Auto` คือระบบเลือกให้ ถ้ามีการใส่การ์ดจอเพิ่มก็จะไปใช้การ์ดจอนั้นเป็นหลักหรือถ้าเอาการ์ดที่เพิ่มนั้นออกก็จะเปลี่ยนกลับไปแสดงผลด้วย VGA Onboard แทน ส่วนถ้าเราจะบังคับเลือกไปเองก็ได้ ซึ่ง `iGPU` ก็คือ Onboard และ `PCIE` ก็คือการ์ดจอที่เราใส่เพิ่ม
- อีกค่าที่ต้องดูก็คือ `iGPU Multi-Monitor` ต้องเป็น `Enabled`

จากการตั้งค่าตรงนี้เสร็จแล้วกด `F10` เพื่อ Save และออกจาก BIOS พอรีบูทเข้า Ubuntu ก็จะได้ผลลัพธ์เป็นที่น่าพอใจคือสามารถใช้การ์ดจอที่มีต่อกับ Monitor เพิ่มได้หลายหน้าจอตามที่เราต้องการ

![Multi Screens Ubuntu](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_600/v1532060466/2018-07-20_10-45-33.png)

คราวนี้บน Ubuntu พอเรามีหลายหน้าจอขึ้นมาจริงๆ นอกจากการตั้งค่าหน้าจอตามปกติแล้ว

![Ubuntu Displays Setting](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_400/v1532060532/2018-07-20_11-15-14.png)

สิ่งที่เราสามารถปรับเลือกการแสดงผลเพิ่มเติมได้ก็ต้องด้วย GNOME Tweaks ‣ ทำการติดตั้งตัวนี้ซะ! โดยไปที่ `Ubuntu Software` แล้ว `Search` หา `GNOME Tweaks` แล้วเลือก `Install`

![GNOME Tweaks](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_400/v1532060536/2018-07-20_11-16-13.png)

สำหรับตัว Tweak นี้จะทำให้เราสามารถตั้งค่าต่างๆ เกี่ยวกับการแสดงผลหน้าจอได้มากขึ้น อย่างเช่นให้แสดง Wallpaper ยาวต่อเนื่องกันไปทุกๆ หน้าจอ ‣ `Appearance` แล้วตรง `Background` กดเลือกรูปจากที่เก็บไฟล์ไว้ใน `Folder: Pictures` แล้วเลือกการแสดงผลเป็น `Spanned`

![GNOME Tweaks Spanned Wallpaper](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_400/v1532060481/2018-07-20_11-13-29.png)

ผลลัพธ์ที่ได้ก็จะขึ้นอยู่กับรูปภาพที่เราเอามาใช้ด้วยเช่นกันแบบนี้

![Ubuntu Spanned 3 Screens Wallpaper](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_600/v1532060545/2018-07-20_11-18-03.png)

ที่ว่ามานี้พวกเรารู้ว่าน่าจะทำให้ทุกๆ คนรู้สึกสนุกและได้ประโยชน์จากการใช้งาน Ubuntu และการ์ดจอที่เรามีอยู่กันอย่างเต็มที่มากขึ้นนะครับ ‣ พอมาถึงตรงนี้ก็จะต้องส่งยิ้มหวานให้กัน พร้อมกับบ๊ายบายแล้วเจอกันใหม่ บ๊ายบายและสวัสดีนะครับ :)
