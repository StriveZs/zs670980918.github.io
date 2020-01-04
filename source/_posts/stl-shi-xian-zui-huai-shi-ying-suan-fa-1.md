---
title: STL实现最坏适应算法
url: 1289.html
id: 1289
categories:
  - C&amp;C++
  - 文章页
  - 算法
date: 2018-06-01 19:01:46
tags:
  - C/C++
  - 最坏适应算法
  - STL
---

![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180529111458.png) 与最佳适应算法相反，最坏适应分配算法要扫描整个空闲分区或链表，总是挑选一个最大的空闲分区分割给作业使用。 算法代码：
```
//最坏适应算法
int k=0;  //全局变量k 以便判断结束条件
int flag1=0;
int flag2=0;
bool BF()
{
    cout<<"注意当你想要结束的时候输入-1即可结束输入"<<endl;
    cout<<"输入你想要存储内存大小（单位为K）：";
    flag2=0;
    cin>>k;
    bool flag=true;
    if(k==-1)
    {
        flag1=1;
        return false;
    }
    for(pos=Q.begin();pos!=Q.end();pos++)
    {
        if((*pos).Length>=k)
        {
            if(((*pos).Length-k)<=1)  //这里设置如何存储内存后剩余空间小于等于1则将状态改为已分配
            {
                (*pos).State='F';
                cout<<endl;
                cout<<"如下模块已经被分配："<<endl;
                cout<<(\*pos).Start<<"K         "<<(\*pos).Length<<"K       ";
                if(((*pos).State)=='F')
                    cout<<"已分配"<<endl;
                for(int i=0;i<n;i++)
                    if(mode\[i\].Start == (*pos).Start)
                    {
                        jilu\[x\]=i+1;
                        break;
                    }
                Q.erase(pos);
            }
            else
            {
                (*pos).Start += k;
                (*pos).Length -=k;
            }
            flag=false;
            break;
        }
    }
    if(flag == true)
    {
        cout<<"该需要存储的模块在内存中没有找到合适的模块来存储！"<<endl;
        flag2=1;
        return false;
    }
    cout<<"该模块已经成功存储！"<<endl;
    return true;
}
```
使用到的数据结构、相关函数以及全局变量
```
#include<iostream>
#include<deque>

using namespace std;

#define numUse 10  //定义空闲区说明表最多有十个可用存储空间

struct Mode{  //定义空闲区说明表
    int Start;  //起始地址
    int Length;  //长度
    char State;  //状态 R为未分配 F为以分配
}mode\[numUse\];

deque<Mode> Q;  //创建一个空的deque队列用来存储可能空闲空间
deque<Mode>::iterator pos;  //创建迭代器
int jilu\[numUse\];  //记录已经分类的模块号
int x=0;  //记录数组的下标

int n=5; //这里定义五个可用空间
int q=0;
void Init()  //初始化
{
    int start\[5\] = {10,25,40,60,90};  //这里事先定义初始地址
    int length\[5\] = {10,3,15,20,25}; //这里事先定义长度
    for(int i=0;i<n;i++)
    {
        mode\[i\].Start = start\[i\];
        mode\[i\].Length = length\[i\];
        mode\[i\].State = 'R';
        Q.push_back(mode\[i\]);
    }
}
//对空间说明表按照长度排序
void WFModeSort()
{
    deque<Mode>::iterator pos1;  //创建pos1迭代器以便于排序时使用
    for(pos=Q.begin();pos!=Q.end();pos++)
        for(pos1=pos+1;pos1!=Q.end();pos1++)
           if((\*pos).Length<(\*pos1).Length)
              {
                  swap(\*pos1,\*pos);
              }
}
```
结果： ![](http://47.100.4.8/wp-content/uploads/2018/06/自行车自行车.png) ![](http://47.100.4.8/wp-content/uploads/2018/06/爱上大声地阿萨德.png)