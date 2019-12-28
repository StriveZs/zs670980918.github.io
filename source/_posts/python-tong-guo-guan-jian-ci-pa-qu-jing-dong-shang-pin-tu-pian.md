---
title: python通过关键词爬取京东商品图片
url: 1340.html
id: 1340
categories:
  - Python功能
  - Python爬虫
  - 文章页
date: 2018-06-08 23:26:26
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/u407244128253124607fm27gp0.jpg) 最近在看爬虫方面的知识，所以写了一个小爬虫可以爬取京东商城商品的图片，可以通过关键词进行搜索指定的商品，也可以进行多页爬取。 具体实现代码：  

import urllib.request
import re
import requests
import os

url="https://search.jd.com/Search?keyword="

def CrawImg(url,page):
    headers = \['User-Agent',
               'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36'\]
    req =urllib.request.Request(url)
    req.add_header(headers\[0\],headers\[1\])
    data = urllib.request.urlopen(req).read()
    data = str(data)
    re1 = '<div class="gl-i-wrap">.+</div>'
    result1 = re.compile(re1).findall(data)
    result1 = str(result1)  #首次信息筛选
    re2 = '<img width="220" height="220" class="err-product" data-img="1" (.+?)>'
    result2 = re.compile(re2).findall(result1)
    result2 = str(result2) #再次筛选
    re3 = '//.+?\\.jpg'
    result3 = re.compile(re3).findall(result2)  #最终得到图片地址
    return result3

i=1
keyword=input("输入要查询的内容：")
keyword = urllib.request.quote(keyword)
for x in range(1,2):
    url = url + keyword +"&enc=utf-8&page="+str(x)
    imglist = CrawImg(url,x)
    print(url)
    for img in imglist:
        imgname = "G:/paqu/img/图片"+str(i)+".jpg"
        imgurl = "http:"+str(img)
        if not os.path.exists(imgname):  # 检查文件名是否存在
            r = requests.get(imgurl)
            r.encoding = r.apparent_encoding
            with open(imgname, 'wb')as f:
                f.write(r.content)
                f.close()
            i += 1

结果： ![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180608232235.png) ![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180608232338.png) 后来想爬取一下百度图片首页每天推荐的图片发现返回的html代码中imglist没有我想要的结果。貌似百度给他隐藏了，反正我搞了半天没搞出来，后来使用beautifulsoup库返回相关的标签属性发现为空。 然后就凉了，有兴趣的朋友可以自己去看看。 如果弄出来可以手动@我，谢谢