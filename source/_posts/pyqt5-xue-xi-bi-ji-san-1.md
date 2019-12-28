---
title: PyQt5学习笔记（三）
url: 325.html
id: 325
categories:
  - Python模块PyQt5
  - 文章页
date: 2018-03-12 18:15:48
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180308122611.png) 偶哈呦，敏娜！ O(∩_∩)O~   今天继续发PyQt5的学习笔记，最近比较忙只能发一些自己写的以前的东西了，请见谅(*^▽^*)~   ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180308123017.png) 框布局控制： 创建水平布局： hbox = QHBoxLayout() 添加水平布局的伸展因子和添加按钮 hbox.addStretch(1) hbox.addWidget(okButton)   创建竖直布局： vbox = QVBoxLayout() 添加竖直布局的伸展因子 vbox.addStretch(1) 将水平布局添加到竖直布局中 vbox.addLayout(hbox)   设置窗口的布局界面： self.setLayout(vbox)   效果图： ![](http://47.100.4.8/wp-content/uploads/2018/03/zxc-300x227.png)   接下来是： 表格布局控制：  import QGridLayout 创建表格布局： grid = QGridLayout()   给表格布局添加元素 grid.addWidget()   设置到窗口上： self.setLayout(grid)   表格布局形式以坐标定位i，j  添加按钮： grid.addWidget(button,*position) postion为坐标 ![](http://47.100.4.8/wp-content/uploads/2018/03/爱上大声地周星驰-300x169.png)   End！ ![](http://47.100.4.8/wp-content/uploads/2018/03/cropped-1474764002363-2.jpeg) **ヾ(ToT)Bye~Bye~** [代码记录三](http://47.100.4.8/wp-content/uploads/2018/03/代码记录三.rar)