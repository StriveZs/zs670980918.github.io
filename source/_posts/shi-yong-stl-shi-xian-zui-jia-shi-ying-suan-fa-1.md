---
title: 使用STL实现最佳适应算法
url: 1279.html
id: 1279
categories:
  - C&amp;C++
  - 文章页
  - 算法
date: 2018-05-30 13:04:01
tags:
  - C/C++
  - STL
  - 最佳适应算法
---

![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180529111458.png) 介绍： 它从全部空闲区中找出能满足作业要求的、且大小最小的空闲分区，这种方法能使碎片尽量小。为适应此算法，空闲[分区表](https://baike.baidu.com/item/%E5%88%86%E5%8C%BA%E8%A1%A8)（空闲区链）中的空闲分区要按从小到大进行排序，自表头开始查找到第一个满足要求的自由分区分配。该算法保留大的空闲区，但造成许多小的空闲区。 思想： 首先我先定义好一个空间说明表，然后根据空间长度的大小**从小到大进行排序**，接下来输入需求空间值大小，根据输入的需求空间值的大小遍历整个空间说明表，**由于已经事先对空间说名表排好序**所以当碰到合适的空间时，根据输入的大小和占用的大小做差，当差小于一定值时，则该存储整个被占用（这里我设置的值是小于等于1），如果大于1则根据该空间的首地址+输入的大小来划分出来一块空间然后剩余的空间的首地址更新一下，以及剩余空间的长度更新一下即可。需要注意的是在进行删除操作时，要清空所有数据。   主要算法代码：
```
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
数据结构、初始化函数以及一些数据：
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
```
结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/123123-2.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/23242424.png)