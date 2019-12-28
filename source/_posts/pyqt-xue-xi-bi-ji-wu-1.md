---
title: PyQt学习笔记（五）
url: 391.html
id: 391
categories:
  - Python模块PyQt5
  - 文章页
date: 2018-03-20 10:46:54
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180308122611.png) [始めましょう！](https://translate.google.cn/#zh-CN/ja/%E6%88%91%E4%BB%AC%E5%BC%80%E5%A7%8B%E5%90%A7)   依旧是学习笔记  咕咕~~ ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180308123017.png)

##### 菜单栏使用以及图标应用

具体形式如上： QAction可以操作菜单栏,工具栏,或自定义键盘快捷键  QIcon可以将图片添加到你想要放置的位置 创立一个QAction对象  QIcon设置图标 **‘****&****名称’** 记住格式 exitAction = QAction(QIcon('qwe.jpeg'),'&Exit',self) 注：顺序不能更改   定义该操作的快捷键 exitAction.setShortcut('Ctrl+Q')   绑定信息 创建一个鼠标指针悬停在该菜单项上时的提示 exitAction.setStatusTip('Exit application')   当我们点击菜单的时候，调用qApp.quit,终止应用程序。 或者按Ctrl+Q exitAction.triggered.connect(qApp.quit)   ![](http://47.100.4.8/wp-content/uploads/2018/03/啊实打实大大学城站下车.png)     另一种设置一个图标的方式： 和上面例子的一样 exitAction = QAction(QIcon('qwe.jpeg'),'&Exit',self) exitAction.setShortcut('Ctrl+Q') exitAction.triggered.connect(qApp.exit) 绑定快捷键  设置退出   创建一个简单的工具栏 toolbar为鼠标放置小提示 self.toolbar = self.addToolBar('Exit') self.toolbar.addAction(exitAction) self.toolbar.addAction 连接事件 self.addToolBar(‘提示内容’)  添加提示内容,鼠标放到上面显示提示内容     QLCDNumber控件用于显示一个LCD数字。 它可以显示几乎任意大小的数字。可以显示十进制、十六进制、八进制或二进制数。很容易使用display()槽连接到数据源，这个槽可以被任何五个参数类型的数据源重载。 ![](http://47.100.4.8/wp-content/uploads/2018/03/啊输出大润发色的.png) [代码记录五](http://47.100.4.8/wp-content/uploads/2018/03/代码记录五.rar) End！ ![](http://47.100.4.8/wp-content/uploads/2018/03/u26562914982410145144fm27gp0-240x300.jpg)