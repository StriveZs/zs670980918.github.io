---
title: Python数据分析学习笔记（三）
url: 487.html
id: 487
categories:
  - python数据分析
  - 文章页
date: 2018-04-01 22:48:13
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180322184136.png) 还有好多存货没有发。只能先发发这个课…… 在Ipython提示符下： ![](http://47.100.4.8/wp-content/uploads/2018/04/3321321.png) ndarray对象属性： ![](http://47.100.4.8/wp-content/uploads/2018/04/1232321312.png) ![](http://47.100.4.8/wp-content/uploads/2018/04/32434123213.png) ndarray的元素类型： ![](http://47.100.4.8/wp-content/uploads/2018/04/4232423123.png) 支持布尔类型 intc（与c语言中int类型一样） intp（用于索引的整数） int8（字节长度整数类型） int16（16位的整数类型） int32（……） int64（……）   没有负数的整数类型  无符号整数 ![](http://47.100.4.8/wp-content/uploads/2018/04/321231235412.png) 使用ndarray数组创建非同质对象构成。 ![](http://47.100.4.8/wp-content/uploads/2018/04/45343242.png) ![](http://47.100.4.8/wp-content/uploads/2018/04/2134324234.png)![](http://47.100.4.8/wp-content/uploads/2018/04/12321543534.png) 数据类型为O   则代表的是对象类型 当ndarray的元素数据类型不同的时候，或者每一个元素的维度数量不相同的是时候，ndarray会将每一个元素认为一个对象 当ndarray非同质时不能放回numpy的优势   一维数组的索引和切片的python的列表相似。 ![](http://47.100.4.8/wp-content/uploads/2018/04/1111111111111111.png) a\[① : ② : ③\]  第一部分是起始编号 第二部分是终止编号 第三部分是步长   多维数据索引和切片：   索引操作： np.arange(24)用来生成一个一维数组  使用reshape（（2,3,4））改变格式 这样刚才的一维数据就生成了2,3,4维度的数组 通过索引来访问 ![](http://47.100.4.8/wp-content/uploads/2018/04/12312312312312312323123123.png) ![](http://47.100.4.8/wp-content/uploads/2018/04/22222222222222222222.png) 上面的图示可得 一维数组（0-23）被分为了两个大的数组 其中每一个数组又被分为了三个数组 其中每个的数组又被分为了四个元素 End！ [代码记录三](http://47.100.4.8/wp-content/uploads/2018/04/代码记录三.rar) ![](http://47.100.4.8/wp-content/uploads/2018/03/timg-1.jpg)