---
title: Python爬虫学习urllib.request之Get
url: 1360.html
id: 1360
categories:
  - Python功能
  - Python爬虫
  - 文章页
date: 2018-06-19 23:09:34
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/阿达下次再撒.jpg) **Get请求实例分析：** 代码：

import urllib.request

url="https://www.baidu.com/s?wd="
keyword = "strivez"
url1 = url+keyword
req = urllib.request.Request(url1)
req.add_header('User-Agent', 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36')
data= urllib.request.urlopen(req,timeout=80).read()
filenanme = open("F:/a.html","wb")
filenanme.write(data)

结果： ![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180619230553.png) ![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180619230615.png) **接下来对代码进行优化，由于之间介绍过的编码问题在地址中不能使用中文，因此要对想要查找的中文进行编码。** 代码：

import urllib.request

url="https://www.baidu.com/s?wd="
key = "你好"
keyword = urllib.request.quote(key)  #对中文进行编码
url1 = url+keyword
req = urllib.request.Request(url1)
req.add_header('User-Agent', 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36')
data= urllib.request.urlopen(req,timeout=80).read()
filenanme = open("F:/a.html","wb")
filenanme.write(data)
filenanme.close()

结果： ![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180619230648.png) 使用Get的请求思路：

*   构建对应的URL地址（一般为一个模板URL+关键词），该URL地址包含Get请求的字段名和字段内容等信息，且URL地址满足GET请求的格式，即“http://网址？字段名1=字段内容……”;（必要的时候要对字段内容进行编码）
*   以对应的URL为参数，构建Request
*   最好添加一下报头信息，以防止403错误
*   通过urlopen（）打开构建的Request对象
*   按照需求进行相关的后续处理