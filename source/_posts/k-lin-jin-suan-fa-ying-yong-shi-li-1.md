---
title: k-邻近算法应用实例
url: 542.html
id: 542
categories:
  - k-邻近算法
  - 文章页
  - 机器学习
date: 2018-04-08 12:10:16
tags:
  - Machine Learnig
  - KNN
  - Matplotlib
---

这里使用k-邻近算法解决约会网站问题： 步骤：

*   收集数据：提供文本文件。
*   准备数据：使用python解析文本文件。
*   分析算法：使用Matplotlib画二维扩散图
*   训练算法：此步骤使用于k-邻近算法
*   测试算法：使用海伦提供的部分数据作为测试样本。测试样本和费测试样本的区别在于：测试样本是已经完成分类的数据，如果预测分类与实际类别不同，则标记为一个错误。
*   使用算法：产生简单的命令行程序，然后海伦可以输入一些特征数据以判断对方是否为自己喜欢的类型。

准备数据算法： ![](http://47.100.4.8/wp-content/uploads/2018/04/圣诞节好想吃.png) 测试算法： 使用matplotlib绘制第一列和第二列所有数据的散点图 ![](http://47.100.4.8/wp-content/uploads/2018/04/下水道法规.png) ![](http://47.100.4.8/wp-content/uploads/2018/04/个人特让他.png) 归一化特征值：在有的时候会有一个特征值占的权重比较大影响整个计算结果，因此要进行归一化。即将所有的数据范围限制到0到1或-1到1之间 可以使用公式：newvalue=（oldValue-min）/（max-min） max和min分别是数据集中的最小特征值和最大特征值 ![](http://47.100.4.8/wp-content/uploads/2018/04/当非同热腾腾.png) 测试代码： ![](http://47.100.4.8/wp-content/uploads/2018/04/突然热腾腾.png) 结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/额外热污染天.png) 约会网站预测函数： ![](http://47.100.4.8/wp-content/uploads/2018/04/突然对方而儿童.png) 测试： ![](http://47.100.4.8/wp-content/uploads/2018/04/1111111123123123.png)![](http://47.100.4.8/wp-content/uploads/2018/04/32443123123.png)   里面的datingtestset2.txt数据集文件的下载地址： https://download.csdn.net/download/qq_16184125/10331188