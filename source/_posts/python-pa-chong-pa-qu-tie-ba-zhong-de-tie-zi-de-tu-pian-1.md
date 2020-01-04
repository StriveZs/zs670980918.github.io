---
title: Python爬虫爬取贴吧中的帖子的图片
url: 473.html
id: 473
categories:
  - Python功能
  - Python爬虫
  - 文章页
date: 2018-03-30 11:46:28
tags:
  - Python
  - 爬虫
---

![](http://47.100.4.8/wp-content/uploads/2018/03/timg-6.jpg) Python爬虫的一些小程序： 网址：[壁纸](https://tieba.baidu.com/p/4364768066) 用谷歌浏览器的开发工具检查网页，可以发现其每一张图片都有如下格式![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180330114139.png) 所有图片在代码中的相同点就是都以<img class="BDE_Image"开头且都有相似的src。 图片的src可以通过正则表达式来获取 ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180330114216.png) 解释：\[^”\]+. 多次匹配除”以外的所有字符，\\. 是转义 . (.是正则表达式的一种符号，要表达 . 必须转义) 知道了这些，就能获取到页面中的图片，下面用Python来实现这个网络爬虫。 每一句都有注释↓__↓ ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180330114248.png) ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180330114319.png)   代码文件：[代码](http://47.100.4.8/wp-content/uploads/2018/03/代码.rar)   ![](http://47.100.4.8/wp-content/uploads/2018/03/timg-1.jpg)