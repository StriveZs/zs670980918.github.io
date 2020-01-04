---
title: C++ memset使用
url: 1600.html
id: 1600
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2019-01-26 18:39:00
tags:
  - memset
  - C/C++
---

memset 函数是内存赋值函数，用来给某一块内存空间进行赋值的。 其原型是：void* memset(void *\_Dst, int  \_Val, size\_t \_Size)   \_Dst是目标起始地址，\_Val是要赋的值，_Size是要赋值的字节数。 例一：使用memset对字符数组进行快速初始化：
```
char num\[12\];
memset(num,'A',12);
for(int i=0;i<12;i++)
   cout<<num\[i\]<<" ";
cout<<endl;
```
![](http://47.100.4.8/wp-content/uploads/2019/01/QQ图片20190126182812.png) 要注意：memset是逐字节拷贝的 例二：使用memset初始化整形数组 首先要注意一个int是4个字节，因此在对长度赋值时要*4 代码：
```
int num1\[12\];
memset(num1,-1,48);
for(int i=0;i<12;i++)
    cout<<num1\[i\]<<" ";
cout<<endl;
```
结果： ![](http://47.100.4.8/wp-content/uploads/2019/01/QQ图片20190126183303.png) 例三：如果没有*4则话会出现如下问题 代码：
```
int num1\[12\];
memset(num1,-1,32);
for(int i=0;i<12;i++)
    cout<<num1\[i\]<<" ";
c`ut<<endl;
```
结果：这里只写了32没有写48 ![](http://47.100.4.8/wp-content/uploads/2019/01/QQ图片20190126183713.png) 总之，在memset使用时要千万小心，在给char以外的数组赋值时，只能初始化为0或者-1。