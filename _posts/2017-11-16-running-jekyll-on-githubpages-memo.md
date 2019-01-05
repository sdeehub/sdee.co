---
author: reallife
layout: post
title: "บันทึกช่วยจำในการใช้ Jekyll ร่วมกับ GitHub Pages"
date: 2017-11-16 17:17:47 +0700
categories: [developer]
tags: [jekyll, github, sdeesreallife]
description: >
  เนื้อหาในตอนนี้เราจะไม่ได้พูดถึงการติดตั้ง Jekyll ใดๆ เลย หรือแม้แต่ที่มาที่ไปของการใช้งาน GitHub ถ้านั่นคือสิ่งที่คุณคิดว่าต้องทำความเข้าใจเพิ่มละก็ ขอให้ลองหาอ่านเรื่อง การติดตั้ง Jekyll, การใช้งาน GitHub และ GitHub Pages ซะก่อน นั่นน่าจะเป็นเรื่องที่ดีมาก :)
---
เอาล่ะเมื่อเราเข้าใจตรงกันตามนั้น ดูเหมือนว่าคุณจะพร้อมแล้วนะ นี่คือ memo หรือบันทึกช่วยจำถ้าคุณจะต้องทำให้ Jekyll กับ GitHub Pages มาอยู่ด้วยกัน - แบบไหนนะเหรอ? นั่นคือสิ่งที่เราหมายถึงว่า website ถูกสร้างขึ้นมาด้วย Jekyll แล้วก็เอาไป host ไว้บน GitHub Pages

และจากย่อหน้านี้ก็คือการเริ่มกันซะที - หลังจากที่ได้ทำการติดตั้ง Jekyll ลงบนเครื่องของเราเป็นที่เรียบร้อยแล้ว

#### ขั้นตอนที่ 1 (PC Ubuntu): สร้าง Jekyll local site
```bash
# สร้าง Jekyll site: ./sdeesreallife.github.io (ชื่อองค์กรตามด้วย.github.io)
$ jekyll new sdeesreallife.github.io

# เปลี่ยน path ไปที่: sdeesreallife.github.io
$ cd sdeesreallife.github.io

# สั่งให้ Jekyll ทำการ build site บน local server
$ bundle exec jekyll server

# เปิด browser ไปที่: http://localhost:4000
```
#### ขั้นตอนที่ 2: สร้าง Repository บน GitHub
Login เข้าใช้งาน GitHub

คลิกที่รูป Profile ของเรา แล้วเลือก Your Profile

สร้าง Repository ขึ้นมาใหม่ในชื่อเดียวกับชื่อองค์กรตามด้วย.github.io
`https://github.com/sdeesreallife/sdeesreallife.github.io`
#### ขั้นตอนที่ 3: Commit local site ไปที่ GitHub (PC Ubuntu)
```bash
$ cd sdeesreallife.github.io
$ git init
$ git remote add origin https://github.com/sdeesreallife/sdeesreallife.github.io
$ git add .
$ git commit -m "initial commit of the Jekyll's site template."
$ git push -u origin master

# เปิด browser ไปที่:https://sdeesreallife.github.io
```
#### Tips and Tricks
เพื่อให้การใช้งาน Jekyll บน loacl site สะดวกขึ้นอีกนิด เราจะใช้ Plugin Jekyll::Livereload ร่วมด้วย

ขั้นตอนการติดตั้ง: เพิ่มบรรทัด `gem 'jekyll-livereload'` ในไฟล์ Gemfile และสั่ง bundle
```bash
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.6"
  gem "jekyll-livereload" # เพิ่มบรรทัดนี้ลงไป
end

$ bundle
```

ขั้นตอนการรัน: ใช้คำสั่ง `jekyll serve --livereload` หรืออีกแบบที่เพิ่มการแสดง posts ที่เป็น drafts ให้ด้วย `bundle exec jekyll serve --drafts --livereload` - ผลลัพธ์ที่ได้คือทุกครั้งที่เราแก้ไข local site ต่อไปนี้ Jekyll จะทำการ auto regenerated และเพิ่มการ reload หน้าเว็บให้ด้วยเลย :)

<blockquote class="instagram-media" data-instgrm-captioned data-instgrm-version="7" style=" background:#FFF; border:0; border-radius:3px; box-shadow:0 0 1px 0 rgba(0,0,0,0.5),0 1px 10px 0 rgba(0,0,0,0.15); margin: 1px; max-width:658px; padding:0; width:99.375%; width:-webkit-calc(100% - 2px); width:calc(100% - 2px);"><div style="padding:8px;"> <div style=" background:#F8F8F8; line-height:0; margin-top:40px; padding:50.0% 0; text-align:center; width:100%;"> <div style=" background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAsCAMAAAApWqozAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAAAMUExURczMzPf399fX1+bm5mzY9AMAAADiSURBVDjLvZXbEsMgCES5/P8/t9FuRVCRmU73JWlzosgSIIZURCjo/ad+EQJJB4Hv8BFt+IDpQoCx1wjOSBFhh2XssxEIYn3ulI/6MNReE07UIWJEv8UEOWDS88LY97kqyTliJKKtuYBbruAyVh5wOHiXmpi5we58Ek028czwyuQdLKPG1Bkb4NnM+VeAnfHqn1k4+GPT6uGQcvu2h2OVuIf/gWUFyy8OWEpdyZSa3aVCqpVoVvzZZ2VTnn2wU8qzVjDDetO90GSy9mVLqtgYSy231MxrY6I2gGqjrTY0L8fxCxfCBbhWrsYYAAAAAElFTkSuQmCC); display:block; height:44px; margin:0 auto -44px; position:relative; top:-22px; width:44px;"></div></div> <p style=" margin:8px 0 0 0; padding:0 4px;"> <a href="https://www.instagram.com/p/BMllr6jBXQW/" style=" color:#000; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:normal; line-height:17px; text-decoration:none; word-wrap:break-word;" target="_blank">#SDEEsRealLife #SDEEsSelfie - Peg X and Lek</a></p> <p style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; line-height:17px; margin-bottom:0; margin-top:8px; overflow:hidden; padding:8px 0 7px; text-align:center; text-overflow:ellipsis; white-space:nowrap;">A post shared by Odd :) (@odd_daboss) on <time style=" font-family:Arial,sans-serif; font-size:14px; line-height:17px;" datetime="2016-11-09T11:14:11+00:00">Nov 9, 2016 at 3:14am PST</time></p></div></blockquote> <script async defer src="https://platform.instagram.com/en_US/embeds.js"></script>
