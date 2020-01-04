---
title: C++实现银行家算法
url: 1208.html
id: 1208
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-19 22:00:31
tags:
  - C/C++
  - 银行家算法
---

![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180519215119.png) 设计一个n个并发进程共享m个系统资源的程序实现银行家算法。要求包含：    (1) 能显示当前系统资源的占用和剩余情况； (2) 进程提出资源请求，如何可以满足则分配，如果不可以满足则阻塞。 (3) 将银行家算法和随机算法进行比较。 银行家算法 在避免死锁的方法中，所施加的限制条件较弱，有可能获得令人满意的系统性能。在该方法中把系统的状态分为安全状态和不安全状态，只要能使系统始终都处于安全状态，便可以避免发生死锁。 银行家算法的基本思想是分配资源之前，判断系统是否是安全的；若是，才分配。它是最具有代表性的避免死锁的算法。 设进程process提出请求REQUEST \[i\]，则银行家算法按如下规则进行判断。 (1)如果REQUEST \[cusneed\] \[i\]<= NEED\[cusneed\]\[i\]，则转（2)；否则，出错。 (2)如果REQUEST \[cusneed\] \[i\]<= AVAILABLE\[i\]，则转（3)；否则，等待。 (3)系统试探分配资源，修改相关数据： AVAILABLE\[i\]-=REQUEST\[cusneed\]\[i\]; ALLOCATION\[cusneed\]\[i\]+=REQUEST\[cusneed\]\[i\]; NEED\[cusneed\]\[i\]-=REQUEST\[cusneed\]\[i\]; (4)系统执行安全性检查，如安全，则分配成立；否则试探险性分配作废，系统恢复原状，进程等待。 安全性检查算法 （1）设置两个工作向量Work=AVAILABLE;FINISH （2）从进程集合中找到一个满足下述条件的进程， FINISH==false; NEED<=Work; 如找到，执行（3)；否则，执行（4)   （3）设进程获得资源，可顺利执行，直至完成，从而释放资源。 Work=Work+ALLOCATION; Finish=true; GOTO 2 流程图： ![](http://47.100.4.8/wp-content/uploads/2018/05/主程序流程图.png)   代码：
```
#include<iostream>
#include<string.h>

using namespace std;

#define process 5 //并发进程数
#define resource 3 //资源种数

//PCB模块结构
struct PCB{
    int Name;  //进程名
    char State;  //状态  R为就绪 N为没有就绪
    int Request\[resource\];  //对资源的申请量
    int Need\[resource\];  //资源的需求总量
    int Allocation\[resource\];  //对于资源的占有量
    int Max\[resource\]; //对资源的最大需求量
    int Wa\[resource\];  //Work+Allocation的需求量
    int ZY\[resource\]; //Work资源值
    bool Finish;  //能执行完标志
}Process\[process\],Process_back\[process\];
//Process_back\[process\] 作为预分配的备份数据 以便于恢复

struct Available{  //资源模块
    int available;  //资源数目
    int work;  //工作向量
}Resource\[resource\],Resource_back\[resource\];

//Resource_back\[resource\] 作为预分配的备份数据 以便于恢复

int a\[resource\]; //临时数组
int safelist\[process\];  //安全序列
int p_num=0;  //当前完成的进程数

void ShowZiYuan()  //绘制进程数据图
{
    cout<<"当前进程数据图："<<endl;
    cout<<"  进程名            Max            Allocation            Need            状态"<<endl;
    for(int i=0;i<process;i++)
    {
        cout<<"Process"<<Process\[i\].Name;
        cout<<"           ";
        for(int j=0;j<resource;j++)
            cout<<Process\[i\].Max\[j\]<<" ";
        cout<<"           ";
        for(int j=0;j<resource;j++)
            cout<<Process\[i\].Allocation\[j\]<<" ";
        cout<<"              ";
        for(int j=0;j<resource;j++)
            cout<<Process\[i\].Need\[j\]<<" ";
        cout<<"           ";
        cout<<Process\[i\].State<<endl;
    }
    cout<<endl;
}
void init()  //初始化所有数据
{
    int Maxs\[process\]\[resource\]={ {7,5,3},{3,2,2},{9,0,2},{2,2,2},{4,3,3}};
    int Allocations\[process\]\[resource\]={ {0,1,0},{2,0,0},{3,0,2},{2,1,1},{0,0,2}};
    for(int i=0;i<process;i++)
    {
        Process\[i\].Name=i+1;
        Process\[i\].State='R';
        for(int j=0;j<resource;j++)
            {
                Process\[i\].Request\[j\]=0;
                Process\[i\].Wa\[j\]=0;
                Process\[i\].ZY\[j\]=0;
            }
        Process\[i\].Finish=false;
        for(int j=0;j<resource;j++)
        {
            Process\[i\].Max\[j\]=Maxs\[i\]\[j\];
            Process\[i\].Allocation\[j\]=Allocations\[i\]\[j\];
        }
        for(int j=0;j<resource;j++)
            Process\[i\].Need\[j\]=Process\[i\].Max\[j\]-Process\[i\].Allocation\[j\];
    }
    Resource\[0\].available = 10;
    Resource\[1\].available = 12;
    Resource\[2\].available = 11;

}

void ShowSafeList()  //显示安全序列
{
    cout<<"安全序列为："<<endl;
    for(int i=0;i<process-1;i++)
        cout<<safelist\[i\]<<"->";
    cout<<safelist\[process-1\]<<endl;
}

void ShowYuFen()  //绘制成功预分配图
{
    cout<<"成功预分配图"<<endl;
    cout<<"  进程名            Work            Need            Allocation            Work+Allocation            Finish"<<endl;
    for(int i=0;i<process;i++)
    {
        cout<<"Process"<<Process\[i\].Name;
        cout<<"           ";
        if(i==0)
        {
            for(int j=0;j<resource;j++)
                cout<<a\[j\]<<" ";
            cout<<"           ";
        }
        if(i>0)
        {
            for(int j=0;j<resource;j++)
                cout<<Process\[i\].ZY\[j\]<<" ";
            cout<<"           ";
        }
        for(int j=0;j<resource;j++)
            cout<<Process\[i\].Need\[j\]<<" ";
        cout<<"           ";
        for(int j=0;j<resource;j++)
            cout<<Process\[i\].Allocation\[j\]<<" ";
        cout<<"                ";
        for(int j=0;j<resource;j++)
            cout<<Process\[i\].Wa\[j\]<<" ";
        cout<<"                 ";
        if(Process\[i\].Finish == 1)
           cout<<"true"<<endl;
        else
            cout<<"false"<<endl;
    }
    cout<<endl;
    ShowSafeList();
}

void BackUp()  //数据备份
{
    for(int i=0;i<process;i++)
        Process_back\[i\]=Process\[i\];
    for(int i=0;i<resource;i++)
        Resource_back\[i\]=Resource\[i\];

}

void ReBack()  //数据还原
{
    for(int i=0;i<process;i++)
        Process\[i\]=Process_back\[i\];
    for(int i=0;i<resource;i++)
        Resource\[i\]=Resource_back\[i\];
}


int num;
int aff\[resource\];

bool InputRequest()  //输入请求
{
    cout<<"输入进程号以及请求的资源数目：";
    cin>>num;
    for(int i=0;i<resource;i++)
        cin>>aff\[i\];
    int flag = 0;
    for(int i=0;i<resource;i++)
    {
        if(Process\[num-1\].Need\[i\]<aff\[i\])
        {
            cout<<"超出需求上限，请求操作失败"<<endl;
            flag = 1;
            break;
        }
        if(Resource\[i\].available<aff\[i\])
        {
            cout<<"超过当前可获得的资源，请求操作失败"<<endl;
            flag = 1;
            break;
        }
    }
    if(flag == 1)
    {
        ReBack();
        return false;
    }
    for(int i=0;i<resource;i++)
    {
        Process\[num-1\].Need\[i\] -= aff\[i\];
        Process\[num-1\].Allocation\[i\] += aff\[i\];
        Resource\[i\].available -= aff\[i\];
    }
    //ShowZiYuan();
    for(int i=0;i<process;i++)
        Process\[i\].Finish = false;
    return true;
}

bool IsSafe()  //安全性检测算法
{
    int t=0;
    //ShowZiYuan();
    for(int i=0;i<resource;i++)
    {
        a\[i\]=Resource\[i\].available;
    }
    for(int i=0;i<process;i++)
    {
        for(int j=0;j<resource;j++)
           {
               if(Process\[i\].Need\[i\]>Resource\[i\].available)
              {
                  t++;
                  break;
              }
           }
        if(t == 5)
           return false;
    }
    //cout<<"测试"<<endl;
    int counts=0;
    int flag = 0;

    while(counts<5)
    {
        int flag1 = 0;
        for(int i=0;i<process;i++)
        {
            for(int j=0;j<resource;j++)
            {
                if(Process\[i\].Finish == false)
                {
                    if(Resource\[j\].available < Process\[i\].Need\[j\])
                    {
                        flag1 = 1;
                        break;
                    }
                }
                else
                {
                    flag1 = 1;
                    break;
                }
            }
            if(flag1 == 0)
            {
                    safelist\[counts\]=i+1;
                    counts++;
                    flag = 1;
                    for(int j=0;j<resource;j++)
                    {
                        Process\[i\].Wa\[j\]=Process\[i\].Allocation\[j\]+Resource\[j\].available;
                        Process\[i\].ZY\[j\] = Process\[i\].Wa\[j\];
                        Resource\[j\].available = Resource\[j\].available + Process\[i\].Allocation\[j\];

                    }
                    Process\[i\].Finish = true;
            }
        }
        if(flag == 0)
        {
            ReBack();
            return false;
        }
    }
    return true;
}

bool YinHangJia()  //银行家算法
{
    BackUp();
    bool s=true;
    s=InputRequest();
    bool flag;
    flag = IsSafe();
    if(s == false)
    {
        ReBack();
        cout<<"该请求指令被拒绝，无法找到一个有效的安全序列\\n请重新输入！"<<endl;
        return false;
    }
    if(flag = true&&s!=false)
        {
            ShowYuFen();
            return true;
        }
}

int main()
{
    bool t=true;
    init();
    t=IsSafe();
    ShowZiYuan();
    if(t == false)
        cout<<"初始化的可获得值不满足条件找不到安全序列！"<<endl;
    else
    {
    ShowYuFen();
    int k=0;
    bool flag=true;
    while(1)
    {
        for(int i=0;i<process;i++)
            if(Process\[i\].Finish == false)
                {
                    k++;
                }
        if(k!=process)
            if(YinHangJia()==false)
                YinHangJia();
        else
            break;
    }
    }
    return 0;
}
```
  windows下的结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/3213123-1.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/4324234234-1.png)