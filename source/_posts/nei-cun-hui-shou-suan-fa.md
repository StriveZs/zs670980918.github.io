---
title: 内存回收算法
url: 1293.html
id: 1293
categories:
  - C&amp;C++
  - 文章页
  - 算法
date: 2018-06-02 21:56:18
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180529111458.png) **内存回收算法**： 首先是输入你需要归还空间的地址start以及长度length，然后计算出空间的释放区下部地址len，然后循环遍历整个空间说明表，分为以下四种情况：

*   释放区下部邻接空间区
*   释放区上部邻接空闲区
*   释放区上下部都邻接空闲区
*   释放区上下部均不邻接空闲区

操作： 对于情况①，更新空间说明表最后一个元素的所有数据即可。 对于情况②，更新空间说明表第一个元素所有数据即可。 对于情况③，更新空间说明表所要释放位置前后元素的所有数据，并且将他们合并为一个。 对于情况④，重新创建一个模块，然后插入进队列即可。 代码：

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

//回收存储空间算法
void HuiShou()
{
    cout<<"Message：请根据空间空闲表来写入合适回收空间！"<<endl;
    int start1=0; //初始化
    int length1=0;  //初始化
    cout<<"请输入起始地址：";
    cin>>start1;
    cout<<"请输入长度：";
    cin>>length1;
    int len=start1+length1;  //释放区下部
    if(len<=(*(Q.begin())).Start||start1>=((*(Q.end()-1)).Start+(*(Q.end()-1)).Length))
    {
        if(len<(*(Q.begin())).Start)
        {
            mode\[n+q\].Length=length1;
            mode\[n+q\].Start=start1;
            mode\[n+q\].State='R';
            Q.push_front(mode\[n+q\]);
            q++;
        }
        else if(len==(*(Q.begin())).Start)
        {
            (*(Q.begin())).Start=start1;
            (*(Q.begin())).Length+=length1;
        }
        else if(start1==((*(Q.end()-1)).Start+(*(Q.end()-1)).Length))
        {
            (*(Q.end()-1)).Length+=length1;
        }
        else if(start1>((*(Q.end()-1)).Start+(*(Q.end()-1)).Length))
        {
            mode\[n+q\].Length=length1;
            mode\[n+q\].Start=start1;
            mode\[n+q\].State='R';
            Q.push_back(mode\[n+q\]);
            q++;
        }
    }
    else{
    for(pos=Q.begin();pos!=Q.end();pos++)
    {
        if(len==(*(pos+1)).Start&&start1==(\*pos).Start+(\*pos).Length)  //释放区上下部都与空间区邻接
        {
            (\*pos).Length+=(\*(pos+1)).Length+length1;
            Q.erase((pos+1));
        }
        else if((len<(*(pos+1)).Start)&&(start1>(\*pos).Start+(\*pos).Length))
        {
            mode\[n+q\].Start=start1;
            mode\[n+q\].Length=length1;
            mode\[n+q\].State='R';
            Q.insert(pos+1,mode\[n+q\]);
            q++;
        }
        else if((len<(*(pos+1)).Start)&&(start1==(\*pos).Start+(\*pos).Length))
        {
            (\*pos).Length+=(\*(pos+1)).Length+length1;
        }
        else if((len==(*(pos+1)).Start)&&(start1>(\*pos).Start+(\*pos).Length))
        {
            (*(pos+1)).Start = start1;
            (*(pos+1)).Length += length1;
        }
    }
    }
}

结果： ![](http://47.100.4.8/wp-content/uploads/2018/06/123.png)