---
title: STL之queue
url: 1164.html
id: 1164
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-11 23:22:58
tags:
  - C/C++
  - queue
---

queue单向队列使用 queue单向队列与[栈](http://blog.csdn.net/morewindows/article/details/6950881)有点类似，一个是在同一端存取数据，另一个是在一端存入数据，另一端取出数据。单向队列中的数据是先进先出（First In First Out,FIFO）。在STL中，单向队列也是以别的容器作为底部结构，再将接口改变，使之符合单向队列的特性就可以了。因此实现也是非常方便的。下面就给出单向队列的函数列表和VS2008中单向队列的源代码。单向队列一共6个常用函数（front()、back()、push()、pop()、empty()、size()），与[栈](http://blog.csdn.net/morewindows/article/details/6950881)的常用函数较为相似。 ![](http://47.100.4.8/wp-content/uploads/2018/05/512357486.png) 由于仅需取队首和队尾元素的操作，因此**queue****队列容器并不提供任何类型的迭代器对队列中其他位置处的元素进行访问操作。** **函数** **构造函数：** queue<类型>c   创建一个空间queue queue<类型>c1(c2)  用c2初始化c1   数据访问与增减 c.front（）  返回队列头部数据 c.back（）  返回队列尾部数据 c.push（elem）  在队列尾部增加elem数据 c.pop（）   队列头部数据出队   其他操作 c.empty（）  判断队列是否为空 c.size（）  返回队列中数据的个数 代码：
```
#include<iostream>
#include<queue>

using namespace std;
int main()
{
    //创建队列1
    queue<int>test1;
    cout<<"判断队列test1是否为空："<<test1.empty()<<endl;
    cout<<"得到队列test1元素个数:"<<test1.size()<<endl;
    test1.push(1);
    test1.push(2);
    queue<int>test2(test1);
    //打印队列元素
    int t=test1.size();
    for(int i=0;i<t;i++)
    {
        cout<<test1.front()<<" ";
        test1.pop();
    }
    cout<<endl;
    cout<<test2.back()<<" "<<test2.front()<<endl;
    return 0;
}
```
结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/14741.png)