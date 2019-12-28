---
title: 进程同步之生产者消费者问题
url: 1350.html
id: 1350
categories:
  - 操作系统
  - 文章页
date: 2018-06-12 23:41:03
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180612233953.png) 主要介绍的是使用记录性信号量来实现生产者消费者问题。 在介绍生产者消费者问题之前先介绍一些记录型信号量：   采取的是让权等待策略，wait（）和signal（）分别用p（）和v（）来表示 其中包含了一个用于表示资源数目的整型变量value，还包含了一个进程链表指针list。 结构体代码：

typedef struct{

    int value;

    struct process\_control\_block *list;

}

  相应的p和v操作的伪代码：

wait(semaphore *S)

{

    S->value--;

    if(S->value<0)

        block(S->list);  //如果资源数小于0,则调用阻塞进程将该进程阻塞

}



signal(semaphore *S)

{

    S->value++;

    if(S->value<=0)

        wakeup(S->list); //如果有阻塞进程则将它唤醒，将进程转为就绪状态

}

  使用PV操作实现互斥操作： Semaphore mutex=1； P（mutex） 操作； V（mutex） 一般在互斥操作中PV是成对出现的。 而在同步操作中PV操作一般是出现在不同的进程中。   使用记录性信号量来实现消费者生产者问题： 有三种情况：

*   一个生产者、一个消费者、缓冲区只有一个容量
*   一个生产者、一个消费者、缓冲区有多个空间
*   多个生产者、多个消费者、缓冲区有多个空间

情况一的实现伪代码：

//情况一

semaphore full=0,empty=1;  // full代表的是已经被占用的空间数量  empty未被使用的空间数量

main()

cobegin

{

    Process producer()

    while(1)

    {

        生产一个产品;

        P(empty);

        将产品送入缓冲区;

        V(full);

    }

   

    Process customer()

    {

        P(full);

        从缓冲区去除一个产品;

        V(empty);

        使用产品;

    }

}coend;

  由于只有一个消费者和一个生产者所以不需要设置互斥信号量   情况二的实现伪代码：

//情况二

semaphore full=0,empty=n;  //full代表的是已经被占用的空间数量  empty未被使用的空间数量、它的总量为n

semaphore buffer\[n\]; //缓冲区

int in,out;

in=out=0;



main()

cobegin

{

    Process producer()

    while(1)

    {

        生产一个产品;

        P(empty);

        将产品送入缓冲区buffer\[in\];

        in = (in+1)%n;

        V(full);

    }

   

    Process customer()

    {

        P(full);

        从缓冲区buffer\[out\]去除一个产品;

        out = (out+1)%n;

        V(empty);

        使用产品;

    }

}coend;

  情况三具体实现伪代码：

//情况三

semaphore mutex=1,full=0,empty=n;  //互斥信号量的初值为1 full代表的是已经被占用的空间数量  empty未被使用的空间数量、它的总量为n

semaphore buffer\[n\]; //缓冲区

int in,out;

in=out=0;



main()

cobegin

{

    Process producer()

    while(1)

    {

        P(empty);

        生产一个产品;

        P(mutex);

        将产品送入缓冲区buffer\[in\];

        in = (in+1)%n;

        V(mutex);

        V(full);

    }

   

    Process customer()

    {

        P(full);

        P(mutex);

        从缓冲区buffer\[out\]去除一个产品;

        out = (out+1)%n;

        V(mutex);

        V(empty);

        使用产品;

    }

}coend;

  多个消费者和多个消费者实现可以使用多线程来实现，具体实现代码我在之前的博文上已经给出大家可自行翻阅。