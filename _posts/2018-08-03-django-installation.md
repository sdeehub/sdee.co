---
author: reallife
layout: post
title: "มาติดตั้ง Django บน Ubuntu 18.04 กัน"
date: 2018-08-03 18:28:00 +0700
description: >
    วันนี้เราจะมาดูวิธีการติดตั้ง Django - The web framework for perfectionists with deadlines บน Ubuntu 18.04 กันนะครับ
categories: [developer]
tags: [Web, sdeesreallife]
comments: true
---
พร้อมแล้ว `Ctrl + Alt + t` เปิด Terminal กันขึ้นมาได้เลย ใช้คำสั่งนี้ `python3 --version` และ `which python3` เพื่อตรวจดูการติดตั้ง Python3 บนเครื่องของเรา ซึ่งปกติจะมาพร้อมกับ Ubuntu 18.04 เป็นที่เรียบร้อยแล้ว

```
$ python3 --version
Python 3.6.5
$ which python3
/usr/bin/python3
```
ถัดมาเราก็จะทำ `python3` ให้เป็น default ของเรา ด้วยการ `nano ~./bashrc` แล้วเพิ่มบรรทัดนี้ลงที่ท้ายไฟล์ `alias python=python3` เสร็จแล้วก็ `Ctrl-x` เพื่อ Save ไฟล์ ‣ เสร็จแล้วก็สั่ง `Source` แล้วตรวจผลตามนี้:
```
$ source ~/.bashrc
$ python --version
Python 3.6.5
```
ต่อไปก็คือการติดตั้ง Pip ซึ่งก็คือตัวจัดการ Package ของ Python ด้วยคำสั่ง `sudo apt install python3-pip -y` เสร็จแล้วตรวจสอบและทำ link ตามข้างล่างนี้:
```
$ sudo apt install python3-pip -y
$ which pip3
/usr/bin/pip3
$ sudo ln -s /usr/bin/pip3 /usr/bin/pip
$ pip --version
pip 9.0.1 from /usr/lib/python3/dist-packages (python 3.6)
```
ถัดมาก็คือการติดตั้ง Virtualenv ซึ่งก็คือตัวสร้างสภาพแวดล้อม หรือ Python Environment Builder นั่นเอง (ข้อมูลเพิ่มเติมลองอ่านจากที่นี่ดูครับ - [Real Python](https://realpython.com/python-virtual-environments-a-primer/)) การติดตั้งก็ด้วยคำสั่ง `sudo apt install virtualenv` ‣  มาถึงตรงนี้ก็ถือว่าเครื่องมือของพวกเราได้ถูกติดตั้งครบเรียบร้อยล่ะ มาลงมือสร้าง Environment สำหรับ Python และ Django กัน

ในตัวอย่างนี้จะสร้าง Path ไว้ก่อนแบบนี้ `~/.virtualenvs` แล้วสร้าง Environment ด้วยคำสั่ง `virtualenv --python=python3 proj-01`
```
~$ mkdir ./.virtualenvs
$ cd ./.virtualenvs
~/.virtualenvs$ virtualenv --python=python3 proj-01
Running virtualenv with interpreter /usr/bin/python3
Using base prefix '/usr'
New python executable in /home/odd/.virtualenvs/proj-01/bin/python3
Also creating executable in /home/odd/.virtualenvs/proj-01/bin/python
Installing setuptools, pip, wheel...done.
~/.virtualenvs$
```
ถ้าเข้าไปดูที่ `proj-01` ก็จะเห็น folders ต่างๆ ที่ถูกสร้างขึ้นมา ให้เรารัน `source ./bin/activate` แบบนี้
```
~/.virtualenvs/proj-01$ source ./bin/activate
(proj-01)~/.virtualenvs/proj-01$
```
จะเห็นว่า Prompt จะเปลี่ยนไปเพื่อบอกว่าตอนนี้เราอยู่ใน Environment ของ `proj-01` นั่นเอง (ส่วนถ้าจะออกจาก Environment นี้ก็ใช้คำสั่ง `deactivate`)

เอาล่ะพอมาอยู่ใน Environment ที่สร้างมาพร้อมแล้วคราวนี้ก็มาลง Django กัน ด้วยการใช้คำสั่ง `pip install django` และตามด้วยคำสั่งให้สร้าง Project ชื่อ project01 ‣ `django-admin startproject project01`
```
~/.virtualenvs/proj-01$ pip install django
~/.virtualenvs/proj-01$ django-admin startproject project01
~/.virtualenvs/proj-01$ ls -la
total 28
drwxr-xr-x 6 odd odd 4096 Aug  8 18:03 .
drwxr-xr-x 4 odd odd 4096 Aug  8 17:45 ..
drwxr-xr-x 2 odd odd 4096 Aug  8 17:45 bin
drwxr-xr-x 2 odd odd 4096 Aug  8 17:45 include
drwxr-xr-x 3 odd odd 4096 Aug  8 17:45 lib
-rw-r--r-- 1 odd odd   59 Aug  8 17:45 pip-selfcheck.json
drwxr-xr-x 3 odd odd 4096 Aug  8 18:03 project01
~/.virtualenvs/proj-01$
```
มาถึงขั้นตอนใกล้จะสุดท้ายแล้ว ตอนนี้เราจะมาทำให้ Django ของเราถูกเรียกขึ้นมาได้จาก IP ของเรา ด้วยการเข้าไปเพิ่ม `ALLOWED_HOSTS` ในไฟล์ project01/settings.py นั่นเอง
```
~/.virtualenvs/proj-01$ cd project01
~/.virtualenvs/proj-01/project01$ nano project01/settings.py
```
ให้เพิ่ม IP ของเครื่องเราเข้าไป ในตัวอย่างนี้จะเป็น `ALLOWED_HOSTS = ['192.168.1.39']` - วิธีดู IP ใช้ ifconfig -a (ถ้ายังเรียกไม่ได้ให้ติดตั้ง net-tools ซะก่อน ด้วยคำสั่ง `sudo apt install net-tools`)

เรียบร้อยแล้วก็ทำการเรียก Server ขึ้นมาด้วยคำสั่งนี้ `python manage.py runserver 192.168.1.39:8000`
```
~/.virtualenvs/proj-01/project01$ python manage.py runserver 192.168.1.39:8000
Performing system checks...

System check identified no issues (0 silenced).

You have 15 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.

August 03, 2018 - 11:22:10
Django version 2.1, using settings 'project01.settings'
Starting development server at http://192.168.1.39:8000/
Quit the server with CONTROL-C.
```
เปิด Browser ไปที่ http://192.168.1.39:8000 ก็จะเจอกับ Django รออยู่
![django](https://res.cloudinary.com/sdees-reallife/image/upload/c_scale,e_shadow:40,w_600/v1533727467/Screenshot_from_2018-08-08_18-23-52.png)

ส่งท้ายอีกนิดนึงนะครับ ถ้าจะจบการทำงานก็ `Ctrl-c` และดูดีๆ นิดนึงจะมีเรื่อง Migration อยู่อีกหน่อย ก็คือตรงนี้หยุด Server ซะก่อนแล้วใช้คำสั่ง `python manage.py migrate` ทุกอย่างก็จะเรียบร้อยครับ
