---
title: STL之priority_queue
url: 1189.html
id: 1189
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-14 23:02:22
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180507183124.png) 优先级队列是一个拥有权值概念的单向队列，在这个队列中，所有元素是按优先级排 的。 优先队列容器也是一种从一端入队，另一端出对的队列。不同于一般队列的是，队列中最大的元素总是位于队首位置，因此，元素的出对并非按照先进先出的要求，将最先入队的元素出对，而是将当前队列中的最大元素出对。 C++ STL 优先队列的泛化，底层默认采用 vector 向量容器，使得队列容器的元素可做数组操作，从而应用堆算法找出当前队列最大元素，并将它调整到队首位置，确保最大元素出队。   priority\_queue函数列表 构造函数： priority\_queue<类型>c   //创建一个空的priority\_queue   数据访问与添加和删除: c.top()  //返回队列头部元素 c.push()  //在队列尾部添加元素 c.pop（）  //队列头部数据出队   其他操作： c.empty（）   //判断队列是否为空 c.size（）  //返回队列中数据的个数   有上面函数可以看出其实STL中许多成员函数都是相似的。 同样的priority\_queue队列包含在queue头文件中 代码：

#include<iostream>
#include<queue>
#include<stdlib.h>

using namespace std;

int main()
{
    priority_queue<int>test1; //创建一个优先级队列test1  使用vector作为容器
    priority_queue<int>test2(test1);  //使用test1调用复制析构函数来初始化test2
    cout<<"随机输入五个数据：";
    for(int i=0;i<5;i++)  //向优先级队列添加5个数据
    {
        int t=rand()%20;
        test1.push(t);
        cout<<t<<" ";
    }
    cout<<endl;
    cout<<"当前队列的元素个数："<<test1.size()<<endl;
    cout<<"输出队列数据（通过pop（）方式弹出队列头）：";
    for(int i=0;i<5;i++)
    {
        int t = test1.top();  //先接受值然后在弹出 因为弹出没有返回值所以才先用top（）
        test1.pop();
        cout<<t<<" ";
    }
    cout<<endl;
    cout<<"由上面结果可以看出优先级队列会按照输入数据的大小进行排列！"<<endl;
    return 0;
}

  实现： ![](http://47.100.4.8/wp-content/uploads/2018/05/4324234234.png)