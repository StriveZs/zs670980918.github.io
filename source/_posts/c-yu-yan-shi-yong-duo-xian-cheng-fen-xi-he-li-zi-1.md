---
title: C语言使用多线程分析和例子
url: 571.html
id: 571
categories:
  - C语言
  - 多线程
date: 2018-04-11 22:25:38
tags:
  - C/C++
  - thread
---

![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180411221012.png) 因为最近在进行操作系统实验，涉及到了C语言多线程的实现，因此就写一片博文来讲一下。同样这个对于C++也适用。 首先要引用pthread.h 头文件。   声明一个线程变量： 格式：pthread\_t 线程名（ps：这里也可以是一个线程组）   建立一个线程： 格式：pthread\_create（） pthread_create([pthread_t](http://baike.baidu.com/view/4591990.htm) \*restrict tidp,const pthread\_attr\_t \*restrict\_attr,void*（\*start\_rtn)(void\*),void *restrict arg) 四个参数： 第一个参数为指向线程[标识符](http://baike.baidu.com/view/390932.htm)的指针。 第二个参数用来设置线程属性。 第三个参数是线程运行函数的起始地址。 最后一个参数是运行函数的参数。   pthread\_join用来等待一个线程的结束。 格式：pthread\_join void *a  这个随意定义的 pthread\_join (你定义的线程名,&a);   线程的终止： pthread\_exit()； 用来终止当前进程。   下面给出一些常用的操作函数： ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180411222056.png) 常用的同步函数： ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180411222125.png)   接下来是应用实例： 我是以生产者消费者问题为实例，这里我是创建了多个生产者和消费者线程，让他们同时发生。 ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180411222254.png)   特别注意在Linux系统下编译可能会出现： ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180411222415.png) 需要 在编译时使用命令： **gcc a.c -o b -lpthread** 这样就可以编译成功了。(*^▽^*) End！