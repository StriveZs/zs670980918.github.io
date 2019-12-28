---
title: Python数据分析学习笔记（四）
url: 626.html
id: 626
categories:
  - python数据分析
  - 文章页
date: 2018-04-18 18:19:05
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180322184136.png)   切片操作： 在每个维度上给出一个切片空间 ![](http://47.100.4.8/wp-content/uploads/2018/04/3231341234.png) 第一个冒号是对于在第一个维度上覆盖了所有元素 ![](http://47.100.4.8/wp-content/uploads/2018/04/324234132123.png) ndarray数组的运算：   数据与标量之间的运算作用于数组的每一个元素 比如： a和b都是ndarray数组 a\*\*2 + b\*\*3 = c  即为a和b中每一个元素进行平方和三次方运算相加 存储到c中 ndarray数组a  的平均值为：a.mean() ![](http://47.100.4.8/wp-content/uploads/2018/04/33333333333333123123.png) numpy的一元函数： ![](http://47.100.4.8/wp-content/uploads/2018/04/213123123123.png) ![](http://47.100.4.8/wp-content/uploads/2018/04/2132132131241.png) 示例： ![](http://47.100.4.8/wp-content/uploads/2018/04/123543213.png) ![](http://47.100.4.8/wp-content/uploads/2018/04/111111111111111111111111111111.png) 运算后的元素是生成了另一组元素 如果想要修改a数组的值 那么需要将结果在赋值给a  a = np.rint（a）     numpy的二元函数： ![](http://47.100.4.8/wp-content/uploads/2018/04/2131234322222222222222222222.png) 示例： ![](http://47.100.4.8/wp-content/uploads/2018/04/呃呃呃呃呃呃鹅鹅鹅鹅鹅鹅饿.png) 整数和浮点数进行运算 运算的结果就是浮点数   End！ ![](http://47.100.4.8/wp-content/uploads/2018/04/371122f3d7ca7bcb55c99a56b7096b63f624a83c.jpg)