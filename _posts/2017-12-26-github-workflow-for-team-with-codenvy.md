---
author: reallife
layout: post
title: "Workflow ดี ทีมงานก็มีความสุข"
date: 2017-12-26 08:37:16 +0700
description: >
    GitHub เป็นสิ่งที่ developer ทุกคนคุ้นเคย และ ใช้งานกันได้เป็นอย่างดี สำหรับวันนี้เราจะมาดูข้อตกลงกันสักหน่อยว่าพวกเราจะใช้งาน GitHub และ Codenvy กันยังไงเอาแบบที่ให้เกิดเป็น workflow สำหรับใช้งานร่วมกันในทีม แล้วทุกคนมีรอยยิ้มไปพร้อมๆ กัน
categories: [developer]
tags: [github, codenvy, workflow, sdeesreallife]
comments: true
---
<img src="/assets/img/authors/reallife/2017-12-26/github.png" alt="GitHub Logo">

สภาพแวดล้อมการทำงานของเราจะมี GitHub และ Codenvy บวกกับทีมงานที่ผ่านการคัดเลือกให้ทุกคนได้เข้าร่วม read/write แก้ไข code บน repository ของเราได้ สำหรับที่ branch: `master` ถือเป็นปลายทางของงานซึ่งจะผ่านการ deploy แบบอัตโนมัติทันทีออกไปที่ GitHub Pages, Heroku หรือ cloud based อื่นๆ ตามที่เลือกใช้ ส่วนห้อยท้ายของ workflow เรามองว่าเปิดความเป็นไปได้ให้กับเพื่อนๆ FC, groupie หรือผู้ที่ใช้งานมากกว่าทั่วๆ ไป มีความสนใจเข้ามา request ให้ออก feature ใหม่ๆ หรือแจ้ง bug การใช้งานไว้ อะไรแบบนี้ก็สามารถทำได้ด้วยเช่นกัน ‣ จากที่ว่ามานี้มีผลทำให้เราได้ขั้นตอนการทำงานออกมาประมาณนี้คือ:

### ขั้นตอนการทำงาน
{:.no_toc}
* TOC Here!
{:toc}
### New issue
ทุกครั้งที่จะมีการปรับเปลี่ยน, เพิ่มเติม, แก้ไขอะไร เราจะเริ่มต้นด้วยการออก issue ใหม่ใน GitHub ขึ้นมาก่อน ตรงนี้จะเป็นจุดเริ่มต้นที่พวกเราตั้งชื่องาน ใส่รายละเอียดของ issue, ลง label และอ้างถึงผู้ที่เกี่ยวข้องกับงานให้เรียบร้อยครบถ้วนให้มากที่สุด
> Well Begun is Half Done. ~ Aristotle

### New branch
เมื่อได้ issue มาแล้วถัดมาก็จะเปิด branch ใหม่ไว้บน GitHub เพื่อความสะดวกเราจะตั้งให้ชื่อ branch เป็นเลข issue ไปเลย เช่น iss8 คือ branch ของงาน issue #8 แบบนี้เป็นต้น

### Tracking
สำหรับทีมที่จะ code ใน issue นี้ ได้เวลาไปกันที่ Codenvy ‣ workspace:
~~~bash
$ git fetch origin              # download objects and refs.
$ git branch -a                 # list all branches
$ git checkout -t origin/iss8   # create local&tracking branch: iss8
~~~
ที่ branch: `iss8` ทุกคนในทีมจะทำงานร่วมเหมือนอยู่บนเครื่องเดียวกันผ่านทาง workspace นี้ ในส่วนการพูดคุยงานกับผู้ที่เกี่ยวข้องและผู้ที่ให้กำลังใจ ในทุกเรื่องให้ไป comment กันไว้ที่ issue #8 บน GitHub เพราะทุกๆ คนจะได้ track ตามไปพร้อมๆ กันได้จากที่เดียว

*เพิ่มเติม:* ถ้าเวลา git checkout แล้วมี error อย่างเช่น
~~~bash
The following untracked working tree files would be overwritten by checkout:
_site/CODE_OF_CONDUCT.md
_site/CONTRIBUTING.md
_site/ISSUE_TEMPLATE.md
_site/PULL_REQUEST_TEMPLATE.md
_site/assets/img/authors/x/x_128x128.jpg
Please move or remove them before you can switch branches.
Aborting
~~~
ให้ใช้ 2 คำสั่งนี้ก่อนที่จะสั่ง git checkout
~~~bash
$git clean -dn
$git clean -df
~~~
### Merge
ระหว่างทำงานทีมจะ commit และ push งานกลับมาตามจังหวะที่เหมาะสม:
~~~bash
git push -u origin iss8
~~~
ตอนที่ push งานกลับมา ส่วนของ GitHub จะเตรียมพร้อมทำ pull request ไว้ให้ด้วยเลย เราควรที่จะอ้าง pull request และ issue เข้าด้วยกัน เพราะตอน merge และปิด pull request จะได้ปิด issue ไปพร้อมกันเลยทีเดียว นั่นคือเมื่อถึงเวลาที่ทำงานเสร็จ มีการรันเทส และตรวจสอบทุกอย่างเรียบร้อยก็จะ merge เอา branch: `iss8` นี้ไปรวมกับ `master` และปิด issue #8 จบงานไปประมาณนี้

ซึ่งลำดับขั้นตอนการทำงานที่ตกลงกันนี้ก็เพื่อให้ในทีมได้เข้าใจตรงกัน อัพเดทงาน, ทำงานไปพร้อมๆ กันอย่างยิ้มได้สบายๆ ‣ คราวนี้ถ้าจะเป็นการมีส่วนร่วมจากผู้ใช้ภายนอกทั่วไป (ไม่สามารถ read/write มาที่ repository ได้) สำหรับการเปิด issue (หรือตาม track ความเคลื่อนไหวต่างๆ) ตรงนี้สามารถทำได้เป็นปกติเพราะว่า repository จะตั้งค่าเป็น public ไว้ให้อยู่แล้ว หลังจากมี issue เข้ามาพวกเราที่ดูแล repository ก็จะมาเปิด branch และทำตามขั้นตอนที่ว่ามาวนกันไป

*เพิ่มเติม:* การอ้างถึง issue ที่เกี่ยวข้องแล้วให้ระบบทำการปิด issue ให้ด้วยเวลาที่มีการ merge branch เรียบร้อย ให้ใส่ keyword สักอันจากข้างล่างนี้ใน รายละเอียดของ pull request หรือ commit message ของการ merge:
`close`, `closes`, `closed`, `fix`, `fixes`, `fixed`, `resolve`, `resolves`, `resolved` - อย่างเช่นใส่ว่า "งานเรียบร้อยแล้ว! close #iss8"
### Pull request
เรื่องสำคัญที่ห้อยอยู่ตอนท้าย สำหรับ contributor ‣ เพื่อนๆ สามารถ fork งานแล้วไปเพิ่มเติมโน่นนี่นั่นเสร็จแล้วส่ง pull request กลับมาที่พวกเราได้ ด้วยความยินดีและขอขอบคุณในการมีส่วนร่วมของทุกๆ คน หวังว่า workflow แบบนี้น่าจะช่วยให้ทุกๆ คนทำงานกันได้อย่างมีความสุขมากยิ่งขึ้น

> Coming Together is a Beginning; Keeping Together is Progress; Working Together is Success. ~ Henry Ford
