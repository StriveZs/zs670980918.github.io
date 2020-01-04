---
title: python网址二维码生成
url: 1271.html
id: 1271
categories:
  - Python功能
  - 文章页
date: 2018-05-28 21:45:58
tags:
  - Python
---

![](http://47.100.4.8/wp-content/uploads/2018/05/qr.png) 先上效果图，这是我网站的二维码，其中中间的图片要求是ico格式，（这里可以结合我之前的提供的ico转换器使用） 接下来给出具体代码：（暂时还没有做GUI图形界面以后会发的。） 所以这里先上代码了 需要注意的是需要自己安装qrcode库
```
import qrcode
from PIL import Image
import os


def gen_qrcode(string, path, logo=""):
    qr = qrcode.QRCode(
        version=2,
        error\_correction=qrcode.constants.ERROR\_CORRECT_H,
        box_size=8,
        border=1
    )
    qr.add_data(string)
    qr.make(fit=True)

    img = qr.make_image()
    img = img.convert("RGBA")

    if logo and os.path.exists(logo):
        icon = Image.open(logo)
        img\_w, img\_h = img.size
        factor = 4
        size\_w = int(img\_w / factor)
        size\_h = int(img\_h / factor)

        icon\_w, icon\_h = icon.size
        if icon\_w > size\_w:
            icon\_w = size\_w
        if icon\_h > size\_h:
            icon\_h = size\_h
        icon = icon.resize((icon\_w, icon\_h), Image.ANTIALIAS)

        w = int((img\_w - icon\_w) / 2)
        h = int((img\_h - icon\_h) / 2)
        icon = icon.convert("RGBA")
        img.paste(icon, (w, h), icon)
    img.save(path)

if \_\_name\_\_ == "\_\_main\_\_":
   gen_qrcode('http://strivezs.com',"F:/qr.png", "F:/a.ico")
```
这里需要在代码里面手动设置地址。