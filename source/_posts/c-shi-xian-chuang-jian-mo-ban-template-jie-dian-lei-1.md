---
title: c++实现创建模板（template）结点类
url: 1337.html
id: 1337
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-06-08 00:04:47
tags:
  - C/C++
  - Template
---

![](http://47.100.4.8/wp-content/uploads/2018/05/4-5.png) Node.h头文件 代码：
```d
#ifndef NODE_LIBRARY
#define NODE_LIBRARY
#include <iostream>
#include <cstdlib>

using namespace std;

template <class T>
class Node
{
    private:
        Node<T> *next;
    public:
        T data;
        Node (const T& item, Node<T>* ptrnext = NULL);
        void InsertAfter(Node<T> *p);
        Node<T> *DeleteAfter(void);
        Node<T> *NextNode(void) const;
};
template <class T>
Node<T>::Node(const T& item, Node<T>* ptrnext) :data(item), next(ptrnext){}

template <class T>
Node<T> *Node<T>::NextNode(void) const
{
    return next;
}

template <class T>
void Node<T>::InsertAfter(Node<T> *p)
{
    p->next = next;
    next = p;
}

template <class T>
Node<T> *Node<T>::DeleteAfter(void)
{
Node<T> *tempPtr = next;
    if (next == NULL)
        return NULL;
    next = tempPtr->next;
    return tempPtr;
}

template <class T>
Node<T> \*GetNode(const T& item, Node<T> \*nextPtr = NULL)
{
    Node<T>  *newNode;
        newNode = new Node<T>(item, nextPtr);
    if (newNode == NULL)
    {
        cerr << "Memory allocation failure!" << endl;
        exit(1);
    }
    return newNode;
}

enum AppendNewline {noNewline,addNewline};
template <class T>
void PrintList(Node<T> *head, AppendNewline addnl = noNewline)
{
    Node<T> *currPtr = head;
    while(currPtr != NULL)
    {
        if(addnl == addNewline)
            cout << currPtr->data << endl;
        else
            cout << currPtr->data << "  ";
        currPtr = currPtr->NextNode();
    }
}

template <class T>
int Find(Node<T> \*head, T& item, Node<T>\* &prevPtr)
{
	Node<T> *currPtr = head;
	prevPtr = NULL;
	while(currPtr != NULL)
	{
	    if (currPtr->data == item)
            return 1;
        prevPtr = currPtr;
        currPtr = currPtr->NextNode();
	}
	return 0;
}

template <class T>
void InsertFront(Node<T>* & head, T item)
{
       head = GetNode(item,head);
}

template <class T>
void InsertRear(Node<T>* & head, const T& item)
{
    Node<T>  \*newNode, \*currPtr = head;
	    if (currPtr == NULL)
            InsertFront(head,item);
    else
    {
        while(currPtr->NextNode() != NULL)
            currPtr = currPtr->NextNode();
        newNode = GetNode(item);
        currPtr->InsertAfter(newNode);
    }
}

template <class T>
void DeleteFront(Node<T>* & head)
{
    Node<T> *p = head;
    if (head != NULL)
    {
        head = head->NextNode();
        delete p;
    }
}

template <class T>
void Delete (Node<T>* & head, T key)
{
    Node<T>  \*currPtr = head, \*prevPtr = NULL;
    if (currPtr == NULL)
        return;
    while (currPtr != NULL && currPtr->data != key)
        {
            prevPtr = currPtr;
            currPtr = currPtr->NextNode();
            }
    if (currPtr != NULL)
        {
            if(prevPtr == NULL)
                head = head->NextNode();
            else
                prevPtr->DeleteAfter();
            delete currPtr;
        }
}

template <class T>
void InsertOrder(Node<T>* & head, T item)
{
    Node<T> \*currPtr, \*prevPtr, *newNode;
    prevPtr = NULL;
    currPtr = head;
    while (currPtr != NULL)
    {
		if (item < currPtr->data)
	      break;
        prevPtr = currPtr;
        currPtr = currPtr->NextNode();
    }
    if (prevPtr == NULL)
        InsertFront(head,item);
    else
    {
        newNode = GetNode(item);
        prevPtr->InsertAfter(newNode);
    }
}

template <class T>
void ClearList(Node<T> * &head)
{
    Node<T> \*currPtr, \*nextPtr;
    currPtr = head;
    while(currPtr != NULL)
    {
        nextPtr = currPtr->NextNode();
        delete currPtr;
        currPtr = nextPtr;
    }
    head = NULL;
}
#endif

使用： 代码：

#include <iostream>
#include "Node.h"

using namespace std;
int main()
{
     Node<int> \*head = NULL, \*prevPtr, *delPtr;
    int i, key, item;
    cout<<"请输入十个数：";
    for (i=0;i < 10;i++)
	{
	    cin>>item;
           InsertRear(head, item);
	}
      cout << "创建的结点表为: ";
    PrintList(head,noNewline);
    cout << endl;
       cout << "请输入你想要删除的一个整数: ";
    cin >> key;
    prevPtr = head;
    while (Find(head,key,prevPtr) != 0)
	{
	  if(prevPtr == NULL)
         head = head->NextNode();
      else
              delPtr=prevPtr->DeleteAfter();
      delete delPtr;
	}
       cout << "删除后的结果为: ";
    PrintList(head,noNewline);
    cout << endl;
    cout<<"查找一个结点是否存在于结点表中(请输入数值)：";
    int a,t=0;
    cin>>a;
    t=Find(head,a,prevPtr);
    cout<<"结果为："<<(t==1?"存在":"不存在")<<endl;
    cout<<"在表头插入一个数据（输入数值）:";
    cin>>a;
    InsertFront(head,a);
    cout<<"插入之后的表为：";
    PrintList(head,noNewline);
    cout<<endl<<"开始清除结点表！"<<endl;
    ClearList(head);
    cout<<"成功清除结点表"<<endl;
}
```
结果： ![](http://47.100.4.8/wp-content/uploads/2018/06/1235.png)