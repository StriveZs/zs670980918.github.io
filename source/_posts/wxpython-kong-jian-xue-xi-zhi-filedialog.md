---
title: Wxpython控件学习之FileDialog
url: 466.html
id: 466
categories:
  - WxPython
  - 文章页
date: 2018-03-29 12:48:53
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/03/d0c8a786c9177f3e3d1cab2870cf3bc79f3d56ee.png)

### wxpython也是PythonGUI开发所使用到的一个第三方库，它比PyQt和tkinter 更加的方便适用于小型图形界面的开发。

安装方面： 如果没有安装wxpython的朋友这里有下载地址：https://www.wxpython.org/ 也可以在命令提示符界面输入 pip install wxpython 来进行安装 同样如果你使用PyCharm 那么就可以在setting 里面直接安装 比较方便。   我为什么会分享关于FileDialog相关方面的东西？ 是因为之前我在写一个小程序的时候不会使用文件保存对话框，于是就查了不少的资料，在CSDN上找了相关方面的知识，于是就总结了一下。   wx.FileDialog 允许用户从系统的文件中选择一个或者多个文件。支持通配符，可以让用户选择关心的文件。例如："BMP files (*.bmp)|*.bmp|GIF files (*.gif)|*.gif"只会显示和选择图片后缀类型是bmp 和gif。 样文件的类型可以自定义。   这里是调用windows系统提供的文件对话进行使用 Window Styles

wx.FD_OPEN

单个文件选择对话框

wx.FD_SAVE

文件保存对话框

wx.FD\_OVERWRITE\_PROMPT

只对于保存对话框有效，当覆盖文件的时候，会弹出提醒对话框

wx.FD_MULTIPLE

只对于打开对话框有效，支持多选

wx.FD\_CHANGE\_DIR

改变当前工作目录为用户选择的文件夹

  方法集： ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180329124409.png)   如果图片不清楚这里有图片的下载地址：[方法集](http://47.100.4.8/wp-content/uploads/2018/03/方法集.rar)