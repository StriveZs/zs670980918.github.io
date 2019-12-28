---
title: 生产者消费者问题C++实现
url: 678.html
id: 678
categories:
  - C&amp;C++
  - 文章页
  - 生产者消费者问题
  - 算法
date: 2018-04-24 23:22:38
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180424231257.png) 生产者消费者问题 是同步互斥的经典问题。 目的就是验证用信号量机制实现进程互斥的方法，验证用信号量机制实现进程同步的方法。 了解经典同步问题“生产者和消费者” 生产者与消费者可以通过一个环形缓冲池联系起来，环形缓冲池由几个大小相等的缓冲块组成，每个缓冲块容纳一个产品。每个生产者可不断地每次往缓冲池中送一个生产产品，而每个消费者则可不断地每次从缓冲池中取出一个产品。指针in和指针out分别指出当前的第一个空缓冲块和第一个满缓冲块。   首先是在Windows下编写的生产着消费者代码：

#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>
#include <windows.h>
#include <semaphore.h>
#include <unistd.h>
using namespace std;

#define n 10
#define True 1
#define False 0
#define producers 2
#define customers 4

typedef int semaphore;
int buffer\[n\]={0};  //创建缓冲区
semaphore emptys=n,fulls=0; //空和满信号量
pthread\_mutex\_t mutex; //创建互斥信号量

//P操作
int wait(semaphore &mutex1)
{
    mutex1--;
    if(mutex1<0)
        return False;
    else
        return True;
}
//V操作
int signal(semaphore &mutex1)
{
    mutex1++;
    if(mutex1<=0)
        return False;
    else
        return True;
}
//打印缓冲区  在测试时自行选择是否出去
void print()
{
    int i;
    for(i=0;i<n;i++)
        printf("%d ",buffer\[i\]);
    printf("\\n");
}
//生产者
int in=0;
void \*producer(void \*b)
{
    while(True)
    {

        if(wait(emptys))
        {
        //创建一个产品和名称
        pthread\_mutex\_lock(&mutex);  //互斥
        printf("厂家生产一盒牛奶产品，编号为: product%d\\n",in+1);
        buffer\[in\]= 1;
        in=(in+1)%n;
        pthread\_mutex\_unlock(&mutex);
        signal(fulls);
        Sleep(1000);  //设置生产延迟
        }
        else
        {
            printf("<!!!!>库存已经满了<!!!!>\\n");
        }

    }
}

//消费者
int out=0;
void \*consumer(void \*b)
{
    while(True)
    {

        if(!wait(fulls))
        {
            pthread\_mutex\_lock(&mutex);
            if(buffer\[out\] == 1)
            {
                printf("                                      顾客购买了一盒牛奶，产品编号为： product%d\\n",out+1);
                buffer\[out\]= 0;
            }
            out=(out+1)%n;
            pthread\_mutex\_unlock(&mutex);
            signal(emptys);
            Sleep(1000);  //设置消费延迟
        }
        else
        {
            printf("<!!!!>生产池已经为空<!!!!>\\n");
        }

    }
}
int main()
{
    printf("<-------------------------------------------开始生产-------------------------------------------->\\n");
    //初始化信号量
    pthread\_mutex\_init(&mutex,NULL);

    //线程初始化
    int i;
    void *a;
    pthread\_t thread\_pro\[producers\];  //创建生产者线程组
    pthread\_t thread\_cons\[customers\];  //创建消费者线程组
    for(i=0;i<n;i++)
    {
        if(i<producers)
        {
            pthread\_create(&thread\_pro\[i\],NULL,producer,NULL);

        }#include <pthread.h>
        if(i<customers)
            pthread\_create(&thread\_cons\[i\],NULL,consumer,NULL);
    }
    for(i=0;i<n;i++)
    {
        if(i<producers)
        {
            pthread\_join(thread\_pro\[i\],&a);

        }
        if(i<customers)
            pthread\_join(thread\_cons\[i\],&a);
    }
    return 0;
}

  我采用了多线程多个生产者消费者来进行 运行结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/146548913.png)   这里还有在linux下运行的代码：

#include <stdio.h>
#include <pthread.h>
#include <stdlib.h>
#include <semaphore.h>
#include <unistd.h>
using namespace std;

#define n 10
#define True 1
#define False 0
#define producers 2
#define customers 4

typedef int semaphore;
int buffer\[n\]={0};  //创建缓冲区
semaphore emptys=n,fulls=0; //空和满信号量
pthread\_mutex\_t mutex; //创建互斥信号量

//P操作
int wait(semaphore &mutex1)
{
    mutex1--;
    if(mutex1<0)
        return False;
    else
        return True;
}
//V操作
int signal(semaphore &mutex1)
{
    mutex1++;
    if(mutex1<=0)
        return False;
    else
        return True;
}
//打印缓冲区  在测试时自行选择是否出去
void print()
{
    int i;
    for(i=0;i<n;i++)
        printf("%d ",buffer\[i\]);
    printf("\\n");
}
//生产者
int in=0;
void \*producer(void \*b)
{
    while(True)
    {

        if(wait(emptys))
        {
        //创建一个产品和名称
        pthread\_mutex\_lock(&mutex);  //互斥
        printf("The manufacturer produces a carton of milk products, numbered: product%d\\n",in+1);
        buffer\[in\]= 1;
        in=(in+1)%n;
        pthread\_mutex\_unlock(&mutex);
        signal(fulls);
        sleep(1000);  //设置生产延迟
        }
        else
        {
            printf("<!!!!>The inventory is full. <!!!!>\\n");
        }

    }
}

//消费者
int out=0;
void \*consumer(void \*b)
{
    while(True)
    {

        if(!wait(fulls))
        {
            pthread\_mutex\_lock(&mutex);
            if(buffer\[out\] == 1)
            {
                printf("                                      The customer bought a carton of milk, the product number is： product%d\\n",out+1);
                buffer\[out\]= 0;
            }
            out=(out+1)%n;
            pthread\_mutex\_unlock(&mutex);
            signal(emptys);
            sleep(1000);  //设置消费延迟
        }
        else
        {
            printf("<!!!!>Production pool is empty <!!!!>\\n");
        }

    }
}
int main()
{
    printf("<-------------------------------------------开始生产-------------------------------------------->\\n");
    //初始化信号量
    pthread\_mutex\_init(&mutex,NULL);

    //线程初始化
    int i;
    void *a;
    pthread\_t thread\_pro\[producers\];  //创建生产者线程组
    pthread\_t thread\_cons\[customers\];  //创建消费者线程组
    for(i=0;i<n;i++)
    {
        if(i<producers)
        {
            pthread\_create(&thread\_pro\[i\],NULL,producer,NULL);

        }
        if(i<customers)
            pthread\_create(&thread\_cons\[i\],NULL,consumer,NULL);
    }
    for(i=0;i<n;i++)
    {
        if(i<producers)
        {
            pthread\_join(thread\_pro\[i\],&a);

        }
        if(i<customers)
            pthread\_join(thread\_cons\[i\],&a);
    }
    return 0;
}

  下面是在linux下运行的步骤：（有些需要注意的问题在之前的博文中也提到过了）   对代码文件进行编译： ![](http://47.100.4.8/wp-content/uploads/2018/04/856486413.png) 首先打开命令界面，输入 g++ a.cpp –o b –lpthread 即可编译成功生成可执行文件。 ![](http://47.100.4.8/wp-content/uploads/2018/04/78874.png) 运行文件： 在命令行输入： ./b 即可运行文件 需要注意的是： 输出为中文的话可能会出现乱码因此改为了英文。 结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/789745413.png)