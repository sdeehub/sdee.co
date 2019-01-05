---
author: reallife
layout: post
title: "การติดตั้ง LAMP และ Yii2"
date: 2018-03-01 22:40:00 +0700
description: >
      เนื้อเรื่องในตอนนี้คือบันทึกช่วยจำเอาไว้สำหรับทำการติดตั้ง LAMP และ Yii2 แบบกระชับฉับไว ‣ ส่วนเนื้อหาแบบละเอียด มีการอธิบายที่ครอบคลุมเข้าใจง่ายสามารถอ่านได้จาก: [การติดตั้ง LAMP Stack - DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-16-04) และ [การเขียนโปรแกรมด้วย Yii2 - Jeff Reifman : envatotuts+](https://code.tutsplus.com/series/how-to-program-with-yii2--cms-725)
categories: [developer]
tags: [yii2, sdeesreallife]
comments: true
---
LAMP ในที่นี้เราหมายถึง Linux, Apache2, MySQL และ PHP ที่จะทำการติดตั้งบน OS Ubuntu 17.10 และ Yii2 ในที่นี้เราหมายถึง Basic Project Template

#### เริ่มจากติดตั้ง Apache2:
```
$ sudo apt update
$ sudo apt install apache2
```

*ตรวจสอบการติดตั้ง:*
ถ้าเราเปิด browser แล้วเรียก localhost ก็จะพบกับความพร้อมของ Apache2 ในทันที

```
$ which apache2
$ apache2 -v
```

#### ติดตั้ง MySQL Server:
```
$ sudo apt install mysql-server
```

*ตรวจสอบการติดตั้ง:*
```
$ mysql --version
```
เพิ่มความปลอดภัยสำหรับการติดตั้ง ‣ ดูรายละเอียดได้ที่ [dev.mysql.com](https://dev.mysql.com/doc/refman/5.7/en/mysql-secure-installation.html)
```
$ sudo mysql_secure_installation
```

```
Would you like to setup VALIDATE PASSWORD plugin? - Y
There are three levels of password validation policy: - เลือกเป็น level 1 หรือ 2 แล้วใช้ password ที่ซับซ้อนตามระดับที่เลือก
Remove anonymous users? - Y
Disallow root login remotely? - Y
Remove test database and access to it? - Y
Reload privilege tables now? - Y
```

#### ติดตั้ง PHP:
```
$ sudo apt install php libapache2-mod-php php-mysql
```

   *ตรวจสอบการติดตั้ง:*
```
$ php -v
$ php -i
```
ตัวอย่างไฟล์ info.php
```php
<?php
phpinfo();
?>
```

#### ติดตั้ง phpMyAdmin:
```
$ sudo apt install phpmyadmin
```

```
Web server to reconfigure automatically: - [*] apache2
Configure database for phpmyadmin with dbconfig-common? - Yes
```
*ข้อสำคัญ:* กด `SPACE BAR` เพื่อเลือก Apache2 ด้วยนะครับ ต้องมีดอกจันอยู่ในตัวเลือกสีแดงนั้นด้วย - ลองใช้ `SPACE BAR` และ `TAB` ดูจะเข้าใจ แต่ถ้าต้องแก้ไขการเรียกใช้ก็ทำได้เองตามนี้:

*(พิเศษ)* แก้ไขการเรียกใช้ phpMyAdmin:
```
$ echo 'Include /etc/phpmyadmin/apache.conf' | sudo tee -a /etc/apache2/apache2.conf
$ sudo systemctl restart apache2.service
```

#### ติดตั้ง Composer
ในแบบ Global
```
$ cd ~
$ php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
$ php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
$ php composer-setup.php
$ php -r "unlink('composer-setup.php');"
$ sudo mv composer.phar /usr/local/bin/composer
```
#### ติดตั้ง Plugin:
```
$ composer global require "fxp/composer-asset-plugin:~1.3"
```

#### เปลี่ยนในส่วนของ /var/www
```
$ sudo chown -R www-data:www-data /var/www
$ sudo chmod -R 775 /var/www
$ sudo adduser $USER www-data
```
*ข้อสำคัญ:* `adduser` จะมีผลต้อง logout ก่อนแล้ว login กลับเข้ามาใหม่นะครับ

#### ติดตั้ง Yii2:
ใช้ Basic Template สร้างโปรเจคชื่อ hello

```
$ cd /var/www
$ composer create-project --prefer-dist yiisoft/yii2-app-basic hello
```

ปรับเปลี่ยน Apache
```
$ sudo nano /etc/apache2/sites-available/hello.conf
```

```html
<VirtualHost *:80>
 ServerName yourdomain.com
# Set document root to be "basic/web"
DocumentRoot "/var/www/hello/web"
<Directory "/var/www/hello/web">
    # use mod_rewrite for pretty URL support
    RewriteEngine on
    # If a directory or a file exists, use the request directly
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    # Otherwise forward the request to index.php
    RewriteRule . index.php
</Directory>
</VirtualHost>
```

```
$ sudo a2enmod rewrite
$ sudo a2ensite hello.conf
$ sudo a2dissite 000-default.conf
$ sudo systemctl reload apache2
```

*(พิเศษ)* ใช้ Pretty URL : ที่ไฟล์ hello/config/web.php ให้เอา comment ในส่วนนี้ออก
```
'urlManager' => [
    'enablePrettyUrl' => true,
    'showScriptName' => false,
    'rules' => [
    ],
],
```
จากขั้นตอนที่ว่ามานี่ก็จะทำให้เราพร้อมที่จะไปต่อกันกับ Yii2 แล้วนะครับ ‣ ขอให้มีความสุขและสนุกกับการพัฒนาแอปและเขียนโค้ดนะครับทุกๆ คน
