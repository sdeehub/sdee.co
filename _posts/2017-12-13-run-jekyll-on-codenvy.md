---
author: reallife
layout: post
title: "รัน Jekyll บน Codenvy"
date: 2017-12-13 18:14:38 +0700
description: >
    ในการทำงานกับ Jekyll เรามักจะทำการติดตั้ง Jekyll กันบนเครื่อง local แล้วส่งงานขึ้นไปให้ host ไว้ที่ GitHub Pages ‣ วิธีนี้ใช้งานได้ดีเมื่อเราทำงานคนเดียวบนเครื่อง local ของเรา แต่ถ้าต้องการทำงานมากกว่า 1 คน หรือในกรณีที่เราต้องการใช้งานจากเครื่องอื่นด้วยล่ะ?
categories: [developer]
tags: [jekyll, codenvy, sdeesreallife]
comments: true
---
เมื่อในทีมมีหลายๆ คนที่จะต้องเข้ามาทำการอัพเดท site ของเราร่วมกัน (หรือในกรณีที่เราต้องการใช้งานจากเครื่องอื่นได้ด้วย) ‣ การติดตั้ง Jekyll เพิ่มที่แต่ละเครื่องและทำการ config ให้แต่ละเครื่องพร้อมใช้งาน site ของเราเป็นเรื่องที่สามารถทำได้ แต่เพื่อให้สะดวกกว่านั้น วันนี้เราจะมาติดตั้ง Jekyll กันบน [Codenvy](https://codenvy.com/) เพื่อให้ทุกๆ คนในทีมสามารถทำงานกับ site ของเราได้บน cloud workspace ‣ ขั้นตอนที่เราต้องทำก็คือ:

#### สมัครใช้งานเปิด account บน Codenvy
เมื่อเสร็จเรียบร้อยจากขั้นตอนนี้ เข้าใช้งาน Codenvy ได้แล้ว ในนั้นเราจะสร้างทีมและ workspace ที่ติดตั้ง Jekyll ไว้ให้ทุกคนเข้ามาอัพเดท site กัน
#### เพิ่ม stack สำหรับติดตั้ง Jekyll โดยใช้ docker file: [sunix/jekyll4che](https://hub.docker.com/r/sunix/jekyll4che/~/dockerfile/)

* ที่เมนูด้านซ้าย คลิกที่ `Stacks` ‣ `Build Stack From Recipe` ‣ `FROM sunix/jekyll4che`
* ตั้งชื่อ stack แล้วกด `SAVE` (สีเขียว)

![new stack](/assets/img/authors/reallife/2017-12-13/2017-12-14_13-31-10.png)
![docker file](/assets/img/authors/reallife/2017-12-13/2017-12-14_11-48-34.png)
![save stack](/assets/img/authors/reallife/2017-12-13/2017-12-14_11-49-24.png)

#### สร้าง workspace ขึ้นมา
ในกรณีถ้าจะสร้าง workspace ให้ทุกคนในทีมใช้ร่วมกัน ให้สร้างทีมก่อน - อ่านรายละเอียดเกี่ยวกับทีมที่นี่ [Teams in Codenvy](https://codenvy.com/docs/user-guide/teams/index.html) เสร็จจากสร้างทีมค่อยสร้าง workspace ให้เป็นของทีมนั้น ‣ การสร้างทีมให้คลิก `Create Team` ใส่ชื่อทีม และเพิ่มสมาชิกในทีม สมาชิกมี 2 แบบ คือ `Team Developer` สำหรับผู้ใช้งานในทีม กับ `Team Admin` สำหรับผู้ใช้งานในทีมที่ต้องจัดการสมาชิก ดูแลและตั้งค่าต่างๆ ของทีมด้วย

ตอนสร้าง workspace ‣ คลิกที่ `Create Workspace` ให้ใส่ชื่อ workspace แล้วเลือกว่าเป็นแบบส่วนตัว หรือ เลือกให้เป็นของทีม

* ในส่วน `SELECT STACK` ให้เลือก stack ของ Jekyll ที่เราเพิ่งจะเพิ่มกันไปเมื่อสักครู่นี้

![select stack](/assets/img/authors/reallife/2017-12-13/2017-12-14_11-54-02.png)

* ในส่วน `PROJECTS` ตรงนี้จะให้เอาข้อมูลมาจาก GitHub Pages ที่เป็น site ของเรา ‣ เลือก Git แล้วใส่ URL ลงไป (หรือถ้า login ด้วย GitHub เลือกที่ GitHub แล้วเลือกไปที่ repository ที่เป็น site ของเราก็ได้) พอเลือกได้แล้วคลิก `Add` (สีฟ้า) แล้วก็คลิก `CREATE` (สีเขียว)

![git project](/assets/img/authors/reallife/2017-12-13/2017-12-14_16-55-05.png)
![project added](/assets/img/authors/reallife/2017-12-13/2017-12-14_17-02-58.png)

* หลังจากระบบทำ workspace ให้เสร็จเรียบร้อย ที่ Terminal ด้านล่าง `ls -la` จะเห็นว่ามีโฟลเดอร์ของ Jekyll อยู่ด้วย ‣ `cd` เข้าไปที่ site project และสั่งรัน `bundle install`

~~~bash
user@a07075b78942:/projects$ ls -la
total 4
drwxr-xr-x  3 user root   27 Dec 14 04:58 .
drwxr-xr-x 22 root root  258 Dec 14 09:08 ..
drwxr-xr-x 18 user user 4096 Dec 14 05:30 sdeesreallife
user@a07075b78942:/projects$ cd sdeesreallife
user@a07075b78942:/projects/sdeesreallife$ bundle install
~~~

#### ทำ custom run command นิดหน่อย แล้วสั่งรัน
ตั้งชื่อและใส่รายละเอียดในส่วนของ `Command Line` และ `Preview URL`

~~~bash
Command Line:
cd ./sdeesreallife              # ชื่อโฟลเดอร์ที่เป็น site project ของเรา
jekyll serve --host=0.0.0.0     # หรือ bundle exec jekyll serve --host=0.0.0.0

Apply to                        # ให้เลือก `YES`

Preview URL:
http://${server.port.4000}/
~~~

![custom run command](/assets/img/authors/reallife/2017-12-13/2017-12-14_17-44-01.png)
![run command details](/assets/img/authors/reallife/2017-12-13/2017-12-15_18-05-31.png)
![preview link](/assets/img/authors/reallife/2017-12-13/2017-12-14_18-01-32.png)

สั่งรัน และ คลิกดูผลลัพธ์ได้จาก preview link ต่อจากนี้เราก็สามารถเข้ามาจัดการอัพเดท/แก้ไข site ของเราที่ workspace นี้ได้จากทุกเครื่อง ทุกที่ ทุกเวลา

สำหรับการใช้งานร่วมกันหลายๆ คนในทีมบน workspace นี้ ต้องเข้าไปเพิ่มผู้ใช้มาไว้ที่ workspace นี้ด้วยอีกนิดนึง ‣ คลิกที่เมนู Workspaces ด้านซ้าย แล้วคลิกที่ Configure workspace (ขวามือรูปเกียร์ตรงกลางใต้คอลัมน์ `ACTIONS`) ‣ คลิกที่ `Share` ‣ คลิก `+ Add Developer` แล้วเพิ่มผู้ใช้งานเข้าไป

![set workspace](/assets/img/authors/reallife/2017-12-13/2017-12-15_17-39-06.png)
![](/assets/img/authors/reallife/2017-12-13/2017-12-15_17-40-51.png)

คราวนี้ทุกคนก็เข้ามาช่วยกันได้ล่ะ พออัพเดทข้อมูลทุกอย่างเรียบร้อยพร้อมจะเอาขึ้นเว็บแล้วก็แค่ git push กลับขึ้นไปที่ repository ก็เท่านั้น ยิ้มหวานสบายใจกันไปทุกๆ คน - ขอขอบคุณ Jekyll, GitHub และ Codenvy สำหรับเทคโนโลยีของพวกเขาไว้ณ.ที่นี้ด้วย :)