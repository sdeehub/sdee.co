---
author: reallife
layout: post
title: "grep, find และ jpegoptim"
date: 2018-04-16 08:55:00 +0700
description: >
    วันนี้มี 3 คำสั่งมาฝากจาก Ubuntu หรือ Unix (ที่ไม่ใช่ `ls` และ `sudo`) ‣ ลองมาดูกันว่า 3 คำสั่งนี้ คือ `grep`, `find` และ `jpegoptim` น่าจะช่วยให้ชีวิตพวกเราง่ายขึ้น เวลาที่เราต้องตามค้นหาและแก้ไขอะไรบางอย่าง
categories: [developer]
tags: [ubuntu, sdeesreallife]
comments: true
---
![Ubuntu Logo](/assets/img/authors/reallife/2018-04-16/Logo-ubuntu.png)

### grep
g/re/p - (*g*)lobally search a (*r*)egular (*e*)xpression and (*p*)rint เป็น command-line หรือคำสั่งที่ใช้สำหรับค้นหา คำเหมือน ที่มีอยู่ใน plain-text ต่างๆ ตามรูปแบบที่กำหนด ตัวอย่างที่เกิดขึ้นและบ่อยมากของการใช้งาน เช่น ต้องการหาคำอะไรสักคำที่มีอยู่ในทุกๆ ไฟล์ ซึ่งเป็น text file นั่นคือ source code หรือ markdown ประมาณนี้ ที่อยู่ใน folder และ subfolder ที่ต้องการ - ดูรูปแบบและตัวอย่างการใช้กันครับ:

- รูปแบบ คือ `grep -rnw '/path/to/search/' -e 'pattern'`
- ตัวอย่าง คือ ต้องการหาคำว่า `author: odd` ที่มีในทุกไฟล์ ใน folder จากตรงนี้ไปทั้งหมด

