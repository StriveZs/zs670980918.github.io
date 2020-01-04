---
title: FCFS算法和优先级调度算法C++实现
url: 1168.html
id: 1168
categories:
  - C&amp;C++
  - 文章页
  - 算法
date: 2018-05-12 23:15:30
tags:
  - C/C++
  - FCFS
---

![](http://47.100.4.8/wp-content/uploads/2018/05/图片150.png) FCFS调度算法（短作业优先） 该算法采用非剥夺策略，算法按照进程提交或进程变为就绪状态的先后次序，分派 CPU。当前进程占用CPU，直到执行完或阻塞，才出让CPU（非抢占方式）。在进程唤醒后（如I/O 完成），并不立即恢复执行，通常等到当前进程出让CPU。这是最简单的调度算法，比较有利于长进程，而不利于短进程，有利于CPU 繁忙的进程，而不利于I/O 繁忙的进程。 算法流程： ![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180512230549.png) 代码：
```
#include<iostream>
#include<ctime>
#include <cstdlib>
#include<windows.h>
#include<malloc.h>

using namespace std;
#define MAX 5
typedef int ElemType;
typedef char State;

typedef struct PCB{
ElemType flag; //进程标识
struct PCB *next;//链接指针
ElemType arrive; //到达时间
ElemType process; //运行时间
ElemType start; //开始执行时间
ElemType current; //当前状态
}PCB,*PCBList;

typedef struct{
PCBList fronts;
PCBList last;
}PCBLink;

int flagfull = 0; //定义一个全局变量用来表示当前已有进程在处理机中
ElemType times = 1; //初始化全局时间以便确定处理机中进程的开始执行时间
int num=0; //总的进程计数器

//进程插入操作
void InputList(PCBLink &L,int i)
{
    PCB \*p,\*tail,*q;
    int arrivetime=0,processtime=0;
    arrivetime = i*i;
    processtime = time((time_t*)NULL)%20;  //根据系统当前秒数随机生成运行时间
    q=(PCBList)malloc(sizeof(PCB));  //创建列表头节点
    if(i==1)
    {
        L.fronts = L.last = q;
        q->flag = i;  //设置标识符
        q->next = NULL;  //将头指针的后面节点置为空
        q->arrive = arrivetime;  //设置到达时间
        q->start = 0; //初始化开始时间
        q->process = processtime; //设置执行时间
        q->current = 0;  //设置初始状态  R表示就绪 C表示正在运行 O表示运行结束
    }
    else
    {

        p=(PCBList)malloc(sizeof(PCB)); //创建子节点
        p->flag = i;
        p->next = NULL;  //将表尾指针设置为空
        p->current = 0;
        p->process = processtime;
        p->start = 0; //初始化开始时间
        p->arrive = arrivetime;
        L.last->next = p;  //将p节点插入到表尾
        L.last = p;
    }
}
//显示当前就绪队列中的进程的状态
void showState(PCBLink &L)
{
    cout<<endl;
    cout<<endl;
    PCBList p;
    p=(PCBList)malloc(sizeof(PCB));
    p=L.fronts;
    for(int i=1;i<=MAX;i++)
    {
       cout<<"进程"<<i<<endl;
       cout<<"<----------------创建进程的信息：---------------------->"<<endl;
       cout<<"进程标识："<<p->flag<<endl;
       cout<<"进程到达时间："<<p->arrive<<endl;
       cout<<"进程开始时间："<<p->start<<endl;
       cout<<"进程执行时间："<<p->process<<endl;
       if(p->current==-1)
        cout<<"进程当前状态为：O"<<endl;
       else if(p->current==0)
        cout<<"进程当前状态为：R"<<endl;
       else
        cout<<"进程当前状态为：C"<<endl;
       cout<<"<-------------------信息结束：---------------------->"<<endl;
       p=p->next;
       Sleep(500);
    }
    cout<<endl;
    cout<<endl;
}

//处理机进程运行
void overprocess(PCBList &p)
{
    num++;
    Sleep(1000);
    p->process--;
    p->current=-1;
    cout<<"进程"<<num<<"运行结束！"<<endl;
    cout<<"<--------------进程信息：---------------------->"<<endl;
    cout<<"进程标识："<<p->flag<<endl;
    cout<<"进程到达时间："<<p->arrive<<endl;
    cout<<"进程开始时间："<<p->start<<endl;
    cout<<"进程完成时间："<<p->start + p->process + 1<<endl;
       if(p->current==-1)
        cout<<"进程当前状态为：O"<<endl;
       else if(p->current==0)
        cout<<"进程当前状态为：R"<<endl;
       else
        cout<<"进程当前状态为：C"<<endl;
    cout<<"<--------------信息结束：---------------------->"<<endl;
    flagfull=0;
}

//将进程调度进处理机中
void Scheduling(PCBLink &L)
{
    if(flagfull == 1)
    {
        cout<<"当前已有进程在处理机中请等待！"<<endl;
    }
    else
    {
        //将进程从就绪队列中删除
        PCBList p,j;
        p=(PCBList)malloc(sizeof(PCB));
        j=(PCBList)malloc(sizeof(PCB));
        j=L.fronts;
        p = L.fronts->next;
        L.fronts=p;
        j->next = NULL;
        //修改信息
        //j为当前在处理机中的进程
        j->current = 1;
        //处理进程开始执行时间
        if(times == 1) //表示第一个进程
            {
                j->start = times;
                times = j->process; //为下一次进程开始做准备  这里的time更准确的为下次处理进程开始的时间
            }
        else
        {
            if(j->arrive > times)  //如果下一个进程还没到达则time设置为下一个进程到达的时间
                {
                    times = j->arrive;
                    j->start = j->arrive;
                }
            else //否则将time直接加上下一个进程的运行时间
            {
                j->start = times;
                times = times + j->process;
            }
        }
        flagfull = 1;
        overprocess(j);
    }
}

int main()
{
    cout<<"<------------------------信息提示栏：--------------------------------->"<<endl;
    cout<<"                                 R代表就绪状态"<<endl;
    cout<<"                                 C代表运行状态"<<endl;
    cout<<"                                 O代表结束状态"<<endl;
    cout<<"<--------------------------------------------------------------------->"<<endl;
    PCBLink L;
    cout<<"<-------------------------开始运行！---------------------------------->"<<endl;
    for(int i=1;i<=MAX;i++)
    {
        InputList(L,i);
        cout<<"第"<<i<<"个进城进入就绪队列！"<<endl;
        Sleep(1000);
    }
    cout<<"初始化结束！"<<endl;
    cout<<"<------------------------显示当前队列信息！---------------------------->"<<endl;
    showState(L);
    cout<<endl;
    cout<<"<------------------------开始进程调度！-------------------------------->"<<endl;
    while(true)
    {
        Scheduling(L);
        if(num==MAX)
            break;
    }
    cout<<"<-------------------------进程调度结束！------------------------------->"<<endl;

    return 0;
}
```
截图： ![](http://47.100.4.8/wp-content/uploads/2018/05/312312312.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/123154324234.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/4234324234.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/123234234.png)   优先级调度算法： 优先级越高的进程会被优先选择，但是这里不是抢占式的调度算法。 根据每个进程块的优先级在队列中选择一个优先级最大的进程，然后将进程放到处理机中进行运行。进程每运行一次重新计算各进程的响应比。由于本实验是模拟处理器调度，所以，对被选中的进程并不实际的启动运行，而是执行：优先级减1，运行时间减1，然后再次从就绪队列中选择新的优先级进程放入到处理机中，循环执行上面的步骤，当某个进程运行结束后，将它从队列中去除直至所有的进程都从中去除，然后结束。 这里我的优先级是在我的算法中的所有进程初始化的值手动输入的。 在处理机选择进程时，总是选择队列中优先级最高的进程运行。为了采用动态优先级调度，在每次进程运行一次之后，其优先级就会减1.当进程运行结束时首先将它的状态更改为完成状态（C），并且撤出就绪队列，如果就绪队列不为空则重复执行上面的操作。 ![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180512231124.png) 代码：
```
#include<iostream>
#include<stdlib.h>
#include<conio.h>
#include<malloc.h>
#include<windows.h>

using namespace std;

int MAX = 5;

typedef int ElemType;
typedef char State;

typedef struct PCB{
ElemType name;  //进程名
State current;  //进程状态
ElemType priority;  //进程优先级
ElemType runtime; //进程运行时间
ElemType haverun; //进程已经运行的时间
struct PCB *next; //链接指针
}PCB,*PCBList;

typedef struct{
PCBList fronts;
PCBList last;
}PCBLink;

int num=0;  //记录以及运行结束的进程

//进程创建
void inputPCB(PCBLink &L,int i)
{
    PCB \*p,\*tail,*q;
    int run=0,super=0;
    cout<<"请输入第"<<i<<"个进程的运行时间：";
    cin>>run;
    cout<<"请输入第"<<i<<"个进程的优先级:";
    cin>>super;
    q=(PCBList)malloc(sizeof(PCB));  //创建列表头节点
    if(i==1)
    {
        L.fronts = L.last = q;
        q->name = i;
        q->next = NULL;  //将头指针的后面节点置为空
        q->runtime = run;
        q->priority = super;
        q->haverun = 0;
        q->current = 'R';  //设置初始状态  R表示就绪 C表示正在运行 O表示运行结束
    }
    else
    {
            p=(PCBList)malloc(sizeof(PCB)); //创建子节点
            p->name = i;
            p->runtime = run;
            p->priority = super;
            p->haverun = 0;
            p->current = 'R';
            p->next = NULL;  //将表尾指针设置为空
            L.last->next = p;  //将p节点插入到表尾
            L.last = p;
    }
}

//将进程放入处理机
void processing(PCBLink &L,PCBList &q)
{
    if(q->haverun == q->runtime&&num != MAX)
    {
        PCBList s;
        s=(PCBList)malloc(sizeof(PCB));
        s=L.fronts;
        if(s->name == q->name)
        {
            L.fronts=q->next;
            q->next=NULL;
        }
        else
        {
           while(s->next->name!=q->name)
           {
              s = s->next;
           }
           s->next = q->next;
        }
        num++;
        cout<<"进程"<<num<<"完成被移除！"<<endl;
    }
    else
    {
        q->haverun++;
        if(q->priority>0)
            q->priority--;
        cout<<endl;
        cout<<"当前在处理中的进程是："<<q->name<<endl;
        cout<<"进程已经运行的时间："<<q->haverun<<endl;
        cout<<"进程需要运行的剩余时间："<<q->runtime-q->haverun<<endl;
        cout<<"就绪队列中的进程数为："<<MAX-num<<endl;
        cout<<endl;
        Sleep(600);
    }
}

//选择优先级最高的进程放入CPU
void selecthigest(PCBLink &L)
{
    int higest=0;  //存储最大优先级
    int t=0;
    PCBList p,q;
    p=(PCBList)malloc(sizeof(PCB));
    q=(PCBList)malloc(sizeof(PCB));
    q=p=L.fronts;
    higest = p->priority;
    while(p->next!=NULL)
    {
        t = p->next->priority;
        if(t > higest)
        {
            higest = t;
            q=p->next;
        }
        p=p->next;
    }
    processing(L,q);
}

//显示当前就绪队列中的进程的状态
void showState(PCBLink &L)
{
    cout<<endl;
    cout<<endl;
    PCBList p;
    p=(PCBList)malloc(sizeof(PCB));
    p=L.fronts;
    for(int i=1;i<=MAX;i++)
    {
       cout<<"进程"<<i<<endl;
       cout<<"<----------------创建进程的信息：---------------------->"<<endl;
       cout<<"进程标识："<<p->name<<endl;
       cout<<"进程执行时间："<<p->runtime<<endl;
       cout<<"进程当前状态："<<p->current<<endl;
       cout<<"进程的优先级："<<p->priority<<endl;
       cout<<"<-------------------信息结束：---------------------->"<<endl;
       p=p->next;
       Sleep(500);
    }
    cout<<endl;
    cout<<endl;
}

int main()
{
    PCBLink L;
    for(int i=1;i<=MAX;i++)
    {
        inputPCB(L,i);
        cout<<"第"<<i<<"个进城进入就绪队列！"<<endl;
        cout<<endl;
        Sleep(1000);
    }
    showState(L);
    cout<<"<--------------------开始处理进程--------------------------->"<<endl;
    while(num !=MAX)
    {
        selecthigest(L);
    }
    if(num == MAX)
        cout<<"<---------------------所有进程处理完毕！--------------------->"<<endl;
    return 0;
}
```
  实现： ![](http://47.100.4.8/wp-content/uploads/2018/05/1-5.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/2-5.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/3-4.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/4-4.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/5-2.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/6-1.png) ![](http://47.100.4.8/wp-content/uploads/2018/05/7-1.png)