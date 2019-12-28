---
title: 给PyCharm安装QtDesigner
url: 1538.html
id: 1538
categories:
  - Python模块PyQt5
  - 文章页
date: 2018-09-28 19:40:34
tags:
---

                                                                              ![](http://47.100.4.8/wp-content/uploads/2018/09/QQ图片20180928191520.png)

**今天介绍给PyCharm安装外部工具QtDesigner**

首先你要给你的PyCharm安装pyqt5 具体安装方法我提供三种 1\. 使用PyCharm自带的安装工具进行安装 在setting中的Project Interpreter中搜索安装pyqt5以及pyqt5-tool ![](http://47.100.4.8/wp-content/uploads/2018/09/QQ图片20180928192246.png) 2.直接使用pip命令进行安装

E:\\python\\Scripts>pip install pyqt5

个人不是很推荐这种方法，由于直接使用pip安装下载速度实在是太慢，而且pyqt5的轮子大概有90mb所以要下很久很久。 3.直接下载轮子，然后使用pip命令安装即可

E:\\python\\Scripts>pip install G:\\PyQt5-5.11.2-5.11.1-cp35.cp36.cp37.cp38-none-win_amd64.whl

至于轮子的下载地址，大家可以自行去这个网站去找https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted  上面几乎有大部分常用的轮子。下载下来之后按照上面的命令安装即可。 接下来是安装QtDesigner 打开PyCharm，选择Settings -> Tools -> External Tools，点击左上角的绿色加号。 ![](http://47.100.4.8/wp-content/uploads/2018/09/QQ图片20180928193120.png) Name填入QtDesigner（方便后续使用，名称无所谓）。Program选择我们安装的PyQt5-tools下面的designer.exe。Working directory则选择我们的工作目录。然后点击OK，则添加了QtDesigner作为PyCharm的外置工具。 按照下图配置： ![](http://47.100.4.8/wp-content/uploads/2018/09/QQ图片20180928193301.png) 然后添加PyUIC（UI转换工具），PyUIC的Program为Python.exe，在Python的安装目录下面的Scripts目录下，Working directory设为$ProjectFileDir$，Parameters则填入如下代码：

-m PyQt5.uic.pyuic  $FileName$ -o $FileNameWithoutExtension$.py

如图： ![](http://47.100.4.8/wp-content/uploads/2018/09/QQ图片20180928193451.png) 最后添加pyrcc用于PyQt5的资源文件转码。具体配置与上述内容相同，Parameters填入：

$FileName$ -o $FileNameWithoutExtension$_rc.py

如图： ![](http://47.100.4.8/wp-content/uploads/2018/09/QQ图片20180928193736.png) **配置完成！** 在PyCharm中启动QtDesigner ![](http://47.100.4.8/wp-content/uploads/2018/09/QQ图片20180928193837.png) 就可以进行QtDesigner的操作了。