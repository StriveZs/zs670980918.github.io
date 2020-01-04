---
title: 如何给PyCharm安装第三方库┑(￣Д ￣)┍
url: 311.html
id: 311
categories:
  - Python功能
  - 文章页
date: 2018-03-10 18:33:03
tags:
  - PyCharm
  - whl
  - Python
---

![](http://47.100.4.8/wp-content/uploads/2018/03/f561e48065380cd7687e6295a844ad3459828102-300x300.jpg)  

今天给大家带来的是安装第三方Python库的办法 O(∩_∩)O~~~
-----------------------------------

### 第一种方式：

使用PyCharm自带的setting进行第三方库的安装 首先打开File里面的setting ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180310182202-155x300.png) 然后找到project interpreter  点击+ ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180310182300-300x198.png) 然后搜索你想要的 第三方库名称，点击install  即可安装 如果出现错误 一般情况 是你想要安装的库已经和你的python版本不符合 导致的安装失败。

(。﹏。*) 那么只能采用第二种方法才可以了 咕~~~

 

### 第二种方法：

主要是使用pip进行安装 今天以PythonMagick 为例子 首先先去 [https://www.lfd.uci.edu/~gohlke/pythonlibs/#pythonmagick](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pythonmagick) 下载你想要Python库whl文件   然后最好把它放到磁盘根目录下这里我放的是E:盘 然后使用CMD命令找到你Python 目录中Scripts文件夹 进入之后使用dir 确定pip 在里面 没有的话还需要自己去下载pip安装库 这里pip一般都是自带的 ![](http://47.100.4.8/wp-content/uploads/2018/03/自行车自行车.png) ![](http://47.100.4.8/wp-content/uploads/2018/03/啥东西再擦拭的.png) 然后使用在当前目录下使用pip install 文件目录加上文件名 ![](http://47.100.4.8/wp-content/uploads/2018/03/啊擦三大输入法-300x9.png) 格式为：pip install 文件目录 即可安装成功 要注意的是这里不能图省事 将文件名擅自修改否则会出现 ![](http://47.100.4.8/wp-content/uploads/2018/03/安插撒大声地-300x17.png) 遇到这种情况只需安装原来下载的名称 安装即可

欧欧~  今天就到这里了 如果还要其他问题我也爱莫能助了 ，minna 只能自行去问度娘了  QAQ~ ![](http://47.100.4.8/wp-content/uploads/2018/03/dc3a92315c6034a8e725e5f8c2134954082376a7-1-300x300.jpg)