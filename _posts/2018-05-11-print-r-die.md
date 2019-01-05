---
author: reallife
layout: post
title: "print_r(); die(); ทำแบบนี้ได้อ่านง่ายขึ้น"
date: 2018-05-11 15:30:00 +0700
description: >
    วันนี้มีคำแนะนำมาให้สำหรับมือใหม่ในการใช้ `print_r();` และ `die();` - ทำแบบนี้จะช่วยให้เราอ่านผลของการ `print_r();` ได้ง่ายขึ้น
categories: [developer]
tags: [yii2, sdeesreallife]
comments: true
---
ในการเขียน php ด้วยการใช้ Yii2 framework หรืออะไรก็ได้ที่เป็น php เรามักต้องใช้ประโยคเด็ดคู่นี้เสมอๆ นั่นคือ `print_r(); die();` เพื่อใช้ตรวจสอบค่าในโปรแกรมว่าถึงตรงนั้นแล้วค่าตัวแปรเป็นอะไร

และก็เกือบทุกครั้งที่ผลลัพธ์ที่เราต้องการดูซึ่งเป็น object, array หรือ json มันก็จะอ่านยากหน่อยๆ - มาดูวิธีช่วยง่ายๆ กัน:

* ใช้ <pre> เข้าช่วย

```php
<pre>
<?php
$a = array ('a' => 'apple', 'b' => 'banana', 'c' => array ('x', 'y', 'z'));
print_r ($a);
?>
</pre>
```

อันนี้เป็นตัวอย่างที่ยกมาให้ดูจาก php manual ที่ link นี้ครับ: [php.net/manual/en/function.print-r.php](http://php.net/manual/en/function.print-r.php) ‣ สำหรับผลลัพธ์ที่ได้จะเป็นแบบนี้

```php
<pre>
Array
(
    [a] => apple
    [b] => banana
    [c] => Array
        (
            [0] => x
            [1] => y
            [2] => z
        )
)
</pre>
```

หรือแบบนี้ `echo "<pre>"; print_r($model); echo "</pre>";` เพื่อ print ค่าของตัวแปร `$model` ให้อ่านได้ง่ายขึ้น

* ใช้ view source ที่ browser ช่วย

อีกวิธีนึงก็คือเวลา `print_r(); die();` อ่านไม่ค่อยออก ที่ browser ให้เปิด view source จะช่วยให้อ่านได้ง่ายขึ้น

Firefox: `Menu ‣ Web Developer ‣ Page Source` หรือกด `Ctrl-u`

Chrome: `Menu ‣ More tools ‣ Developer tools` หรือกด `Ctrl-Shift-i`

ตัวอย่างเช่นจากผลลัพธ์อะไรคล้ายๆ แบบนี้


```
app\models\RfqUploadedFiles Object ( [_attributes:yii\db\BaseActiveRecord:private] => Array (
[filename_2d] => Screenshot from 2018-04-14 21-59-33.png [filename_3d] => [filename_sample_part] =>
[filename_plating_spec_data] => [filename_other] => [file_md5_2d] => 0497de44eb30dbf.png
[rfq_summary_id] => 4 ) [_oldAttributes:yii\db\BaseActiveRecord:private] =>
[_related:yii\db\BaseActiveRecord:private] => Array ( )
[_relationsDependencies:yii\db\BaseActiveRecord:private] => Array ( )
[_errors:yii\base\Model:private] => Array ( [rfq_summary_id] => Array ( [0] => Rfq Summary ID "4"
has already been taken. ) )
```

จะกลายมาเป็นแบบนี้ บน Firefox ด้วยการกด `Ctrl-u`

```
app\models\RfqUploadedFiles Object
(
    [_attributes:yii\db\BaseActiveRecord:private] => Array
        (
            [filename_2d] => Screenshot from 2018-04-14 21-59-33.png
            [filename_3d] =>
            [filename_sample_part] =>
            [filename_plating_spec_data] =>
            [filename_other] =>
            [file_md5_2d] => 0497de44eb30dbf.png
            [rfq_summary_id] => 4
        )

    [_oldAttributes:yii\db\BaseActiveRecord:private] =>
    [_related:yii\db\BaseActiveRecord:private] => Array
        (
        )

    [_relationsDependencies:yii\db\BaseActiveRecord:private] => Array
        (
        )

    [_errors:yii\base\Model:private] => Array
        (
            [rfq_summary_id] => Array
                (
                    [0] => Rfq Summary ID "4" has already been taken.
                )

        )
```        

วันนี้มาแบบสั้นๆ ง่ายๆ ใช้งานได้อย่างมีประโยชน์ และช่วยให้การเขียน code สนุกและง่ายขึ้น - ขอให้ทุกคนมีความสุขกับการเขียน code กันนะครับ บ๊ายบาย
