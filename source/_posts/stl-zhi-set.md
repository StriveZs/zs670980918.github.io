---
title: STL之set
url: 1215.html
id: 1215
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-20 22:54:39
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/图片150.png) 在STL中，set是以红黑树（RB-tree）作为底层数据结构的，hash\_set是以Hash tabl （哈希表）作为底层数据结构的。set可以在时间复杂度为O(logN)情况下插入、删除和查找数据。hash\_set操作的时间复杂度则比较复杂，这取决于哈希函数和哈希表的负载情况。 set关联式容器。set作为一个容器也是用来存储同一数据类型的数据类型，并且能从一个数据集合中取出数据，在set中每个元素的值都唯一，而且系统能根据元素的值自动进行排序。应该注意的是set中数元素的值不能直接被改变。**C++ STL中标准关联容器set, multiset, map, multimap内部采用的就是一种非常高效的平衡检索二叉树：红黑树，也成为RB树**(Red-Black Tree)。RB树的统计性能要好于一般平衡二叉树，所以被STL选择作为了关联容器的内部结构。 set可以在时间复杂度为O(logN)情况下插入、删除和查找数据。 包含在set头文件中 #include<set> 红黑树初步了解介绍请前往链接：[https://blog.csdn.net/v\_july\_v/article/details/6105630](https://blog.csdn.net/v_july_v/article/details/6105630) http://www.cnblogs.com/skywang12345/p/3245399.html   后面我也写一篇博文去介绍   函数 构造函数： set<类型>c  //创建一个空的set或hash\_set hash\_set<类型>c   数据查找： c.find（elem）  //返回存在指向查找的对象或指向c.end（）迭代器 c.count（elem） //存在则返回1否则返回0   数据访问： c.begin（）  //返回指向第一个数据的迭代器 c.end（）  //指向迭代器中的最后一个数据的下一个位置 c.rbegin（）  //返回一个逆向集的第一个数据 c.rend（）  //返回一个逆向集的最后一个数据的下一个位置   插入数据： c.insert（elem）  //插入一个elem，返回pair<iterator,bool> c.insert（pos，elem）  //在pos位置插入一个elem数据，返回迭代器 c.insert（beg，end）  //在\[beg，end\]区间中的数据赋值给c，无返回值   删除数据： c.erase（pos）  //删除pos位置的数据，无返回值 c.earse（elem） //删除elem c.erase（beg,end） //删除\[beg，end\]区间的数据   其他： c.empty（）  //判断容器是否为空 c.max_size（）  //返回容器中最大数据的数量 c.size（）  //返回容器中实际数据的个数 c.swap（c2）  //将c1和c2数据进行交换 代码：

#include<iostream>
#include<set>
#include<cstdlib>
#include<time.h>

using namespace std;

int main()
{
    set<int>a;  //创建一个大小为10容器
    set<int>::iterator pos;
    srand((unsigned)time(NULL));  //利用时间设置随机数种子
    for(int i=0;i<20;i++)
        {
            int t=rand()%100;
            a.insert(t);
        }
    cout<<"set当前数据有："<<a.size()<<"个"<<endl;
    int t=a.count(5);
    cout<<"查找为5的元素："<<(t==1?"存在":"不存在")<<endl; //条件运算表达式语句
    cout<<"随机产生的数据为："<<endl;
    for(pos=a.begin();pos!=a.end();pos++)
        {
            cout<<*pos<<" ";
        }
    cout<<endl;
    a.insert(a.begin(),101); //  在尾部插入一个数据
    for(pos=a.begin();pos!=a.end();pos++)
        {
            cout<<*pos<<" ";
        }
    cout<<endl;
    a.erase(a.begin());  //删除头元素
    for(pos=a.begin();pos!=a.end();pos++)
        {
            cout<<*pos<<" ";
        }
    cout<<endl;
    cout<<"判断set是否为空："<<(a.empty()==0?"不为空":"为空")<<endl;
    return 0;
}

实现： ![](http://47.100.4.8/wp-content/uploads/2018/05/123123-1.png)