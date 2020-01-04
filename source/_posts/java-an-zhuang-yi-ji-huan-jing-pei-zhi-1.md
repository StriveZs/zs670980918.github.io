---
title: Java安装以及环境配置
url: 1406.html
id: 1406
categories:
  - Java
  - 文章页
date: 2018-07-04 20:34:32
tags:
  - Java
---

![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180704195513.png) **今天介绍一下java的安装以及环境变量的配置**   首先你需要下载一个java的安装程序（大概有200M）这里我就不上传了有点大 大家自行下载：http://www.oracle.com/technetwork/java/javase/downloads/index.html 至于安装方面： ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180704200846.png) 安装目录可以自行选择，其他步骤几乎都下一步了。。。 至于环境配置方面： 首先右键我的电脑，找到高级系统设置 ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180704201242.png) 然后点开环境配置： ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180704201201.png) 然后新建和编辑： ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180704201529.png) 按照如下配置   **1.1 新建变量名：JAVA\_HOME 变量值：C:\\Program Files\\Java\\jdk1.8.0\_102（这是我的jdk安装路径）**  **1.2 编辑变量名：Path 变量值：%JAVA\_HOME%\\bin;%JAVA\_HOME%\\jre\\bin**  **1.3 新建变量名：CLASSPATH 变量值： .;%JAVA\_HOME%\\lib;%JAVA\_HOME%\\lib\\dt.jar;%JAVA_HOME%\\lib\\tools.jar （注意：CLASSPATH变量值前面有个"." 、 在设置变量的末尾时不要加上“;”）** 最后在CMD中输入 java -version若显示出来java的版本，说明配置完成 ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180704203231.png)