```
$ grep -rnw '.' -e 'author: odd'
./_posts/2014-12-07-meetup-party.md:2:author: odd
./_posts/2018-04-04-the-nights-to-remember.md:2:author: odd
./_posts/2018-01-10-install-google-chrome-ubuntu-1710.md:2:author: odd
./_posts/2017-11-28-dont-know-what-you-got.md:2:author: odd
./_posts/2015-02-14-peace-treaty.md:2:author: odd
./_posts/2016-10-02-hello-google-allo.md:2:author: odd
./_posts/2018-03-08-big-days-of-2018.md:2:author: odd
./_posts/2017-03-05-what-are-you-up-to.md:2:author: odd
./_posts/2018-04-14-while-we-were-waiting.md:2:author: odd
./_posts/2018-01-24-buddhist-holy-days-2018.md:2:author: odd
./_posts/2018-01-18-katyayana.md:2:author: odd
./_posts/2016-10-09-why-you-should-like-firefox.md:2:author: odd
./_posts/2016-09-25-wifi-setup-with-net-analyzer.md:2:author: odd
./_posts/2016-05-29-tipitaka-buddist-pray.md:2:author: odd
./_posts/2016-04-21-pray-for-forgiveness.md:2:author: odd
./_posts/2014-12-06-thankful-and-grateful.md:2:author: odd
$
```
ถ้าเจอ - จะบอกชื่อไฟล์และบรรทัดที่เจอในไฟล์นั้นๆ ‣ และถ้าไม่เจอก็คือไม่เจอ ก็จะไม่มีผลลัพธ์อะไรขึ้นให้นะครับ (ตามตัวอย่างข้างล่าง) สำหรับข้อมูลเพิ่มเติมหาได้ทั่วไปหรือจะอ่านเพิ่มเติมจากใน [Stack Overflow นี้ก็ได้ครับ](https://stackoverflow.com/questions/16956810/how-do-i-find-all-files-containing-specific-text-on-linux)
```
$ grep -rnw '.' -e 'author: james'
$
```
### find
ถัดมาเป็นคำสั่ง `find` คือเอาไว้หาไฟล์ที่มีชื่อตามที่เราต้องการค้นหา (ไม่ได้จะเข้าไปค้นเนื้อหาข้างในไฟล์อย่างกับ `grep`) รูปแบบการใช้งานง่ายๆ คือ `find . -name "file pattern"` เช่น `find . -name *.svg` คือหาไฟล์ทุกไฟล์ที่มีนามสกุล `.svg` ใน folder จากตรงนี้ไปทั้งหมด
```
$ find . -name *.svg
./_site/assets/icomoon/fonts/icomoon.svg
./_site/assets/icons/safari-pinned-tab.svg
./assets/icomoon/fonts/icomoon.svg
./assets/icons/safari-pinned-tab.svg
$
```
มีเนื้อหาให้อ่านเพิ่มเติมได้ทั่วไปเช่นกันนะครับ เพราะเป็น command-line ปกติ หรือจะอ่านจากที่นี่ [Indiana University: Knowledge Base](https://kb.iu.edu/d/admm) อธิบายได้ละเอียดดีครับ
### jpegoptim
สำหรับคำสั่งที่ 3 นี่ไม่ใช่คำสั่งที่มีมาให้กับ Unix หรือ Ubuntu ต้องติดตั้งเพิ่ม แต่มีประโยชน์มากใช้สำหรับการลดขนาดไฟล์รูปภาพ JPEG

การติดตั้งใช้คำสั่ง `sudo apt install jpegoptim` และการใช้งานง่ายๆ คือ `jpegoptim --size=512k *.jpg` ความหมายคือบอก `jpegoptim` ให้พยายามลดขนาดไฟล์ที่มีนามสกุล `jpg` ให้ได้ 512k - สั่งห้วนๆ แบบนี้ถ้าไฟล์ไหนที่ลดขนาดได้ไฟล์จะถูก overwrite กลายเป็นขนาดเล็กลงไปเลยนะครับ

ถ้าต้องการให้เอาผลลัพธ์ที่ได้ไปไว้อีกที่ให้สร้าง folder ขึ้นมาก่อนแล้วสั่งเพิ่มลงไปแบบนี้ `jpegoptim --size=512k *.jpg --dest=resize` คือจะลดขนาดแล้วสร้างไฟล์ใหม่ไว้ให้ที่ folder ที่เราสร้างไว้ชื่อ `resize` แบบนี้ไฟล์เดิมก็ยังอยู่ที่เดิมและจะยังมีขนาดเท่าเดิมอยู่นะครับ ส่วนไฟล์ไหนที่ลดขนาดไม่ได้ `jpegoptim` ก็จะข้ามไปไม่มีผลอะไรเกิดขึ้นครับ
```
$ ls -la *.jpg
-rw-rw-r-- 1 odd odd 3117529 Apr 16 09:55 anete-lusina-609852-unsplash.jpg
-rw-rw-r-- 1 odd odd 5406296 Apr 16 09:55 brooke-cagle-609883-unsplash.jpg
-rw-rw-r-- 1 odd odd  879189 Apr 16 09:55 felix-russell-saw-609920-unsplash.jpg
-rw-rw-r-- 1 odd odd 1079051 Apr 16 09:55 felix-russell-saw-609923-unsplash.jpg
$
```
ดูตัวอย่างและผลลัพธ์ขนาดของไฟล์เปรียบเทียบตามขัอมูล ข้างบน/ข้างล่าง นี้ครับ ส่วนคุณภาพของรูปภาพก็จะต้องลดไปด้วยเพราะเอาตามขนาดไฟล์ที่เราสั่งให้ลดเป็นที่ตั้ง ส่วนในหลายๆ ครั้งถ้าเราต้องการลดขนาดไฟล์แต่ไม่ต้องการลดคุณภาพของรูป ให้ใช้คำสั่งห้วนๆ สั้นๆ กว่าที่สั่งมานั้นลงไปอีกครับ คือ `jpegoptim *.jpg` สั่งแบบนี้คือไม่ระบุขนาดจะปล่อยให้ `jpegoptim` พยายามอย่างสุดความสามารถซึ่งจะลดขนาดไฟล์ในแบบ lossless ให้ครับ นั่นคือลดให้ได้มากที่สุดโดยที่จะไม่ให้เสียคุณภาพของรูปไป - รายละเอียดเพิ่มเติม search หา `jpegoptim` ก็จะหาอ่านได้ทั่วๆ ไป หรืออ่านได้จาก [Peter Dave Hello's Blog](https://www.peterdavehello.org/2016/02/use-jpegoptim-to-optimizere-compress-your-jpg-images/)

*หมายเหตุ:* ในนั้นมีการพูดถึง [optipng และ link](https://www.peterdavehello.org/2015/05/use-optipng-to-optimize-re-compress-your-png-images-losslessly/) ไปเนื้อหาที่ Peter Dave เขียนไว้ด้วยครับ
```
$ jpegoptim --size=512k *.jpg --dest=resize
anete-lusina-609852-unsplash.jpg 4256x2832 24bit N ICC JFIF  [OK] 3117529 --> 524724 bytes (83.17%), optimized.
brooke-cagle-609883-unsplash.jpg 5472x3648 24bit N ICC JFIF  [OK] 5406296 --> 489363 bytes (90.95%), optimized.
felix-russell-saw-609920-unsplash.jpg 3000x2000 24bit N ICC JFIF  [OK] 879189 --> 82659 bytes (90.60%), optimized.
felix-russell-saw-609923-unsplash.jpg 3000x2000 24bit N ICC JFIF  [OK] 1079051 --> 131416 bytes (87.82%), optimized.
$ ls -la resize
total 1220
drwxr-xr-x 2 odd odd   4096 Apr 16 09:59 .
drwxr-xr-x 4 odd odd   4096 Apr 16 10:08 ..
-rw-rw-r-- 1 odd odd 524724 Apr 16 09:59 anete-lusina-609852-unsplash.jpg
-rw-rw-r-- 1 odd odd 489363 Apr 16 09:59 brooke-cagle-609883-unsplash.jpg
-rw-rw-r-- 1 odd odd  82659 Apr 16 09:59 felix-russell-saw-609920-unsplash.jpg
-rw-rw-r-- 1 odd odd 131416 Apr 16 09:59 felix-russell-saw-609923-unsplash.jpg
```
เรียบร้อยล่ะครับ 3 คำสั่งง่ายๆ ได้ประโยชน์ สำหรับเพิ่มความสะดวก รวดเร็วจากการเรียกใช้ในการช่วยทำงาน ถัดไปก็เป็นเวลากลับจากวันหยุดสงกรานต์ ขอให้พวกเราเดินทางกันอย่างปลอดภัย และมีชีวิตให้สมดุลย์ได้มีความสุขกับชีวิตส่วนตัว ครอบครัว และการทำงานไปพร้อมๆ กันทุกๆ คน ‣ แล้วพบกันใหม่ขอให้มีความสุขกับการพัฒนาโปรแกรมไว้ใช้นะครับพวกเรา บ๊ายบาย!
