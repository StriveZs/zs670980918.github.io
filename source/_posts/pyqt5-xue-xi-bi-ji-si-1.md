---
title: PyQt5学习笔记（四）
url: 377.html
id: 377
categories:
  - Python模块PyQt5
  - 文章页
date: 2018-03-18 18:14:02
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180308122611.png) [んこんにちは皆さん、もう一度お会いできてうれしいです！！](https://translate.google.cn/#auto/zh-CN/%E3%82%93%E3%81%93%E3%82%93%E3%81%AB%E3%81%A1%E3%81%AF%E7%9A%86%E3%81%95%E3%82%93%E3%80%81%E3%82%82%E3%81%86%E4%B8%80%E5%BA%A6%E3%81%8A%E4%BC%9A%E3%81%84%E3%81%A7%E3%81%8D%E3%81%A6%E3%81%86%E3%82%8C%E3%81%97%E3%81%84%E3%81%A7%E3%81%99)   好久没发了，抱歉抱歉  O(∩_∩)O嘿嘿~ ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180308123017.png)   标签和文本输入框的使用： 文本输入框分为： 条形输入框：![](http://47.100.4.8/wp-content/uploads/2018/03/123123123123.png)   引用QLineEdit 矩形输入框： ![](http://47.100.4.8/wp-content/uploads/2018/03/2324234234.png) 引用QTextEdit 标签模块：![](http://47.100.4.8/wp-content/uploads/2018/03/657567567567.png)   引用QLabel 创建标签： title = QLabel('Title')   创建条形文本输入框： titleEdit = QLineEdit()   创建矩形文本输入框： reviewEdit = QTextEdit()   创建表格布局并且设置组件之间的间距 grid = QGridLayout() grid.setSpacing(10)   添加部件并且设置其位置（坐标形式）： grid.addWidget(reviewEdit,3,1,5,1) 3,1 为其行列  5,1为其中心点的坐标   将表格布局添加到窗口界面： self.setLayout(grid)     状态栏创建： class Example(QMainWindow): def \_\_init\_\_(self): super().\_\_init\_\_() self.initUI() 窗口继承了QMainWindow类  self则代表一个该对象   创建一个状态栏并且显示一个信息： self.statusBar().showMessage('Ready') 使用statusBar（）创建一个状态栏 使用showMessage（‘信息’）  来显示信息 注：不能重复使用否则不会进行覆盖 如下： self.statusBar().showMessage('Ready') self.statusBar().showMessage('    ') self.statusBar().showMessage('Hello World') ![](http://47.100.4.8/wp-content/uploads/2018/03/中心擦伤的请问如果.png) [代码记录四](http://47.100.4.8/wp-content/uploads/2018/03/代码记录四.rar) End！ ![](http://47.100.4.8/wp-content/uploads/2018/03/timg-1-300x225.jpg)