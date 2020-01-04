---
title: k-邻近算法应用实例以及分析
url: 553.html
id: 553
categories:
  - k-邻近算法
  - 文章页
  - 机器学习
date: 2018-04-09 18:20:54
tags:
  - Machine Learning
  - KNN
---

![](http://47.100.4.8/wp-content/uploads/2018/04/timg.jpg) 这里的实例是手写数字识别系统。 步骤：

*   收集数据：提供文本文件。
*   准备数据：编写函数img2vector（），将图像格式转换为分类器使用的向量格式
*   分析数据：在python命令提示符中检查数据，确保它符合要求
*   训练算法：此步骤不适用于k-邻近算法
*   测试算法：编写函数使用提供的部分数据集作为测试样本，测试样本与费测试样本的区别在于测试样本是已经完成分类的数据，如果预测分类与实际分类类别不同，则标记为一个错误。
*   使用算法：本实例中没有此步骤

准备数据：将图像转换为测试向量 ![](http://47.100.4.8/wp-content/uploads/2018/04/11.png) 文档内容：（这里已经将手写的数字转换为了01数字） ![](http://47.100.4.8/wp-content/uploads/2018/04/22.png) 得到的向量就是一个一个array数组。   使用算法： ![](http://47.100.4.8/wp-content/uploads/2018/04/33.png) 训练数据集文件名： ![](http://47.100.4.8/wp-content/uploads/2018/04/44.png) 测试数据集文件名： ![](http://47.100.4.8/wp-content/uploads/2018/04/55.png) 使用： ![](http://47.100.4.8/wp-content/uploads/2018/04/66.png) 运行代码的结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/77.png) 上面测试文件的下载地址：https://download.csdn.net/download/qq_16184125/10332382 End！