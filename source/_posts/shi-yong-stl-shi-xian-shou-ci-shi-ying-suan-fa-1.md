---
title: 使用STL实现首次适应算法
url: 1274.html
id: 1274
categories:
  - C&amp;C++
  - 文章页
  - 算法
date: 2018-05-29 11:19:28
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180529111458.png) 介绍： 首次适应算法从空闲[分区表](https://baike.baidu.com/item/%E5%88%86%E5%8C%BA%E8%A1%A8)的第一个表目起查找该表，把最先能够满足要求的空闲区分配给作业，这种方法目的在于减少查找时间。为适应这种算法，空闲分区表(空闲区链)中的空闲分区要按地址由低到高进行排序。该算法优先使用低址部分空闲区，在低址空间造成许多小的空闲区，在高[地址空间](https://baike.baidu.com/item/%E5%9C%B0%E5%9D%80%E7%A9%BA%E9%97%B4)保留大的空闲区。 实现思路： 首先我先定义好一个空间说明表（在这里我定义的说明表已经实现按照地址空间大小排好序），然后根据输入的需求空间值的大小遍历整个空间说明表，当碰到首次合适的空间时，根据输入的大小和占用的大小做差，当差小于一定值时，则该存储整个被占用（这里我设置的值是小于等于1），如果大于1则根据该空间的首地址+输入的大小来划分出来一块空间然后剩余的空间的首地址更新一下，以及剩余空间的长度更新一下即可。需要注意的是在进行删除操作时，要清空所有数据。 代码：

//首次适应算法
bool FF()
{
    flag2=0;
    cout<<"注意当你想要结束的时候输入-1即可结束输入"<<endl;
    cout<<"输入你想要存储内存大小（单位为K）：";
    cin>>k;
    if(k==-1)
    {
        flag1=1;
        return false;
    }
    bool flag=true;
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
        cout<<endl<<"该需要存储的模块在内存中没有找到合适的模块来存储！"<<endl;
        flag2=1;
        return false;
    }
    cout<<endl<<"<--------该模块已经成功存储！-------->"<<endl;
    return true;
}

上面给出的是主要算法，接下来给出一些定义的结构体、初始化函数以及使用到Deque队列：

#include<iostream>
#include<deque>

using namespace std;

#define numUse 100  //定义空闲区说明表最多有十个可用存储空间

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
int q=0; //计数器
void Init()  //初始化
{
    int start\[5\] = {10,25,40,60,90};  //这里事先定义初始地址
    int length\[5\] = {10,10,15,20,25}; //这里事先定义长度
    for(int i=0;i<n;i++)
    {
        mode\[i\].Start = start\[i\];
        mode\[i\].Length = length\[i\];
        mode\[i\].State = 'R';
        Q.push_back(mode\[i\]);
    }
}

最终结果为： ![](http://47.100.4.8/wp-content/uploads/2018/05/123.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/312.png)