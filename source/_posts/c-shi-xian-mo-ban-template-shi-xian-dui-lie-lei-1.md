---
title: C++实现模板（template）实现队列类
url: 1353.html
id: 1353
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-06-13 23:45:30
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/图片150.png)   queue.h头文件 代码：

#ifndef QUEUE_CLASS
#define QUEUE_CLASS
#include <iostream>
#include <cstdlib>
#include "LinkedList.h"

using namespace std;

template <class T>
class Queue
{
    private:
        LinkedList<T> queueList;
    public:
        Queue(void);
        void QInsert(const T& elt);
        T QDelete(void);
        T QFront(void);
        int QLength(void) const;
        int QEmpty(void) const;
        void QClear(void);
};
template <class T>
Queue<T>::Queue(void)
{}
template <class T>
int Queue<T>::QLength(void) const
{
    return queueList.ListSize();
}
template <class T>
int Queue<T>::QEmpty(void) const
{
    return queueList.ListEmpty();
}
template <class T>
void Queue<T>::QClear(void)
{
    queueList.ClearList();
}
template <class T>
void Queue<T>::QInsert(const T& elt)
{
    queueList.InsertRear(elt);
}
template <class T>
T Queue<T>::QDelete(void)
{
    if (queueList.ListEmpty())
    {
        cerr << "Calling QDelete for an empty queue!" << endl;
        exit(1);
    }
    return queueList.DeleteFront();
}
template <class T>
T Queue<T>::QFront(void)
{
    if (queueList.ListEmpty())
    {
        cerr << "Calling QFront for an empty queue!" << endl;
        exit(1);
    }
    queueList.Reset();
    return queueList.Data();
}
#endif

使用：

#include "queue.h"
#include<iostream>

using namespace std;
int main()
{
	Queue<int> A;
	cout<<"输入6个数值用来创建队列:";
	int a=0;
	for(int i=0;i<=5;i++)
	{
	    cin>>a;
		A.QInsert(a);
	}
	cout<<"创建成功！"<<endl;
	cout << "显示队列中的所有元素为：" ;
	while(!A.QEmpty())
	{
		cout << A.QFront() << "   ";
		A.QDelete();
	}
	cout<<endl;
	cout<<"判断队列是否为空："<<(A.QEmpty()==0?"为空":"不为空")<<endl;
	cout << endl;
	cout<<"开始清空队列！"<<endl;
	A.QClear();
	cout<<"队列成功清空！"<<endl;
	return 0;
}