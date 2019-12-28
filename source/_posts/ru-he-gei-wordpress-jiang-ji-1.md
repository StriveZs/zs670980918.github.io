---
title: '如何给WordPress降级(￣_,￣ )'
url: 228.html
id: 228
categories:
  - Website building
  - 文章页
date: 2018-03-05 23:17:27
tags:
---

手动降级的方法： **1.下载对应的 WordPress 旧版本** 下载你目前使用的语言版本（即如果你使用官方中文版，就下载官方中文的旧版本，如果是英文原版，就下载英文旧版本） WordPress官方中文版各版本下载地址：https://cn.wordpress.org/releases/#older WordPress官方英文版各版本下载地址：http://wordpress.org/download/release-archive/ **2.更换 WordPress 程序文件** (1) 解压下载的旧版本，然后删除解压后的 wp-content 文件夹，使用 FTP 上传其他文件覆盖原来的文件。 注意：主机空间的 wp-content 文件夹里面有主题和插件等文件，根目录的 wp-config.php 里面是WordPress的配置文件，切记不要覆盖这些文件！！ (2) 访问 http://你的网址/wp-admin/ ，稍等会出现一个页面，提示你需要更新数据库，点击更新，就可以恢复到旧版本的wordpress。 ![](http://47.100.4.8/wp-content/uploads/2018/03/371122f3d7ca7bcb55c99a56b7096b63f624a83c-300x300.jpg)是不是感觉一点也不会……其实我也不会233333┗|｀O′|┛ 嗷~~   在线降级方法，其实就是一个添加一个插件就能解决的事情，惊不惊喜意不意外，只需在![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180305230719.png) 搜索 WP Downgrade ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180305230707-300x121.png) 在设置里打开插件会有如下界面： ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180305231530-300x98.png) 选择自己想要得版本点击红色按钮即可2333

o(*≧▽≦)ツ┏━┓  是不是很简单！ ![](http://47.100.4.8/wp-content/uploads/2018/03/09fa513d269759ee9acfdca1b1fb43166d22df39.gif)