---
title: SQLServerWindows用户登陆转为混合登陆
url: 1414.html
id: 1414
categories:
  - SQLServer
  - 数据库
  - 文章页
date: 2018-07-05 22:20:20
tags:
  - SQLServer
  - Windows
---

![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180621230739.png) **今天来介绍一下SQLServer 如何将Windwos身份验证登陆转为混合验证登陆**。 为什么要进行这个设置呢？在对数据库进行操作时可以通过用户名和密码来连接数据库。 首先你先用Windwos登陆验证登陆 ![](http://47.100.4.8/wp-content/uploads/2018/07/1-2.png) 然后右键服务器点击属性 ![](http://47.100.4.8/wp-content/uploads/2018/07/2.png) 在安全性一栏中将服务器身份验证改为SQL Server和Windwos身份验证模式 ![](http://47.100.4.8/wp-content/uploads/2018/07/3.png) 接下来在安全性登录名你会发现sa上面是有一个红色的叉 ![](http://47.100.4.8/wp-content/uploads/2018/07/4.png) 右键sa属性在状态一栏中将登录名启用 ![](http://47.100.4.8/wp-content/uploads/2018/07/5.png) 然后在常规里面随便设置一个自己能记住的密码。 接下来新建一个查询将如下语句执行 ALTER LOGIN sa ENABLE; GO ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>'; 执行成功之后重新启动一下服务器 ![](http://47.100.4.8/wp-content/uploads/2018/07/6.png) 启动完成后断开连接，重新登录在身份验证一栏中选择SQLServer身份验证，用户名为sa密码为你之前设置的密码。 单击连接即可登陆成功