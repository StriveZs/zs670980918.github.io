---
title: Centos部分基础操作指令
url: 173.html
id: 173
categories:
  - Centos
  - 文章页
date: 2018-03-04 14:52:22
tags:
---

  ![](http://47.100.4.8/wp-content/uploads/2018/03/QQ图片20180304144234-300x298.png) 1.连接远程服务器用户名统一为root 密码一般为自己设置的 2.安装解压  yum  install -y zip 3.安装解压 yum  install -y unzip 4.解压文件的命令 unzip 名称.zip  /位置 5.压缩文件的命令 zip 名称.zip /位置 6.进入文件夹 cd /文件夹名称 7.查找文件位置  find / -name 文件名 8.一般运行文件直接输入该文件名称要加上后缀名 9.移动文件的操作 mv 文件名称 /位置 10.删除文件  rm -f 文件名称   （尽量处在文件目录） 11.以root（管理员身份）修改文件权限    chmod -R 777 文件夹的名字 （当前所在的目录下的文件夹，777代表可读可写可操作）