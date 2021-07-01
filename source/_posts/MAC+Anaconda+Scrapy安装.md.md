---
title: MAC+Anaconda+Scrapy安装以及简单使用

categories:
  - MAC
  - Anaconda
  - Scrapy

tags:
  - Scrapy
  - Python
  - MAC
  - Anaconda
---

# MAC+Anaconda+Scrapy安装
## Scarpy
Scrapy由 Python 编写的爬虫框架。如果你刚接触并且好奇这门语言的特性以及Scrapy的详情， 对于已经熟悉其他语言并且想快速学习Python的编程老手， 我们推荐 Learn Python The Hard Way ， 对于想从Python开始学习的编程新手， [非程序员的Python学习资料列表](http://wiki.python.org/moin/BeginnersGuide/NonProgrammers)。

## 创建新的虚拟环境
首先在Anaconda上使用如下命令创建新的虚拟环境。

```
创建环境:
conda create -n env'name python==python版本

激活环境:
conda actiavte env'name
```

## 安装
在终端输入如下命令进行安装
```
conda install scrapy
```

## 入门
思维导图:

![figure.1](https://gitee.com/zyp521/upload_image/raw/master/Scrapy入门.png)

### 创建项目
使用如下命令创建一个Scrapy项目，其中tutorial为项目名称（事先使用命令行进入你想要创建项目的目录下）

```
scarpy startproject tutorial
```

创建的项目结构为:
```
tutorial/
    scrapy.cfg
    tutorial/
        __init__.py
        items.py
        pipelines.py
        settings.py
        spiders/
            __init__.py
            ...
```

这些文件分别是:
- scrapy.cfg: 项目的配置文件
- tutorial/: 该项目的python模块。之后您将在此加入代码。
- tutorial/items.py: 项目中的item文件.
- tutorial/pipelines.py: 项目中的pipelines文件.
- tutorial/settings.py: 项目的设置文件.
- tutorial/spiders/: 放置spider代码的目录

### 定义Item
这里的Item是用来存储爬虫爬取到的数据的容器，它的使用方法和python的字典机制十分相似，并且它提供了额外的保护机制来避免拼写错误导致的未定义名称报错。  

类似Java/C++中的类继承机制一样，你可以编写一个scrapy.item类，该类继承scrapy.Item，通过定义一个类型为 **scrapy.Field** 的类属性来定义一个Item。  

在创建这个Item之前，我们需要对需要爬取的数据进行建模，在完成建模之后，在Item中定义响应的字段，即编写tutorial目录中的items.py文件：

例子(这里以爬取百度图片):
```
import scrapy

class DmozItem(scrapy.Item):
    title = scrapy.Field()
    link = scrapy.Field()
    desc = scrapy.Field()
```

### 编写爬虫例子
Spider(爬虫)是用户编写用于从单个网站或者一些网站爬取数据的类。  

其中包含了一个用于下载的初始URL，如何跟进网页中的连接以及如何分析页面中的内容，提取生成item的方法。  

为了创建一个Spider，您必须继承 scrapy.Spider 类， 且定义以下三个属性:

- name: 用于区别Spider。 该名字必须是唯一的，不可以为不同的Spider设定相同的名字。
- start_urls: 包含了Spider在启动时进行爬取的url列表。 因此，第一个被获取到的页面将是其中之一。 后续的URL则从初始的URL获取到的数据中提取。
- parse() 是spider的一个方法。 被调用时，每个初始URL完成下载后生成的 Response 对象将会作为唯一的参数传递给该函数。 该方法负责解析返回的数据(response data)，提取数据(生成item)以及生成需要进一步处理的URL的 Request 对象。

Spider示例:创建一个spider文件放在tutorial/spiders文件目录下，代码如下：

```
import scrapy

class DmozSpider(scrapy.Spider):
    name = "dmoz"
    allowed_domains = ["dmoz.org"]
    start_urls = [
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Books/",
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Resources/"
    ]

    def parse(self, response):
        filename = response.url.split("/")[-2]
        with open(filename, 'wb') as f:
            f.write(response.body)
```

![figure.2](https://gitee.com/zyp521/upload_image/raw/master/Rz97TH.png)

刚才发生的过程为：Scrapy为Spider的 start_urls 属性中的每个URL创建了 scrapy.Request 对象，并将 parse 方法作为回调函数(callback)赋值给了Request。

Request对象经过调度，执行生成 scrapy.http.Response 对象并送回给spider parse() 方法。

#### 提取数据
Scrapy提取数据有自己的一套机制。它们被称作选择器(seletors)，因为他们通过特定的 XPath 或者 CSS 表达式来“选择” HTML文件中的某个部分。有关selectors的使用暂时先跳过，放在后面进行学习。  
先使用如下代码进行：

```
import scrapy
class DmozSpider(scrapy.Spider):
    name = "dmoz"
    allowed_domains = ["dmoz.org"]
    start_urls = [
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Books/",
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Resources/"
    ]

    def parse(self, response):
        for sel in response.xpath('//ul/li'):
            title = sel.xpath('a/text()').extract()
            link = sel.xpath('a/@href').extract()
            desc = sel.xpath('text()').extract()
            print(title, link, desc)
```

#### 使用Item存储提取的数据
Item对象是我们在Item.py文件中创建的类，我们通过创建一个/多个对象来存储我们提取得到的数据，通过字典的方式来访问每个属性，然后对每个属性进行赋值。

```
import scrapy

from scrapyProject.items import ScrapyprojectItem

class DmozSpider(scrapy.Spider):
    name = "dmoz"
    allowed_domains = ["dmoz.org"]
    start_urls = [
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Books/",
        "http://www.dmoz.org/Computers/Programming/Languages/Python/Resources/"
    ]

    def parse(self, response):
        for sel in response.xpath('//ul/li'):
            item = ScrapyprojectItem()
            item['title'] = sel.xpath('a/text()').extract()
            item['link'] = sel.xpath('a/@href').extract()
            item['desc'] = sel.xpath('text()').extract()
            yield item
```

### 保存爬取到的数据
最简单存储爬取的数据的方式是使用 Feed exports:
```
scrapy crawl dmoz -o items.json
```

该命令将采用 JSON 格式对爬取的数据进行序列化，生成 items.json 文件。

在类似本篇教程里这样小规模的项目中，这种存储方式已经足够。 如果需要对爬取到的item做更多更为复杂的操作，您可以编写 Item Pipeline 。 类似于我们在创建项目时对Item做的，用于您编写自己的 tutorial/pipelines.py 也被创建。 不过如果您仅仅想要保存item，您不需要实现任何的pipeline。

### 问题记录
1. 报错：ModuleNotFoundError: No module named 'protego'  
使用conda 安装protego包即可解决。  

```
conda install protego
```

2. 失败说明
由于链接我尝试自己访问了一下发现无法访问了，应该是国外网站（墙的问题），暂时还没学xpath相关的知识，因此打算在之后尝试一下国内的网站使用。