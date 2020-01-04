---
title: Python数据分析学习笔记（二）
url: 425.html
id: 425
categories:
  - python数据分析
  - 文章页
date: 2018-03-23 23:45:03
tags:
  - Python
  - Data analysis
  - Numpy
---

![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180322184136.png) 今天依旧是这个。23333   这里是一个例子： import numpy;   print('生成数组') a = \[1,2,3,4,5\]  #创建列表元素 x = numpy.array(a)  #创建数组  列表形式 print(x) #打印数组 print(x.ndim) #打印数组维度 print(x.shape) #打印数组各个维度的长度 shape 是一个元祖 print(x.dtype) #打印数组元素的类型   print('使用zeros/ones/empty创建数组:根据shape来创建') x = numpy.zeros(6) #创建维度为6的，元素都是0的一维数组 print(x)   x = numpy.zeros((2,3)) #创建一维长度为2,二维长度为3的二维0数组 print(x)   x = numpy.ones((2,3)) #创建一维长度为2，二维长度为3的二维1数组 print(x)   x = numpy.empty((3,3)) #创建一维长度为2，二维长度为3，未初始化的二维数组 print(x)   print('使用arrange生成连续元素') print(numpy.arange(6)) #创建一个长度为6的连续区间 print(numpy.arange(0,6,2))  #创建一个从开始到6结束（不算6），步长为2的区间   由于服务器出了点问题。上传图片上传半天都没反应，难受香菇所以暂时是没有了。这能以上面的这个例子来给出参考了。