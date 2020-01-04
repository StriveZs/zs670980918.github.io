---
title: PyCharm上使用Graphviz
url: 1576.html
id: 1576
categories:
  - Python功能
  - Python知识
  - 文章页
date: 2018-11-08 18:02:05
tags:
  - Python
  - Graphviz
---

**由于最近需要用到Graphviz去画图，所以今天就介绍了自己是如何在pycharm上使用graphviz进行画图的。** **环境配置** 1.首先先去官网上下载安装程序，地址为：http://www.graphviz.org/Download_windows.php ![](http://47.100.4.8/wp-content/uploads/2018/11/QQ图片20181108174954.png) 2.接下来打开你的PyCharm在setting中安装Graphviz的包，或者你可以直接在命令行里面使用pip进行安装，再不行直接下载轮子手动安装吧。 ![](http://47.100.4.8/wp-content/uploads/2018/11/QQ图片20181108175229.png) 3.接下来需要配置一下系统的环境变量（在Path中添加路径） 首先是配置用户的环境变量![](http://47.100.4.8/wp-content/uploads/2018/11/QQ图片20181108175508.png) 然后是修改系统的环境变量![](http://47.100.4.8/wp-content/uploads/2018/11/QQ图片20181108175558.png) 4.配置完成之后重启PyCharm即可使用了呀。   具体使用例子：
```
g = Digraph('test')
g.node(name='a', color='red') #设置点
g.node(name='b', color='red')
g.edge('a','b','c',color='blue')  #c为边的名字 ab分别为起始点和终止点
g.view()
```
运行之后的结果： ![](http://47.100.4.8/wp-content/uploads/2018/11/QQ图片20181108180000.png)