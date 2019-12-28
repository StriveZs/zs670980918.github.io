---
title: C++实现模板（template）链表类
url: 1346.html
id: 1346
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-06-09 22:58:56
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180609225518.png) 链表相信都很熟悉了就不过多的介绍，如果需要自行翻阅数据结构。这里面使用到了之前结点类 创建LinkedList.h头文件 代码：

#ifndef LINKEDLIST_CLASS
#define LINKEDLIST_CLASS
#include <iostream>
#include <cstdlib>
#include "Node.h"

using namespace std;

template <class T>
class LinkedList
{
   private:
      Node<T> \*front, \*rear;
      Node<T> \*prevPtr, \*currPtr;
      int size;
      int position;
      Node<T> \*GetNode(const T& item,Node<T> \*ptrNext=NULL);
      void FreeNode(Node<T> *p);
      void CopyList(const LinkedList<T>& L);
   public:
      LinkedList(void);
      LinkedList(const LinkedList<T>& L);
      ~LinkedList(void);
      LinkedList<T>& operator= (const LinkedList<T>& L);
      int ListSize(void) const;
      int ListEmpty(void) const;
      void Reset(int pos = 0);
      void Next(void);
      int EndOfList(void) const;
      int CurrentPosition(void) const;
      void InsertFront(const T& item);
      void InsertRear(const T& item);
      void InsertAt(const T& item);
      void InsertAfter(const T& item);
           T DeleteFront(void);
      void DeleteAt(void);
            T& Data(void);
      void ClearList(void);
};
template <class T>
Node<T> *LinkedList<T>::GetNode(const T& item,
                      Node<T>* ptrNext)
{
   Node<T> *p;
   p = new Node<T>(item,ptrNext);
   if (p == NULL)
   {
      cout << "Memory allocation failure!\\n";
      exit(1);
   }
   return p;
}
template <class T>
void LinkedList<T>::FreeNode(Node<T> *p)
{
   delete p;
}
template <class T>
void LinkedList<T>::CopyList(const LinkedList<T>& L)
{
   Node<T> *p = L.front;
   int pos;
   while (p != NULL)
   {
      InsertRear(p->data);
      p = p->NextNode();
   }
    if (position == -1)
     return;
     prevPtr = NULL;
   currPtr = front;
   for (pos = 0; pos != position; pos++)
   {
      prevPtr = currPtr;
      currPtr = currPtr->NextNode();
   }
}
template <class T>
LinkedList<T>::LinkedList(void): front(NULL), rear(NULL),
      prevPtr(NULL),currPtr(NULL), size(0), position(-1)
{}
template <class T>
LinkedList<T>::LinkedList(const LinkedList<T>& L)
{
   front = rear = NULL;
   prevPtr = currPtr = NULL;
   size = 0;
   position = -1;
   CopyList(L);
}
template <class T>
void LinkedList<T>::ClearList(void)
{
   Node<T> \*currPosition, \*nextPosition;
   currPosition = front;
   while(currPosition != NULL)
   {
	  nextPosition = currPosition->NextNode();
      FreeNode(currPosition);
      currPosition = nextPosition;
   }
   front = rear = NULL;
   prevPtr = currPtr = NULL;
   size = 0;
   position = -1;
}
template <class T>
LinkedList<T>::~LinkedList(void)
{
    ClearList();
}
template <class T>
LinkedList<T>& LinkedList<T>::operator=(const LinkedList<T>& L)
{
   if (this == &L)
      return *this;
   ClearList();
   CopyList(L);
   return *this;
}
template <class T>
int LinkedList<T>::ListSize(void) const
{
   return size;
}
template <class T>
int LinkedList<T>::ListEmpty(void) const
{
   return size==0;
}
template <class T>
void LinkedList<T>::Next(void)
{
   if (currPtr != NULL)
   {
      prevPtr = currPtr;
      currPtr = currPtr->NextNode();
      position++;
   }
}
template <class T>
int LinkedList<T>::EndOfList(void) const
{
   return currPtr == NULL;
}
template <class T>
int LinkedList<T>::CurrentPosition(void) const
{
   return position;
}
template <class T>
void LinkedList<T>::Reset(int pos)
{
   int startPos;
    if (front == NULL)
      return;
   if (pos < 0 || pos > size-1)
   {
      cerr << "Reset: Invalid list position: " << pos << endl;
      return;
   }
   if(pos == 0)
   {
      prevPtr = NULL;
      currPtr = front;
      position = 0;
   }
   else
     {
       currPtr = front->NextNode();
       prevPtr = front;
       startPos = 1;
    for(position=startPos; position != pos; position++)
	   {
	       prevPtr = currPtr;
	       currPtr = currPtr->NextNode();
      }
   }
}
template <class T>
T& LinkedList<T>::Data(void)
{
    if (size == 0 || currPtr == NULL)
        {
            cerr << "Data: invalid reference!" << endl;
            exit(1);
        }
    return currPtr->data;
}
template <class T>
void LinkedList<T>::InsertFront(const T& item)
{
    if (front != NULL)
      Reset();
    InsertAt(item);
}
template <class T>
void LinkedList<T>::InsertRear(const T& item)
{
   Node<T> *newNode;
   prevPtr = rear;
   newNode = GetNode(item);
   if (rear == NULL)
      front = rear = newNode;
   else
   {
      rear->InsertAfter(newNode);
      rear = newNode;
   }
   currPtr = rear;
   position = size;
   size++;
}
template <class T>
void LinkedList<T>::InsertAt(const T& item)
{
   Node<T> *newNode;
   if (prevPtr == NULL)
   {
      newNode = GetNode(item,front);
      front = newNode;
   }
   else
   {
      newNode = GetNode(item);
      prevPtr->InsertAfter(newNode);
   }
   if (prevPtr == rear)
   {
      rear = newNode;
      position = size;
   }
     currPtr = newNode;
   size++;
}
template <class T>
void LinkedList<T>::InsertAfter(const T& item)
{
   Node<T> *p;
   p = GetNode(item);
   if (front == NULL)
   {
      front = currPtr = rear = p;
      position = 0;
   }
   else
   {
      if (currPtr == NULL)
      currPtr = prevPtr;
      currPtr->InsertAfter(p);
      if (currPtr == rear)
      {
        rear = p;
        position = size;
      }
      else
       position++;
      prevPtr = currPtr;
      currPtr = p;
   }
   size++;
}
template <class T>
T LinkedList<T>::DeleteFront(void)
{
   T item;
   Reset();
   if (front == NULL)
   {
      cerr << "Invalid deletion!" << endl;
      exit(1);
   }
   item = currPtr->data;
   DeleteAt();
   return item;
}
template <class T>
void LinkedList<T>::DeleteAt(void)
{
   Node<T> *p;
   if (currPtr == NULL)
   {
      cerr << "Invalid deletion!" << endl;
      exit(1);
   }
     if (prevPtr == NULL)
   {
      p = front;
      front = front->NextNode();
   }
   else
    p = prevPtr->DeleteAfter();
   if (p == rear)
   {
      rear = prevPtr;
      position--;
   }
   currPtr = p->NextNode();
   FreeNode(p);
   size--;
}
#endif

使用： 代码：

#include<iostream>
#include "LinkedList.h"
using namespace std;

int main()
{
	LinkedList<int> A, B;
	int a=0;
	cout<<"输入4个数用于创建链表A：";
	for(int i=0;i<4;i++)
	{
	    cin>>a;
		A.InsertRear(a);
	}
    cout<<"输入3个数用于创建链表A：";
	for(int i=0;i<3;i++)
	{
	    cin>>a;
		B.InsertRear(a);
	}
	A.Reset();
    B.Reset();
	cout << "将B中的元素复制到链表A的尾部……" << endl;
	B.Reset();
	while(!B.EndOfList())
	{
		A.InsertRear(B.Data());
		B.Next();
	}
	A.Reset();
	cout << "合并之后，链表A的元素为：" ;
	while(!A.EndOfList())
	{
		cout << A.Data() << "   ";
		A.Next();
	}
	cout << endl;
}

结果： ![](http://47.100.4.8/wp-content/uploads/2018/06/15613.png)