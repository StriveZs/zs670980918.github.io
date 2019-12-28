---
title: STL之Stack学习
url: 1148.html
id: 1148
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-09 22:41:26
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180507183124.png) 栈是一种容器适配器，特别为后入先出而设计的一种（LIFO ），那种数据被插入，然后再容器末端取出 栈实现了容器适配器，这是用了一个封装了的类作为他的特定容器，提供了一组成员函数去访问他的元素，元素从特定的容器，也就是堆栈的头取出。 遵循先进先出的原则。栈口只有一个，允许新增元素（只能在栈顶上增加）、移除元素（只能一处栈顶元素）、取得栈顶元素等操作。在STL，栈是以别的容器作为底部结构，再将接口改变，使之符合栈的特性就可以了。   栈的相关函数 构造函数： stack<Elem>c  创建一个空的stack stack<Elem>c1(c2)  用c2初始化c1   数据增减： c.top（）  返回栈顶元素 c.push（elem） 在栈顶增加elem数据 c.pop（）  弹出栈顶元素   其他操作： c.empty（）   判断栈是否为空 c.size（）  返回栈中数据的个数 代码：

#include<iostream>
#include<stack>

using namespace std;

int main()
{
    stack<int>s;  //创建一个栈
    cout<<"创建栈成功！"<<endl;
    cout<<"当前栈的数据个数："<<s.size()<<endl;\
    cout<<"添加三个元素在之后："<<endl;
    s.push(1);  //向栈中添加元素
    s.push(2);
    s.push(3);
    cout<<"当前栈的数据个数："<<s.size()<<endl;
    cout<<"返回栈顶元素："<<s.top()<<endl;
    cout<<"弹出栈顶元素之前的数据个数："<<s.size()<<endl;
    s.pop();
    cout<<"弹出栈顶元素之后的数据个数："<<s.size()<<endl;
    cout<<"判断栈是否为空:"<<s.empty()<<endl;
    return 0;
}

  结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/12335424.png)