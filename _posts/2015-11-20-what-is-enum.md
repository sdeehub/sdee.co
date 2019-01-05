---
author: x
layout: post
title: "การใช้ Enum ในการเขียนโปรแกรมด้วย C#"
date: 2015-11-20 15:17:47 +0700
categories: [developer]
tags: [c#, x]
description: >
  e·nu·mer·a·tion /əˌn(y)o͞oməˈrāSH(ə)n/ ‣ noun: the action of mentioning a number of things one by one.
---
**Enumeration** จะเป็นการสร้างตัวแปรให้อยู่กันเป็นชุด เป็นกลุ่ม หรือประเภทเดียวกัน  ซึ่งกลุ่มของตัวแปรที่เราสร้างขึ้นมักจะมีตัวเลขกำกับอยู่ด้วยเสมอ โดยใช้คำสั่ง enum ดังนี้:

~~~csharp
public enum Days : int
{
    Sun,
    Mon,
    Tue,
    Wed,
    Thu,
    Fri,
    Sat
}
~~~
จากตัวอย่าง enum นี้มีชื่อว่า Days และมีสมาชิกที่เป็น integer อยู่ 7 ตัว โดยสมาชิกต่างๆ ของ enum นี้เราไม่ได้กำหนดค่าให้มัน จึงมีค่าเริ่มต้นเป็น

`Sun = 0, Mon = 1, Tue = 2` ไปจนถึง `Sat = 6` ตามลำดับ

แต่ถ้าเราต้องการกำหนดค่าเป็นอย่างอื่นก็ให้ใส่ค่าตามตัวอย่าง คือ
~~~csharp
public enum Days
{
    Sun = 7,
    Mon = 1,
    Tue = 2,
    Wed = 3,
    Thu = 4,
    Fri = 5,
    Sat = 6
}
~~~
สำหรับการนำค่า Enum ไปใช้งานนั้นก็ทำได้ดังนี้
~~~csharp
public class EnumTest
{
    enum Days { Sun, Mon, Tue, Wed, Thu, Fri, Sat };

    static void Main()
    {
        int x = (int)Days.Sun;
        int y = (int)Days.Fri;
        Console.WriteLine("Sun = {0}", x);
        Console.WriteLine("Fri = {0}", y);
    }
}
~~~
Output ที่ได้คือ
~~~bash
Sun = 0
Fri = 5
~~~
*ข้อดีของการใช้ Enum ก็คือ:* ทำให้การอ่าน code ทำได้ง่ายขึ้น ในบางกรณีการใช้ตัวแปร enum แทนการใช้ array ก็อาจเพิ่มประสิทธิภาพให้กับ Software ได้
