---
title: Python爬虫的定向爬取技术
url: 439.html
id: 439
categories:
  - Python功能
  - 文章页
date: 2018-03-26 22:20:46
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/03/阿达下次再撒-300x188.jpg)

### Python爬虫的定向爬取技术就是根据设置的主题，对要爬取的网址或者网页中的内容进行筛选。

  ![](http://47.100.4.8/wp-content/uploads/2018/03/u39006933292571644373fm27gp0-300x198.jpg) 爬虫定向爬取技术主要需要解决的三个问题 1.清晰地定义好爬虫爬取的目标，规划好主题。 2.建立好爬取网址的过滤筛选规则以及内容的过滤筛选规则 3.建立好URL排序算法，让爬虫能够明确优先爬取哪些页面，以什么顺序爬取待爬取的网页。   ![](http://47.100.4.8/wp-content/uploads/2018/03/0x0ss-85-300x300.jpg) 定向爬取某些信息的步骤主要有： 1.理清爬取的目的 2.设置网址的过滤规则 3.设置好内容采集规则 4.规划好采集任务 5.将采集结果进行相应的修正，处理成我们想要的格式 6.对结果进行进一步的处理，来完成任务   ![](http://47.100.4.8/wp-content/uploads/2018/03/u16344762390419462fm200gp0-298x300.jpg) 进行信息筛选的主要策略有： 1.通过正则表达式筛选 一些简单的操作符： ![](http://47.100.4.8/wp-content/uploads/2018/03/123123122323123-300x133.png) ![](http://47.100.4.8/wp-content/uploads/2018/03/21334543345-300x127.png) 2.通过Xpath表达式筛选 简介： XPath即为XML路径语言，它是一种用来确定[XML](https://baike.baidu.com/item/XML)（[标准通用标记语言](https://baike.baidu.com/item/%E6%A0%87%E5%87%86%E9%80%9A%E7%94%A8%E6%A0%87%E8%AE%B0%E8%AF%AD%E8%A8%80)的子集）文档中某部分位置的语言。XPath基于XML的树状结构，有不同类型的节点，包括元素节点，属性节点和文本节点，提供在数据结构树中找寻节点的能力。\[1\]  起初 XPath 的提出的初衷是将其作为一个通用的、介于XPointer与XSLT间的语法模型。但是 XPath 很快的被开发者采用来当作小型查询语言。 3.通过xslt筛选 简介： 在计算机科学中，XSLT是 **扩展样式表转换语言** 的外语缩写，这是一种对[XML](https://baike.baidu.com/item/XML)（[标准通用标记语言](https://baike.baidu.com/item/%E6%A0%87%E5%87%86%E9%80%9A%E7%94%A8%E6%A0%87%E8%AE%B0%E8%AF%AD%E8%A8%80)的子集）[文档](https://baike.baidu.com/item/%E6%96%87%E6%A1%A3)进行转化的语言，XSLT中的T代表英语中的“转换”（**T**_r__ansformation_）。它是**XSL**（_e_**X**_tensible_ **S**_tylesheet_ **L**_anguage_）规范的一部分。