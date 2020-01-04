---
title: STL之deque学习
url: 1144.html
id: 1144
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-08 23:14:08
tags:
  - C/C++
  - STL
  - deque
---

![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180507183124.png)

*   deque双向队列：

deque双向队列是一种双向开口的连续线性空间，可以高效的在头尾两端插入和删除元素，deque在接口上和vector非常相似，下面列出deque的常用成员函数：   构造析构函数： deque<类型>c  创建一个名称为c的空元素类型的deque deque<类型>c(a2)  用c2来初始化c1 deque<类型>c（n）  创建deque，含有n个数据，数据均有基础构造函数初始化 deque<类型>c（n，t）  创建一个含有n个t构成的deque deque<类型>c（start,end）创建一个以（start，end）区间的deque c ~deque<类型>（）   析构函数   赋值函数： 可以直接使用c\[i\]=x 直接进行赋值 c.assign（n，elem）  将n个elem赋值给c   数据访问： c.at（index）   返回索引index所指的数据  如果index大于最大边界 则抛出一个异常 c.front（）  返回deque第一个数据 c.back（）  返回最后一个数据 c.begin（）   返回指向第一个数据的迭代器 注意： deque<int>::iterator pos;  声明一个迭代器变量 使用pos=c.begin（）  来接收返回值不能使用int定义的变量接收否则会报错！ c.end（）同理。 c.end（）   返回指向最后一个数据的下一个位置的迭代器 c.rbegin（）  返回逆向队列的第一个数据 c.rend（）  返回逆向队列指向最后一个数据的下一个位置的迭代器   加入数据： c.push\_back（elem）  在尾部加入一个数据 c.push\_from（elem）  在头部插入一个数据 c.insert（pos，elem）  在pos位置后面插入一个elem  返回新的数据位置 c.insert（pos，n，elem）  在pos位置后面插入n个elem，无返回值   删除数据： c.pop\_back（）  删除最后一个数据 c.pop\_from（）  删除头部数据 c.erase（pos）  删除pos位置的数据，返回下一个数据的位置   其他操作： c.empty（）  判断容器是否为空 c.max_size（）  返回容器中最大数据的数量 c.resize（num）  重新指定队列长度 c.size（）  返回容器实际数据值 c.swap（s）  将c和s的元素互换 swap（c，s）   deque从逻辑上看是连续的内存，本质是由一段段固定大小的连续的空间组成。 ![](http://47.100.4.8/wp-content/uploads/2018/05/1232154.png) 采用一小块连续的内存索引缓存结点，每个缓存结点也是一段连续的空间，可以存储多个数据，当索引内存空间满载时，需要申请一块更大的内存做索引。   使用：
```
#include<iostream>
#include<deque>
#include <cstdio>

using namespace std;

int main()
{
    deque<int> test1(20);  //创建一个数据大小为20的deque
    deque<int>::iterator pos1;  //声明deque test1的迭代器变量为pos

    //初始化
    for(int i=0;i<20;i++)
        test1\[i\]=i;
    cout<<"输出test1初始化数据："<<endl;
    for(int i=0;i<20;i++)
        cout<<test1\[i\]<<" ";
    cout<<endl;

    cout<<"用test1初始化test2的数据："<<endl;
    deque<int> test2(test1);  //用test1初始化test2
    for(int i=0;i<20;i++)
        cout<<test2\[i\]<<" ";
    cout<<endl;

    deque<int> test3(4);
    test3.assign(5,5);
    for(int i=0;i<5;i++)
        cout<<test3\[i\]<<" ";
    cout<<endl;

    cout<<"对test1进行相关操作："<<endl;
    cout<<"test1.front():"<<test1.front()<<endl;
    cout<<"test1.back():"<<test1.back()<<endl;
    //这里要注意的test1.begin（） 需要使用声明迭代器的变量来接收  输出时使用*pos1来输出  pos1为地址
    cout<<"通过使用迭代器进行test1的数据输出："<<endl;
    for(pos1=test1.begin();pos1!=test1.end();pos1++)
        cout<<*pos1<<" ";
    cout<<endl;
    int s=1;
    deque<int>test4;
    cout<<"使用push\_back和push\_front使用："<<endl;
    test4.push_front(1);
    test4.push_back(0);
    cout<<"size（）使用："<<test4.size()<<endl;
    cout<<"pop\_back和pop\_from的使用："<<endl;
    test4.pop_back();
    //test4.pop_front();
    cout<<"当前的大小:"<<test4.size()<<endl;
    cout<<"对test3进行插入操作：";
    test3.insert(test3.begin()+1,3);  //要注意插入操作 插入下标位置使用的是test.begin()+i
    for(pos1=test3.begin();pos1!=test3.end();pos1++)
        cout<<*pos1<<" ";
    cout<<endl;
    cout<<"判断容器test3是否为空："<<test3.empty()<<endl;
    deque<int>test5(10);
    cout<<"输入test5当前的大小:"<<test5.size()<<"  \\n输出最大数据的数量："<<test5.max_size()<<endl;
    return 0;
}
```
结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/4324235.png)