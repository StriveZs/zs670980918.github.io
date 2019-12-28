---
title: 给MatLab安装遗传算法工具箱
url: 1443.html
id: 1443
categories:
  - MatLab
  - 文章页
date: 2018-07-11 16:41:19
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180706191552.png)

**今天介绍一下如何给MatLab安装遗传算法工具箱（gatbx）**

之前参考过网上的许多办法，总结了一下，因为写的对我的MatLab版本都不太合适，每个都有要调整的地方（ps：这也许就我是这样吧）总之也是给matlab新版的朋友提供一个方法吧。 **首先先去官网下载工具箱** 之前看好多人在CSDN上上传该工具箱，都要5到10个C币，这也太黑了，官网上明明免费好不？ 下面是链接：http://codem.group.shef.ac.uk/index.php/ga-toolbox **文件名批量修改** 下载完解压完文件之后会看到一些文件如下： ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180711162859.png) 这些后缀为.M的M文件都需要改为.m文件，否则会报错的。 注意：这里不能直接修改 首先创建一个txt文件，将**ren *.M *.jpg**写入文件中，然后将txt文件修改为.bat文件， 运行之后再创建一个txt文件将**ren *.jpg *.m**写入文件中，然后将txt文件修改为.bat文件。 运行结束之后会发现所有.M的文件后缀都改为了.m。这样对文件的修改就ok了！ ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180711163515.png) **安装工具箱** 将解压出来的两个文件放到../MatLab/toolbox文件目录下 ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180711163429.png) 然后打开MatLab在命令行输入**pathtool**，然后点击添加文件夹 ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180711163744.png) 将需要安装的工具箱所在文件夹选择即可。 **Finally** 测试一下：在命令行中输入**v = ver('gatbx')'** 如果显示关于工具箱的相关信息则证明你安装成功了。 ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180711163918.png)   End！