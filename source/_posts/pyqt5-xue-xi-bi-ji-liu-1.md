---
title: PyQt5学习笔记（六）
url: 481.html
id: 481
categories:
  - Python模块PyQt5
  - 文章页
date: 2018-03-31 23:13:20
tags:
  - Python
  - PyQt5
  - 学习笔记
---

![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180308122611.png) 很久没发这个了…… 今天就发点存货吧23333 ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180308123017.png) QLCDNumber控件用于显示一个LCD数字。 它可以显示几乎任意大小的数字。可以显示十进制、十六进制、八进制或二进制数。很容易使用display()槽连接到数据源，这个槽可以被任何五个参数类型的数据源重载。 ![](http://47.100.4.8/wp-content/uploads/2018/03/按我发的股发行.png) 创建一个QLCDNumber对象 **lcd = QLCDNumber(self)**   将滑动条的滑动连接到数字上 在这里我们将滚动条的valueChanged信号连接到lcd的display插槽。 **sld.valueChanged.connect(lcd.display)** lcd.display  就是连接其他控制接口   QSlider部件提供了一个垂直或水平滑动条。 QSlider很少有自己的函数，大部分功能在QAbstractSlider中。最有用的函数是setValue()，用来设置滑块的当前值；triggerAction()来模拟点击的效果（对快捷键有用），setSingleStep()、setPageStep()用来设置步长，setMinimum()和setMaximum()用于定义滚动条的范围。 QSlider提供了一些方法来控制刻度标记。可以使用setTickPosition()来表示刻度标记的位置，使用setTickInterval()来指定刻度的间隔；当前设置的刻度位置和间隔可以分别使用tickPosition()和tickInterval()函数来查询。 ![](http://47.100.4.8/wp-content/uploads/2018/03/向翡翠是递四方速递发的.png) QSlider只提供整数范围。   创建一个水平滑动条 **sld = QSlider(Qt.Horizontal,self)** 将水平滑动条绑定LCD数字显示 **sld.valueChanged.connect(lcd.display)**   End！ [代码记录](http://47.100.4.8/wp-content/uploads/2018/03/代码记录.rar) ![](http://47.100.4.8/wp-content/uploads/2018/03/dc3a92315c6034a8e725e5f8c2134954082376a7-1.jpg)