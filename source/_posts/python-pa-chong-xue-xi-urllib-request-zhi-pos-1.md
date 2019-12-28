---
title: Python爬虫学习urllib.request之Post
url: 1365.html
id: 1365
categories:
  - Python功能
  - Python爬虫
  - 文章页
date: 2018-06-20 12:55:10
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180620124632.png) **Post请求分析** 实现思路：

*   设置好URL网址
*   构建表单数据，并使用parse.urlencode对数据进行编码处理
*   创建Request对象，参数包括URL地址和要传递的数据
*   使用add_header（）添加头信息，模拟浏览器进行爬取
*   使用request.urlopen（）打开对应的Request对象，完成信息的传递
*   后续处理，比如读取内容，将内容写入文件

代码：

import urllib.request
import urllib.parse

url = "https://www.zhihu.com/sign"
data={"username":"54651565@qq.com","password":"1223131233"}
postdata = urllib.parse.urlencode(data).encode('utf-8')
headers = \['User-Agent', 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36'\]
req = urllib.request.Request(url,postdata)
req.add_header(headers\[0\],headers\[1\])
data = urllib.request.urlopen(req).read()
filename  = open("F:/a.html","wb")
filename.write(data)
filename.close()

post主要用于进行网页提交信息时候用，或者在登陆网站上面使用。后面会介绍使用cookie进行登陆。   **post请求时，在\_data，\_full_data,data 中都可以看到请求的参数，然后这些参数可以设置对应格式的字典，对字典进行编码后可以使用post进行提交。** ![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180620125213.png) post信息可以在网页界面按F12键 network中进行查看。如果不想用也可以使用fiddler进行获取。