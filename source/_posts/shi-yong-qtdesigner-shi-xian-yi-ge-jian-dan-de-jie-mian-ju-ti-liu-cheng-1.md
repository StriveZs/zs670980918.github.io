---
title: 使用QtDesigner实现一个简单的界面（具体流程）
url: 1553.html
id: 1553
categories:
  - Python模块PyQt5
  - 文章页
date: 2018-10-08 22:01:55
tags:
  - Python
  - PtQt5
  - QtDesigner
---

![](http://47.100.4.8/wp-content/uploads/2018/10/QQ图片20181008213410.png) 之前教大家如何给PyCharm安装QtDesigner，今天我就说一下使用它的具体流程，（\\(^o^)/~） 首先打开主界面，如弹出如下界面 ![](http://47.100.4.8/wp-content/uploads/2018/10/QQ图片20181008214102.png) 正常情况下我们应该选择MainWindow 作为主要窗口，至于其他的Dialog窗口等我们在以后的界面跳转时会介绍。 单击Create后会出现如下操作界面： ![](http://47.100.4.8/wp-content/uploads/2018/10/QQ图片20181008214510.png) 以上大概介绍了一些常用的控件，由于我也是初学者所以好多控件也不是很了解，希望大家见谅。 首先应该将一个frame框架 拖入主窗口，目的是能够将一些小控件放到上面在，然后就可以对整个frame进行，而不需要仅仅对一个控件进行操作，而且frame在以后的多界面切换也有很大的作用。 然后尝试在上面放置一些pushButton、Label和lineEdit 修改Label的字体颜色的等属性： ![](http://47.100.4.8/wp-content/uploads/2018/10/QQ图片20181008215028.png) 点击change rich text之后会跳出一下界面 ![](http://47.100.4.8/wp-content/uploads/2018/10/QQ图片20181008215143.png) 然后大家就可以修改相关字体的一些信息了。 下面是我快速创建的一个小界面： ![](http://47.100.4.8/wp-content/uploads/2018/10/QQ图片20181008215301.png) 然后将该文件保存，并且将该文件用PyCharm打开，会得到如下.xml文件 ![](http://47.100.4.8/wp-content/uploads/2018/10/QQ图片20181008215444.png) 然后使用之前添加的PyUIC来将该.xml文件转换为.py文件 ![](http://47.100.4.8/wp-content/uploads/2018/10/QQ图片20181008215545.png) 就会生成如下文件： ![](http://47.100.4.8/wp-content/uploads/2018/10/QQ图片20181008215639.png) 运行： 首先创建一个文件并且import该之前生成的UI文件 然后书写如下代码即可调用该UI文件：
```
from test import *
import sys
from PyQt5.QtWidgets import QApplication, QMainWindow

class testWindow(QMainWindow,Ui_MainWindow):
    def \_\_init\_\_(self,parent=None):
        super(testWindow, self).\_\_init\_\_(parent)
        self.setupUi(self)

if \_\_name\_\_ == '\_\_main\_\_':
    app = QApplication(sys.argv)
    myWin = testWindow()
    myWin.show()
    sys.exit(app.exec_())
```
运行结果： ![](http://47.100.4.8/wp-content/uploads/2018/10/QQ图片20181008215944.png)