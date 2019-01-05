---
author: reallife
layout: post
title: "Yii2 กับ Heroku + ClearDB"
date: 2018-07-04 16:46:00 +0700
description: >
    สำหรับวันนี้เราจะมาดูภาคต่อของ Yii2 หลังจากที่ได้เอาขึ้นไปอยู่บน Heroku แล้ว (อ่านตอน [Yii2 กับ Heroku](https://www.sdee.co/developer/2018/04/07/yii2-deploy-to-heroku/) ได้ที่นี่) ‣ มาดูกันว่าเราจะต้องทำยังไงให้ Yii2 ของเราสามารถใช้งานร่วมกับ ClearDB ที่มีให้บน Heroku ได้ (แทนการใช้ MySQL และ phpMyAdmin บน localhost)
categories: [developer]
tags: [yii2, sdeesreallife]
comments: true
---
![ClearDB](/assets/img/authors/reallife/2018-07-04/cleardb_owler_20170322_143747_original.jpg)

ขั้นแรกเราจะติดตั้ง ClearDB ที่เป็น Add-ons ให้กับ Heroku App ของเราซะก่อน โดยจะใช้คำสั่งจากเครื่อง local คือ:
```
$ cd /var/www/hello
$ heroku addons:create cleardb:ignite
```
![ClearDB Plans & Pricing](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_500/v1530863429/Screenshot_from_2018-07-06_14-45-21.png)
เมื่อเราได้ทำการเพิ่ม ClearDB เข้าไปแล้ว ให้ใช้คำสั่ง
```
$ heroku config | grep CLEARDB_DATABASE_URL
CLEARDB_DATABASE_URL: mysql://b10f05d5ef83b2:a0c30bf2@us-cdbr-iron-east-04.cleardb.net/heroku_5be7befd94c8849?reconnect=true
```
หรือจากบนหน้าเว็บ Heroku App ของเรา โดยไปที่ `Settings` ‣ `Reveal Config Vars` เพื่อเอาค่าของ `CLEARDB_DATABASE_URL` มาใช้ จากตัวอย่างผลลัพธ์ของค่า CLEARDB_DATABASE_URL ตามข้างบนนี้ เราจะเอาไปแก้ไขไฟล์ `config/db.php` ซึ่งปกติจะเป็นการตั้งค่าเพื่อใช้งานร่วมกับ MySQL บน localhost
```
<?php

return [
    'class' => 'yii\db\Connection',
    'dsn' => 'mysql:host=localhost;dbname=yii2basic',
    'username' => 'root',
    'password' => '',
    'charset' => 'utf8',
```
ให้เปลี่ยนมาเป็น
```
<?php

return [
    'class' => 'yii\db\Connection',
    'dsn' => 'mysql:host=us-cdbr-iron-east-04.cleardb.net;dbname=heroku_5be7befd94c8849',
    'username' => 'b10f05d5ef83b2',
    'password' => 'a0c30bf2',
    'charset' => 'utf8',
```
นั่นคือค่าของ:
- `host` จะเริ่มจากหลัง `@` ไปจนถึง `/`
- `dbname` จะเริ่มจากหลัง `/` ไปจนถึง `?`
- `username` จะเริ่มจากหลัง `mysql://` ไปจนถึง `:` และ
- `password` จะเริ่มจากหลัง `:` ไปจนถึง `@`

จากนั้นเราจะสั่งคำสั่ง `migrate/create` และ `migrate/up` ที่เครื่อง localhost แต่จะเป็นการไปจัดการสร้าง DB ที่ตัว ClearDB ตามค่าที่เรากำหนดไว้ในไฟล์ `config/db.php` นั่นเอง

```
$ ./yii migrate/create create_post_table --fields="title:string,body:text"
Yii Migration Tool (based on Yii v2.0.15.1)

Create new migration '/var/www/hello/migrations/m180706_094307_create_post_table.php'? (yes|no) [no]:yes
New migration created successfully.

$ ./yii migrate/up
Yii Migration Tool (based on Yii v2.0.15.1)

Total 1 new migration to be applied:
	m180706_094307_create_post_table

Apply the above migration? (yes|no) [no]:yes
*** applying m180706_094307_create_post_table
    > create table post ... done (time: 0.286s)
*** applied m180706_094307_create_post_table (time: 1.715s)


1 migration was applied.

Migrated up successfully.
```
หลังจากที่ได้ Table มาแล้วคราวนี้ก่อนที่เราจะเรียก Gii ที่ localhost ให้แก้ไขไฟล์ `web/index.php` เพื่อให้ค่า environment กลับไปเป็น mode ของการ dev. ซะก่อน ตามนี้

```
<?php

// comment out the following two lines when deployed to production
defined('YII_DEBUG') or define('YII_DEBUG', true);
defined('YII_ENV') or define('YII_ENV', 'dev');

require __DIR__ . '/../vendor/autoload.php';
require __DIR__ . '/../vendor/yiisoft/yii2/Yii.php';

$config = require __DIR__ . '/../config/web.php';

(new yii\web\Application($config))->run();
```

เมื่อเราเรียก Gii ให้สร้าง code ต่างๆ ให้เสร็จ บวกกับเราพัฒนา code ต่อไปจนทุกอย่างเรียบร้อยแล้ว เราก็พร้อมที่จะกลับไปสู่ mode ที่เป็น production ด้วยการใส่ comment คืนที่ 2 บรรทัดนี้:
```
// defined('YII_DEBUG') or define('YII_DEBUG', true);
// defined('YII_ENV') or define('YII_ENV', 'dev');
```
แล้วก็ทำการ commit และ push ขึ้น Heroku - เวลาเพิ่มค่าลงใน DB *สังเกตว่า auto_increment ของ ClearDB ในตัวอย่างคือค่า ID* จะเพิ่มทีละ 10? ซึ่งสามารถดูคำอธิบายเพิ่มเติมได้จากที่นี่ [ClearDB FAQ](http://w2.cleardb.net/faqs/#general_16)

![Yii2 on Heroku](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_500/v1530872407/Screenshot_from_2018-07-06_17-18-09.png)

สำหรับ interface ในส่วนของการจัดการ DB เราจะใช้ Add-ons ที่ชื่อ Adminium มาใช้แทน phpMyAdmin ที่เราเคยติดตั้งและใช้งานกันอยู่บน localhost - ซึ่ง Adminium นี้จะสามารถติดตั้งผ่านทางหน้าเว็บ Heroku App ของเราก็ได้ หรือจะด้วยคำสั่งนี้:

```
$ heroku addons:create adminium
```

![Adminium DB Management](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_500/v1530873200/Screenshot_from_2018-07-06_17-31-28.png)

ทั้งหมดนี้ก็จะทำให้ Yii2 ของเราไปรันอยู่บน Heroku พร้อมกับ ClearDB ได้อย่างเรียบร้อย สบายใจไปทั่วหน้ากัน ‣ ขอให้มีความสุขกับการพัฒนาเว็บแอพด้วย Yii2 กับ Heroku + ClearDB นะครับทุกๆ คน
