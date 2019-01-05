---
author: reallife
layout: post
title: "รูปแบบที่ใช้เวลาจะเขียน Post"
date: 2017-11-22 17:55:47 +0700
description: >
  If you are our website's writer: **READ THIS FIRST!** • สำหรับทุกคนที่จะเขียน blog ลงที่นี่: **กรุณาอ่านเนื้อหานี้ก่อน!**
categories: [developer]
tags: [hydejack, post, sdeesreallife]
comments: true
---

เพื่อให้เกิดความสอดคล้องไปในทิศทางเดียวกันที่ดูง่ายและสะดวกสำหรับการเข้ามาใช้งานที่ website นี้ ในหน้าที่ต่างๆ กันของ: คนเขียน / คนอ่าน / และ machine (ในการแปลง format) เราจึงขอสร้างข้อตกลงต่างๆ ทั้งหมดสำหรับการเขียน post เอาไว้ในที่นี้

### สารบัญ
{:.no_toc}
* TOC Here!
{:toc}
### Front Matter

หัวไฟล์ของ Markdown (.md file) จะมีหัวข้อตามตัวอย่างข้างล่างนี้
~~~
---
author: reallife
layout: post
title: "รูปแบบที่ใช้เวลาจะเขียน Post"
date: 2017-11-22 17:55:47 +0700
description: >
  If you are our website's writer: **READ THIS FIRST!** • สำหรับทุกคนที่จะเขียน blog ลงที่นี่: **กรุณาอ่านเนื้อหานี้ก่อน!**
categories: [developer]
tags: [hydejack, post]
comments: true
---
~~~
### Headers

สำหรับการเขียนหัวข้อ เราตกลงให้มีใช้กัน 2 ขนาด คือ
* หัวข้อใหญ่ ให้ใช้ `###` (header3) และ
* หัวข้อเล็กลง ให้ใช้ `####` (header4)

~~~
### หัวข้อใหญ่
#### หัวข้อเล็กลง
~~~

อันนี้เป็นข้อแนะนำสำหรับความสวยงาม อ่านเนื้อหาได้สบายตา และ เกี่ยวข้องโดยตรงกับรูปแบบที่จะถูกแปลงเนื้อหาของหน้าที่เขียน ในการที่จะให้ระบบทำ `สารบัญ - TOC {:toc}` ให้เราด้วยโดยอัตโนมัติ

_หมายเหตุ:_ สำหรับ {:toc} จะสร้าง link มาจาก header ที่เราเขียน (พบว่า link ที่สร้างมาจะใช้ได้เฉพาะกับ header คำภาษาอังกฤษเท่านั้น)
### Images

ขนาดของรูปที่ไม่ใช่รูปที่เกิดจากการ embedded ให้ใช้:
* รูปเล็ก 200x200
* รูปทั่วไป 400x200
* รูปยาว 800x100

![Cover image 200x200](/assets/img/authors/reallife/2017-11-22/200x200.png)

![Story image 400x200](/assets/img/authors/reallife/2017-11-22/400x200.png)

![BarLine image 800x100](/assets/img/authors/reallife/2017-11-22/800x100.png)

_หมายเหตุ:_ ใช้ Inline `+ style="border-radius:50%"` ในกรณีให้ Cover image กลม / ใช้ tag `{:.lead}` ดึงรูปยาวให้เต็ม และใช้ tag `{:.lead}` กับ text และ blockquote เพื่อเน้นข้อความได้ด้วย

<img src="/assets/img/authors/reallife/2017-11-22/200x200.png" alt="Cover image 200x200 (Circle)" style="border-radius:50%">

![BarLine image 800x100 (lead)](/assets/img/authors/reallife/2017-11-22/800x100.png){:.lead}

### Blocks
สำหรับการใช้ block แนะนำให้แยกการใช้ block แบบต่างๆ ตามนี้คือ:
* coding block - ใช้สำหรับการเขียนถึงภาษาโปรแกรม - coding (สำหรับภาษาที่รองรับให้ดูเพิ่มเติมได้ที่ [Rouge](https://github.com/jneen/rouge))
* blockquote - สำหรับใช้กับการ quote หรือข้อความที่อ้างถึง เพราะระบบสามารถจะทำ large quote ให้ได้ด้วย
* message block - สำหรับใช้เน้นข้อความทั่วๆ ไปในกล่องข้อความ

_หมายเหตุ:_ รูปแบบ font ใน coding block จะเป็น font **มาตรฐาน** ส่วน blockquote และ message block จะใช้ font **สวยงาม** ตามปกติของหน้าเว็บ
