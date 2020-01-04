---
title: PyQt5 学习笔记（一）
url: 263.html
id: 263
categories:
  - Python模块PyQt5
  - 文章页
date: 2018-03-08 12:31:47
tags:
  - Python
  - PyQt5
---

![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180308122611.png)

### PyQt简介：

### **PyQt**实现了一个Python模块集。它有超过300类，将近6000个函数和方法。它是一个多平台的工具包，可以运行在所有主要操作系统上，包括UNIX，Windows和Mac。 **PyQt采用双许可证，开发人员可以选择GPL和商业许可。在此之前，GPL的版本只能用在Unix上，从PyQt的版本4开始，GPL许可证可用于所有支持的平台。**

闲话讲了一堆接下来就是笔记了  不慌 23333

～(￣▽￣～)(～￣▽￣)～

![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180308123017.png)   app = QApplication(sys.argv)  pyqt对象要在这个应用程序对象上建立 w = QWidget()  创建一个pyqt5 窗口 w.resize()  设置窗口大小 w.move 将窗口移动到指定位置 w.setWindowTitle(‘’)设置窗口标题 w.show（） 窗口显示 sys.exit(app.exec_())  系统exit（）方法确保程序干净的退出 必须有才能显示窗口否则会闪退 窗口界面常用格式： **import sys** ** from PyQt5.QtWidgets import QApplication,QWidget** ** from PyQt5.QtGui import QIcon** ** class Example(QWidget):** **     def \_\_init\_\_(self):** **         super().\_\_init\_\_()** **         self.initUI()  #界面绘制交给InitUi方法** **def initUI(self):self.show()if \_\_name\_\_ == '\_\_main\_\_':** **     app = QApplication(sys.argv)** **     ex = Example()** **     sys.exit(app.exec_())** 相关语句解释： 设置窗口位置 **self.setGeometry(300,300,300,220)  #设置窗口的位置和大小** 设置窗口标题 **self.setWindowTitle('Icon')  #设置窗口标题** 设置窗口的图标 **self.setWindowIcon(QIcon('qwe.jpeg'))** 创建一个按钮： **btn = QPushButton('Button',self)** 设置按钮的尺寸: **btn.resize(btn.sizeHint())** **btn.sizeHint（） 为显示默认尺寸** End！ ![](http://47.100.4.8/wp-content/uploads/2018/03/8c08513e6709c93d3db5cd8f963df8dcd1005426-300x300.jpg) **[代码记录（一）](http://47.100.4.8/wp-content/uploads/2018/03/代码记录（一）.rar)**