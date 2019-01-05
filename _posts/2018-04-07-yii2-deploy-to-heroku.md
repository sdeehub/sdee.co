---
author: reallife
layout: post
title: "Yii2 กับ Heroku"
date: 2018-04-07 20:52:00 +0700
description: >
    หลังจากที่เราได้เคยทำการติดตั้ง Yii2 แบบใช้งานบนเครื่อง Local กันไปแล้วกับในตอนที่ชื่อว่า: [การติดตั้ง LAMP และ Yii2](https://www.sdee.co/developer/2018/03/01/install-lamp-and-yii2/) ‣ วันนี้เราจะมาดูขั้นตอนที่จะเอา Yii2 ไปไว้บน Heroku ด้วยกัน
categories: [developer]
tags: [yii2, sdeesreallife]
comments: true
---
![Deploy to Heroku Logo](/assets/img/authors/reallife/2018-04-07/Deploy-to-heroku-logo.png)

เหตุผลที่เราจะใช้งาน Yii2 กับ Heroku ก็เพราะ เราไม่มี Server เป็นของตัวเอง (555) และเมื่อเรามีความจำเป็นที่จะต้องใช้ Server ที่สามารถ Access ได้จาก Internet ทั่วๆ ไป เราก็ต้องหาผู้ให้บริการ และเผอิญว่า Heroku มีบริการ PaaS ที่รองรับ Java, Node.js, Scala, Clojure, Python, PHP และ Go แบบที่มี Plan ให้ใช้งานได้ฟรี (1) และ สะดวกสำหรับการ Deploy PHP (2) ทั้ง 2 ข้อนี้รวมกันนั่นทำให้เราต้องเข้าไป [Sign Up กับ Heroku ในทันที](https://signup.heroku.com/)
#### Sign Up และ Git
เมื่อได้ Account มาเรียบร้อยแล้ว หันมาที่เครื่อง Local (Ubuntu) เปิด Terminal แล้วติดตั้ง Heroku CLI ให้เรียบร้อยด้วยคำสั่ง

```
$ sudo snap install heroku --classic
```
จากนั้นทำการสร้าง Heroku App
```
$ cd /var/www/hello
$ git init
$ heroku create
Creating app... !
 ▸    Invalid credentials provided.
Enter your Heroku credentials:
Email: odd.daboss@sdee.co
Password: ***********
Creating app... done, ⬢ guarded-bastion-40430
https://guarded-bastion-40430.herokuapp.com/ | https://git.heroku.com/guarded-bastion-40430.git
```
ใส่ Email และ Password ที่เราใช้ตอนที่ทำการ Sign Up เสร็จแล้วจะได้ Heroku App มา 1 ตัว ในตัวอย่างนี้คือ `guarded-bastion-40430` (สำหรับ Free Plan ในขั้นแรกจะให้เราสามารถสร้าง App ได้สูงสุด 5 ตัว - [อ่านรายละเอียดเพิ่มเติมที่นี่](https://www.heroku.com/free))

เมื่อได้ App มาแล้ว เราก็จะได้ Git มาด้วยเช่นกัน (ตรวจสอบด้วยคำสั่ง `git remote -v` หรือถ้าต้องจัดการเพิ่มเอาเองก็จัดการเพิ่ม Remote ซะให้เรียบร้อย)
```
$ git remote -v
heroku	https://git.heroku.com/guarded-bastion-40430.git (fetch)
heroku	https://git.heroku.com/guarded-bastion-40430.git (push)
```
#### Procfile สำหรับ Apache2 บน Heroku
สร้าง Procfile ที่มีบรรทัดนี้ `web: vendor/bin/heroku-php-apache2 web/` ไว้ที่ `/var/www/hello` ของเราด้วยคำสั่ง
```
$ cat > Procfile
web: vendor/bin/heroku-php-apache2 web/
<Ctrl-d>
```
ที่ Heroku เราจะใช้ไฟล์นี้เพื่อบอกให้ Root Directory ไปอยู่ที่ `web`
#### แก้ไข composer.json
ใน `composer.json` ให้เพิ่มในส่วนของ `require` ด้วย 2 รายการนี้:
```
"fxp/composer-asset-plugin": "*",
"ext-gd": "*"
```
`fxp/composer-asset-plugin` อันนี้ต้องใช้แต่โดยปกติเราจะลงเป็น Global ไว้ก็เลยเอามาเพิ่มไว้ในนี้ด้วย ถัดมา `ext-gd` คือ สิ่งที่เราต้องใช้เพื่อแสดง Captcha ในหน้า Contact - เสร็จแล้วให้สั่ง `composer update` ด้วย
#### แก้ไข web/index.php
ตามค่า Default แล้ว Heroku จะ Deploy เป็น Production ซึ่งถ้าเราจะใช้ Yii2 สำหรับ Deploy Production ให้เรา Comment 2 บรรทัดตามที่บอกอยู่ใน `web/index.php` ออกไป
```
<?php

// comment out the following two lines when deployed to production
// defined('YII_DEBUG') or define('YII_DEBUG', true); --->>> Comment!
// defined('YII_ENV') or define('YII_ENV', 'dev'); ------>>> Comment!

require __DIR__ . '/../vendor/autoload.php';
require __DIR__ . '/../vendor/yiisoft/yii2/Yii.php';

$config = require __DIR__ . '/../config/web.php';

(new yii\web\Application($config))->run();
```
#### Pretty URLs
สร้างไฟล์ `web/.htaccess` ตามนี้
```
RewriteEngine on
# If a directory or a file exists, use it directly
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
# Otherwise forward it to index.php
RewriteRule . index.php
```
#### Push & Deploy
```
$ git add .
$ git commit -m "first commit to heroku"
$ git push heroku master
Counting objects: 96, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (77/77), done.
Writing objects: 100% (96/96), 42.80 KiB | 2.04 MiB/s, done.
Total 96 (delta 3), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote:
remote: -----> PHP app detected
remote: -----> Bootstrapping...
.
.
.
remote: Verifying deploy... done.
To https://git.heroku.com/guarded-bastion-40430.git
 * [new branch]      master -> master
```
ทุกครั้งที่เรา Push ขึ้นไป Heroku จะทำการ Build และ Deploy ให้เราทุกครั้งโดยอัตโนมัติ และถ้าทุกอย่างเรียบร้อยเราก็เข้าไปดูผลลัพธ์ที่หน้าเว็บได้เลย จะเข้าจาก URL (ในตัวอย่างนี้คือ https://guarded-bastion-40430.herokuapp.com/) หรือจะ Login เข้า Heroku คลิกที่ App ตัวที่เราใช้ แล้วเลือก `Open app` ที่มุมบนด้านขวาของหน้าเว็บก็ได้เช่นกัน - ขอให้สนุกกับ Yii2 และ Heroku นะครับ!
