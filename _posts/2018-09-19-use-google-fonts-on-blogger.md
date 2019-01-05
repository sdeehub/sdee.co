---
author: reallife
layout: post
title: "บน Blogger ถ้าจะเปลี่ยนมาใช้ Google font ต้องทำแบบนี้"
date: 2018-09-19 15:29:47 +0700
categories: [developer]
tags: [blogger, sdeesreallife]
description: >
    ต้องการเปลี่ยน font ที่จะใช้บน Blogger มาเป็น Google font ที่มีตัวหนังสือภาษาไทยสวยๆ ต้องทำยังไงดี?
---
![Blogger Logo](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,w_200/v1537345937/blogger_logo.png)

ต่อไปนี้เป็นวิธีที่เราใช้ในการเปลี่ยน font บน Blogger โดยจะทำการเปลี่ยนมาใช้ Google font ทั้งที่แสดงผลบน Desktop และ Mobile แต่ส่วนว่าจะใช้ font ไหนกันบ้าง อันนี้ก็แล้วแต่ความชอบ ‣ เริ่มจากไปที่ [Google font](https://fonts.google.com/) เพื่อเลือกดู font ต่างๆ

![Google fonts](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_600/v1537422482/Screenshot_2018-09-20_Google_Fonts.png)

พอใจกับ font ที่จะใช้แล้วให้คลิก `(+)` แล้วเปิดไปดูที่ `EMBED` ‣ `STANDARD` เสร็จแล้วก็มาที่ Blogger เพื่อทำตามขั้นตอนต่อไปนี้ได้เลย:

*(1)* - `Login` เข้า Blogger แล้วเปิดไปที่ `Theme` ‣ คลิกที่ `Edit HTML`

![Blogger Theme](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_600/v1537346319/Screenshot_2018-09-19_Blogger_Odd_s_Horizon_-_Theme.png)

*(2)* - หลังจาก `<head>` tag เราก็จะเอา `<link>` tag ของ Google font ที่เราเลือกใช้ใส่ลงไป ‣ เสร็จแล้วคลิก `Save theme`
ในตัวอย่างนี้คือเราจะใช้ font: Athiti และ Prompt ก็จะใส่ไปแยก 2 อันเลยเพื่อความชัดเจน เวลาเรากลับมาอ่าน หรือมาแก้ทีหลังได้ดูง่ายๆ หน่อย

```
<link href='https://fonts.googleapis.com/css?family=Athiti' rel='stylesheet'/>
<link href='https://fonts.googleapis.com/css?family=Prompt' rel='stylesheet'/>
```
![Link tag](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_600/v1537422491/Screenshot_2018-09-20_Blogger_Odd_s_Horizon_-.png)

*(3)* - คลิก `Back` กลับมาที่หน้า Theme อีกครั้ง ‣ คราวนี้ คลิกที่ `Customize`

![Blogger Theme](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_600/v1537346319/Screenshot_2018-09-19_Blogger_Odd_s_Horizon_-_Theme.png)

*(4)* - ที่เมนูด้านซ้าย คลิกไปที่ `Advanced` แล้วเลื่อนลงไปล่างสุดเพื่อคลิก `Add CSS` ‣ เพิ่ม Code CSS ลงไป

```
.post-body { font-family: 'Athiti', sans-serif; }
.post-title { font-family: 'Prompt', sans-serif; }
.mobile h3.post-title { font: normal 20px Prompt; }
.mobile-index-title { font: normal 20px Prompt; }
```

![Add CSS](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_600/v1537422499/Screenshot_2018-09-20_Blogger_Odd_s_Horizon_-_Template_Designer.png)

ตรงนี้ 2 บรรทัดแรกเราจะกำหนด font ให้กับ .post-body และ .post-title ซึ่งอาจจะพอแค่ 2 บรรทัดนี้ก็ได้

*เพิ่มเติม:* ส่วน 2 บรรทัดที่เหลือเป็นการกำหนดเพิ่มเข้าไปเพราะการแสดงผลบน Mobile ของเรายังไม่ได้ font อย่างที่เราอยากได้ ก็เลยบอกเพิ่มในส่วนของ .mobile post-title กับ .mobile-index-title ลงไปด้วย

*(5)* - คลิก `Apply to Blog` ที่ด้านขวาบน ‣ คลิก `<< Back to Blogger`

*(6)* - กลับมาที่หน้า Theme อีกครั้ง ‣ คราวนี้ คลิกที่รูปเกียร์ ใต้ส่วน Mobile

![Blogger Theme](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_600/v1537346319/Screenshot_2018-09-19_Blogger_Odd_s_Horizon_-_Theme.png)

*(7)* - คลิกที่ `Choose mobile theme` เปลี่ยนค่าจาก `Default` ‣ ให้เป็น `Custom` แล้วคลิก `Save`

![Mobile theme default](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_600/v1537422505/Screenshot_2018-09-20_Blogger_Odd_s_Horizon_-_Theme.png)

![Mobile theme custom](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_600/v1537422512/Screenshot_2018-09-20_Blogger_Odd_s_Horizon_-_Theme_1.png)

และแล้วขั้นตอนทั้งหมดก็จบลง เราก็จะได้ Blogger ที่มี font สวยงามดั่งใจ คราวนี้ก็ขอให้ลงมือ blog กันได้อย่างเต็มที่เต็มอารมณ์ พร้อมด้วย font ที่งามๆ กันเน้อ
