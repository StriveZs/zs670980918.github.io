---
title: Python爬虫学习笔记
url: 1262.html
id: 1262
categories:
  - Python功能
  - Python爬虫
  - 文章页
date: 2018-05-26 12:42:55
tags:
---

Urllib库是python中一个用于操作URL的模块。 在Python3.X中一些库引用名： import urllib.request import urllib.error import urllib.parse import urllib.urlopen import urllib.urlencode import urllib.quote http.CookieJar urllib.request.Request  **快速爬取一个网页：** 使用file=urllib.request.urlopen() 打开并爬取一个网页 使用file.read() 读取网页内容 也可以使用file.readline（）读取一行内容 具体代码如下：

import urllib.request

file = urllib.request.urlopen("http://strivezs.com")
data = file.read()
dataline = file.readline()

print(data)
print(dataline)

  结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/147.png) 等太长了不复制了就。上面就是成功爬取下来后得到的网页的html代码 这里需要的注意的是： 通过使用read（）得到的内容会以字符串的形式存储。 而通过readline（）得到的是会以列表的形式存储   将爬取到的网页以htm的形式保存：

import urllib.request

file = urllib.request.urlopen("http://strivezs.com")
data = file.read()
dataline = file.readline()

filestring = open("F:/data.html","wb")
filestring.write(data)

结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/1-8.png) 同样还可以使用txt，等其他形式进行保存。 也可以使用urllib.request.urlretrieve直接对网页进行爬取并自动保存到本地设置的路径。

filename = urllib.request.urlretrieve("http://strivezs.com",filename="F://2.html")
urllib.request.urlcleanup()  #清除urlretrieve（）造成缓存

结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/2-8.png) 返回与当前环境有关的信息使用info（）进行返回 print(file.info()) 调用的格式为爬取网页.info（）   获得爬取网页的状态码使用getcode（） print(file.getcode()) 调用格式为：爬取网页.getcode（）   获得爬取网页的url使用geturl（） print(file.geturl()) 调用格式爬取网页.geturl（）   需要注意的是：url标准中只会允许一部分ASCII字符比如数组。字母。部分符号等。而一些其他字符比如汉字等则不符合标准。 如果我们在URL中使用一些其他不符合标准的字符就会出现问题，此时可以使用URL编码的方式解决。 使用urllib.request.quote（网址）进行编码 使用urllib.request.unquote（编码后的网址）进行解码 使用：

import urllib.request

file = urllib.request.urlopen("http://strivezs.com")
data = file.read()
dataline = file.readline()
print(file.info())
print(file.getcode())
print(file.geturl())

**浏览器的模拟——Headers属性** headers={“**User-Agent”,** “Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36” } 在爬取某些网页时会出现403错误，则证明该网页在robots协议中拒绝了爬虫。 使用build_opener（）修改报头：

import urllib.request

url="http://strivezs.com"
headers={"User-Agent", "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36"}
opener = urllib.request.build_opener()
opener.addheaders = \[headers\]
data=opener.open(url).read()

  上面这种方法不作具体的介绍了。 使用add_header（）添加报头：  这里我更加推荐使用这种方法，因为比较简单好理解。 代码：

import urllib.request

url="http://strivezs.com"
req = urllib.request.Request(url)
req.add_header('User-Agent', 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36')
data= urllib.request.urlopen(req).read()
print(data)

  add_header（）是用来添加对应的报头信息   超时设置： 有时我们在访问一个网页时长时间没有响应，系统就会判断超时了，然后就无法打开网页。 但是有时我们需要根据自己的需求来设置超时的时间。一般都设为80秒。 代码：

import urllib.request

url="http://strivezs.com"
headers=\['User-Agent', 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36'\]
req = urllib.request.Request(url)
req.add_header('User-Agent', 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36')
data= urllib.request.urlopen(req,timeout=80).read()

  Http协议请求主要分为6种类型，各类型的主要作用如下：

*   Get请求：GET请求会通过URL网址传递信息，可以直接在URL中写上要传递的信息，也可以由表单进行传递。如果使用表单进行传递，这表单中的信息会自动转为URL地址中的数据，通过URL地址传递。
*   Post请求：可以向服务器提交数据，是一种比较主流也比较安全的数据传递方式，比如登陆时，经常使用Post请求发送地址。
*   Put请求：请求服务器存储一个资源，通常要指定存储的位置。
*   Delete请求：请求服务器删除一个数据
*   Head请求：请求获得服务器报头信息
*   Options请求：可以获得当前URL所支持的请求类型