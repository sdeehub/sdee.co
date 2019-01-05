---
author: reallife
layout: post
title: "ลง driver การ์ดจอ Nvidia บน Ubuntu 17.10"
date: 2018-02-20 15:25:15 +0700
description: >
    สำหรับใครที่ใช้การ์ดจอของ Nvidia และต้องการติดตั้ง driver สำหรับใช้งานบน Ubuntu เรามีวิธีการติดตั้งมาแนะนำเพื่อนๆ ตามนี้ครับ
categories: [developer]
tags: [ubuntu, sdeesreallife]
comments: true
---
เริ่มด้วยการเปิด terminal ขึ้นมาก่อนเป็นอันดับแรก ด้วยการกด ‣ `Ctrl` + `Alt` + `t`

จากนั้นตรวจสอบกันก่อนว่าตอนนี้บนเครื่องของเราใช้ driver VGA อะไรอยู่ โดยปกติทั่วไปแล้ว Ubuntu จะใช้ nouveau ซึ่งเป็น VGA driver ที่เป็น Open Source สำหรับการ์ดจอ nvidia ของเรา ‣ การตรวจดูตรงนี้ทำได้ด้วยคำสั่ง:

`lsmod | grep nouveau` จะได้ผลลัพธ์บนหน้าจอประมาณแบบนี้

```bash
ubuntu@Computer-All-Series:~$ lsmod | grep nouveau
nouveau              1638400  24
mxm_wmi                16384  1 nouveau
i2c_algo_bit           16384  1 nouveau
ttm                    94208  1 nouveau
drm_kms_helper        167936  1 nouveau
drm                   356352  26 nouveau,ttm,drm_kms_helper
wmi                    24576  4 asus_wmi,wmi_bmof,mxm_wmi,nouveau
video                  40960  2 asus_wmi,nouveau
```

หรือถ้าเราลองใช้คำสั่ง `lsmod | grep nvidia` จะไม่มีอะไรขึ้นมาเลยเพราะตอนนี้เครื่องยังไม่ได้ลงและเรียกใช้ driver ของ nvidia นั่นเอง แต่เราจะแน่ใจได้ยังไงว่าเราใช้การ์ดจอของ nvidia? ‣ ตรวจสอบง่ายๆ ด้วยคำสั่งนี้:

`lspci | grep VGA` จะได้ผลลัพธ์บนหน้าจอประมาณแบบนี้

```bash
ubuntu@Computer-All-Series:~$ lspci | grep VGA
01:00.0 VGA compatible controller: NVIDIA Corporation GT218 [GeForce 210] (rev a2)
```

จากตัวอย่างเครื่องเรามีการ์ดจอของ nvidia เสียบอยู่ อย่างที่เห็นคือ `GeForce 210` (รุ่นยอดนิยมจิ๋วแต่แจ๋วสบายกระเป๋า) พอรู้แล้วว่า Ubuntu ของเราเสียบ nvidia แต่ไม่ได้ใช้ driver ของ nvidia ถึงตรงนี้ให้หยุดคิดนิดนึง และถ้าตัดสินใจว่า **ทำการเปลี่ยนซะ!** (*ตั้งใจอ่านในวงเล็บนี้ซะหน่อย* - ถ้าใช้งานได้ดีเรียบร้อยอยู่แล้วไม่ต้องเปลี่ยนก็ได้ แต่หลายๆ ครั้งเราพบว่าการใช้ driver ของ nvidia เองจะรองรับอะไรได้ดีกว่า ที่เห็นได้ชัด เช่น การรองรับเวลาต่อจอหลายตัว) 

และถ้าตัดสินใจว่า **ทำการเปลี่ยนซะ!** ก็จะต้องมาจัดการเพิ่ม repository กันด้วยคำสั่งนี้:

`sudo add-apt-repository ppa:graphics-drivers` และตามด้วย:

`sudo apt update`

ให้ดูรายละเอียดของ driver ที่เราจะใช้ให้ตรงรุ่นกับการ์ดจอของเราจากที่นี่ [https://launchpad.net/~graphics-drivers/+archive/ubuntu/ppa](https://launchpad.net/~graphics-drivers/+archive/ubuntu/ppa) และที่นี่ [http://www.nvidia.com/Download/index.aspx?lang=th](http://www.nvidia.com/Download/index.aspx?lang=th)

เสร็จแล้วก็ใช้คำสั่งเพื่อติดตั้ง driver ที่ตรงรุ่นกับการ์ดจอของเรา อย่างในตัวอย่างนี้คือใช้ nvidia-340 ซึ่งจะรองรับการ์ดจอหลายๆ รุ่น และ หลายๆ ซีรี่ส์ที่มี `GeForce 210` ของเรารวมอยู่ด้วย คำสั่งที่ใช้ในการติดตั้ง driver ก็คือ:

`sudo apt install nvidia-340` เสร็จแล้วก็ reboot เครื่อง และใช้คำสั่งนี้ดูอีกที:

`lsmod | grep nvidia` จะได้ผลลัพธ์บนหน้าจอประมาณแบบนี้

```bash
ubuntu@Computer-All-Series:~$ lsmod | grep nvidia
nvidia_uvm             36864  0
nvidia              10559488  86 nvidia_uvm
drm                   356352  6 nvidia
```

นั่นคือตอนนี้ Ubuntu ของเราที่เสียบการ์ดจอ nvidia ก็จะเรียกใช้ driver ของ nvidia ไปเป็นที่เรียบร้อย และที่สำคัญด้วยการติดตั้งผ่าน ppa และ apt install ต่อไปเวลามีอัพเดทอะไรที่เกี่ยวกับ driver นี้ ระบบก็จะคอยอัพเดทให้เราด้วยเลย ‣ สำหรับเพื่อนๆ ที่มีประสบการณ์การใช้งาน ความคิดเห็น หรือคำแนะนำอะไรดีๆ เข้ามาแบ่งปันและ comment กันไว้ได้นะครับ
