---
title: C++实现直接插入排序、直接选择排序、冒泡排序
url: 1355.html
id: 1355
categories:
  - C&amp;C++
  - 文章页
  - 算法
date: 2018-06-15 00:07:08
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/图片150.png) 这里的排序算法进行处理的对象是通过array来创建的数组： 配合之前的队列来使用。 至于排序算法的思想，我感觉只要对C艹有一定了解得人大概都能看懂，所以这里不做过多的解释。 头文件代码：

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
5\. 
sort.h头文件：
#ifndef SORT\_H\_INCLUDED
#define SORT\_H\_INCLUDED
#include<iostream>
#include<cstdlib>
using namespace std;

enum ErrorType
  {invalidArraySize, memoryAllocationError, indexOutOfRange};
char *errorMsg\[\] =
{
    "Invalid array size", "Memory allocation error",
    "Invalid index: "
};
template <class T>
class Array
{
    private:
        T*  alist;
        int size;
        void Error(ErrorType error,int badIndex=0) const;
    public:
        Array(int sz = 50);
        Array(const Array<T>& A);
        ~Array(void);
        Array<T>& operator= (const Array<T>& rhs);
        T& operator\[\](int i);
        operator T* (void) const;
        int ListSize(void) const;
        void Resize(int sz);
		void InsertionSort();
		void SelectionSort();
        void BubbleSort();
        int SeqSearch(T key);
};
template <class T>
void Array<T>::Error(ErrorType error, int badIndex) const
{
    cerr << errorMsg\[error\];
    if (error == indexOutOfRange)
        cerr << badIndex;
    cerr << endl;
    exit(1);
}
template <class T>
Array<T>::Array(int sz)
{
    if (sz <= 0)
        Error(invalidArraySize);
    size = sz;
    alist = new T\[size\];
    if (alist == NULL)
        Error(memoryAllocationError);
}
template <class T>
Array<T>::~Array(void)
{
    delete \[\] alist;
}
template <class T>
Array<T>::Array(const Array<T>& X)
{
    int n = X.size;
    size = n;
    alist = new T\[n\];
    if (alist == NULL)
        Error(memoryAllocationError);
    T* srcptr = X.alist;
    T* destptr = alist;
    while (n--)
        \*destptr++ = \*srcptr++;
}
template <class T>
Array<T>& Array<T>::operator= (const Array<T>& rhs)
{
    int n = rhs.size;
    if (size != n)
    {
        delete \[\] alist;
        alist = new T\[n\];
        if (alist == NULL)
            Error(memoryAllocationError);
        size = n;
    }
   T* destptr = alist;
   T* srcptr = rhs.alist;
    while (n--)
        \*destptr++ = \*srcptr++;
    return *this;
}
template <class T>
T& Array<T>::operator\[\] (int n)
{
   if (n < 0 || n > size-1)
      Error(indexOutOfRange,n);
   return alist\[n\];
}
template <class T>
Array<T>::operator T* (void) const
{
    return alist;
}
template <class T>
int Array<T>::ListSize(void) const
{
    return size;
}
template <class T>
void Array<T>::Resize(int sz)
{
    if (sz <= 0)
        Error(invalidArraySize);
    if (sz == size)
        return;
    T* newlist = new T\[sz\];
    if (newlist == NULL)
        Error(memoryAllocationError);
    int n = (sz <= size) ? sz : size;
    T* srcptr = alist;
    T* destptr = newlist;
    while (n--)
        \*destptr++ = \*srcptr++;
    delete\[\] alist;
    alist = newlist;
    size = sz;
}
template <class T>
void Array<T>::InsertionSort()
{
	int i, j;
	T   temp;
	for (i = 1; i < size; i++)
	{
		j = i;
		temp = alist\[i\];
		while (j > 0 && temp < alist\[j-1\])
		{
			alist\[j\] = alist\[j-1\];
			j--;
		}
		alist\[j\] = temp;
	}
}
template <class T>
void Array<T>::SelectionSort()
{
	int smallIndex;
	int i, j;
	for (i = 0; i < size-1; i++)
	{
		smallIndex = i;
		for (j = i+1; j < size; j++)
			if (alist\[j\] < alist\[smallIndex\])
				smallIndex = j;
			swap(alist\[i\], alist\[smallIndex\]);
	}
}
template <class T>
void Swap (T &x, T &y)
{
	T temp;
	temp = x;
	x = y;
	y = temp;
}
template <class T>
void Array<T>::BubbleSort()
{
	int i,j;
	int lastExchangeIndex;
	i = size-1;
	while (i > 0)
	{
		lastExchangeIndex = 0;
		for (j = 0; j < i; j++)
			if (alist\[j+1\] < alist\[j\])
			{
				Swap(alist\[j\],alist\[j+1\]);
				lastExchangeIndex = j;
			}
			i = lastExchangeIndex;
	}
}
template <class T>
int Array<T>::SeqSearch(T key)
{
	for(int i=0;i < size;i++)
		if (alist\[i\] == key)
			return i;
	return -1;
}

#endif // SORT\_H\_INCLUDED

代码：

#include <iostream>
#include <cstdlib>
#include <time.h>
#include <windows.h>
#include "Sort.h"
using namespace std;
int main()
{
	Array<int> A(10);
	int i,k;
	int SearchNum;

	cout << "<--------------使用直接插入排序-------------->" <<endl;
	cout << "随机生成10个整数用来array数组" << endl;
	srand(unsigned(time(NULL)));
	for(i=0;i<10;i++)
	{
		A\[i\]=rand()%100;
	}
	cout << "创建的数组为：" << endl;
	for(i=0;i<10;i++)
		cout << A\[i\] << "  ";
    cout<<endl;
    A.InsertionSort();
	cout << "排序后的数组为：" << endl;
	for(i=0;i<10;i++)
		cout << A\[i\] << "  ";
	cout << endl;

	Sleep(700);
	cout << endl<<"<--------------使用直接选择排序-------------->" <<endl;
	cout << "随机生成10个整数用来array数组" << endl;
	srand(unsigned(time(NULL)));
	for(i=0;i<10;i++)
	{
		A\[i\]=rand()%100;
	}
	cout << "创建的数组为：" << endl;
	for(i=0;i<10;i++)
		cout << A\[i\] << "  ";
    cout<<endl;
    A.SelectionSort();
	cout << "排序后的数组为：" << endl;
	for(i=0;i<10;i++)
		cout << A\[i\] << "  ";
	cout << endl;

	Sleep(600);
	cout <<endl<< "<--------------使用冒泡排序-------------->"<<endl ;
	cout << "随机生成10个整数用来array数组" << endl;
	srand(unsigned(time(NULL)));
	for(i=0;i<10;i++)
	{
		A\[i\]=rand()%100;
	}
	cout << "创建的数组为：" << endl;
	for(i=0;i<10;i++)
		cout << A\[i\] << "  ";
    cout<<endl;
    A.BubbleSort();
	cout << "排序后的数组为：" << endl;
	for(i=0;i<10;i++)
		cout << A\[i\] << "  ";
	cout << endl;

	cout << endl<<"对最后创建的数组进行查找数字的操作：";
	cin >> SearchNum;
	k= A.SeqSearch(SearchNum);
	if (k<0)
		cout << "没有找到数字" << SearchNum << endl;
	else
		cout << SearchNum << "的下标为" << k <<endl;
}

结果： ![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180615000636.png)