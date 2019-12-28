---
title: PyQt5学习笔记（二）
url: 275.html
id: 275
categories:
  - Python模块PyQt5
  - 文章页
date: 2018-03-10 12:39:21
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180308122611.png)

### PyQt简介：

### **PyQt**实现了一个Python模块集。它有超过300类，将近6000个函数和方法。它是一个多平台的工具包，可以运行在所有主要操作系统上，包括UNIX，Windows和Mac。 **PyQt采用双许可证，开发人员可以选择GPL和商业许可。在此之前，GPL的版本只能用在Unix上，从PyQt的版本4开始，GPL许可证可用于所有支持的平台。**

依旧是基础知识，一些基础的内容，相关的控件的使用。 3333……(￣ノへ￣、)

～(￣▽￣～)(～￣▽￣)～

![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180308123017.png)

**显示一个按钮的提示语：首先设置一个用于显示工具提示的字体。** 我们使用10px滑体字体 **QToolTip.setFont(QFont('SanSerif',10))** 设置字体的文本格式： **self.setToolTip('This is a <b>QWidget</b>widget')** 将提示语绑定到按钮上 并且设置提示内容 **btn .setToolTip('This is a <b>QPushButton</b> widget')** 效果图**：![](http://47.100.4.8/wp-content/uploads/2018/03/请问请问-300x227.png)** **qbtn.clicked.connect(QCoreApplication.instance().quit)** 使用MessageBox 来进行消息提示 重新定义了窗口的点X之后的事件： **def closeEvent(self, QCloseEvent)** 将reply 绑定上messagebox 并且设置信息提示语和yes | no按钮 reply用来接收返回的信息 **reply = QMessageBox.question(self,'Message',"Are you sure to quit?",QMessageBox.Yes | QMessageBox.No,QMessageBox.No)** 处理返回值，如果单击Yes按钮,关闭小部件并终止应用程序。 否则我们忽略关闭事件**。** **if reply == QMessageBox.Yes:** ** QCloseEvent.accept()** ** else:** ** QCloseEvent.ignore()** **event.accpet()  ** **窗口关闭** **event.ignore()   ** **不需要做出反应** 将窗口显示到屏幕中间： **def center(self):** ** qr = self.frameGeometry()  #获得窗口** ** cp = QDesktopWidget().availableGeometry().center()  #获得屏幕中心店** ** qr.moveCenter(cp)** ** self.move(qr.topLeft())** 创建标签并且设置位置： **lbll = QLabel('Zetcode',self)** ** lbll.move(15,10)** 一般使用部件名称.move() 来控制部件的位置

**End！** ![](http://47.100.4.8/wp-content/uploads/2018/03/0addfb628535e5ddf06b66a77fc6a7efce1b6226-300x300.jpg) [代码记录（二）](http://47.100.4.8/wp-content/uploads/2018/03/代码记录（二）.rar)