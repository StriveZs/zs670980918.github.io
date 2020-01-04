---
title: C++指针数组学习
url: 1119.html
id: 1119
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-03 22:08:53
tags:
  - C/C++
  - 指针
---

![](http://47.100.4.8/wp-content/uploads/2018/05/图片150.png) 对C++指针的整理： 指针变量是用于存放内存单元地址的。 声明指针的语法形式： 数据类型 *标识符；   要注意的只有指针名字是代表的是赋值给指针元素的地址，如果使用*指针名 则是该元素的真实值。 例如：
```
int *t;
```
  上面例子定义是声明一个整形的指针变量，这个指针的名称为t专门用来存放int型数据的地址。   指针的赋值 语法形式： 数据类型 *标识符; 指针名=数据名 //注意这里的数据的类型要和指针的类型相同   例如：
```
int a=0;

int *t;

t = a;
```
    一个数组，可以用他的名字来直接表示它的起始地址。 例如：
```
int a\[10\]={0};

int *t = a;
```
  这里还有一点需要注意的是： 通过指针访问数组元素时要使用：*(t+i)  i为该元素在数组中的序号 综上诉述：（给出一个实例来表示） 代码：  
```
#include <iostream>



using namespace std;



int main()

{

    int a\[5\]={1,2,3,4,5};

    int *t=a;

    cout<<"数组值："<<endl;

    for(int i=0;i<5;i++)

    {

        cout<<a\[i\]<<" ";

    }

    cout<<endl;

    cout<<"指针值："<<endl;

    for(int i=0;i<5;i++)

        cout<<*(t+i)<<" ";

    cout<<endl;

    return 0;

}

  结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/1-2.png)     接下来介绍的二维数组的指针介绍以及在函数参数传递时使用指针经传递：   二维指针数组的定义为： 类型 (*指针名)\[二维数组每列元素的个数\]; 例如：

int (*t)\[2\];

  在访问指针二维数组时 格式为 *（*（指针名+i）+j） 如果为：（*（指针名+i）+j） 则代表数组的每行的首地址 使用： 代码：  

#include <iostream>



using namespace std;



int main()

{

    int (*t)\[2\];

    int a\[2\]\[2\]={1,2,3,4};

    t=a;

    for(int i=0;i<2;i++)

    {

        for(int j=0;j<2;j++)

           cout<<a\[i\]\[j\]<<" ";

        cout<<endl;

    }

    cout<<"对比："<<endl;

    for(int i=0;i<2;i++)

    {

        for(int j=0;j<2;j++)

           cout<<*(*(t+i)+j)<<" ";

        cout<<endl;

    }

    return 0;

}
```
  结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/2-2.png)   接下来介绍指针二维数组作为参数传递的使用： 其实数组不使用指针传递，在调用的函数中如果有对数组的修改原数组的值也会发生改变 下面用一个给出（这是一个矩阵转置的例子） 代码：  
```
#include<iostream>

using namespace std;



void MatrixTranspose(int a\[\]\[3\])

{

    int b\[3\]\[3\]={0};

    for(int i=0;i<3;i++)

        for(int j=0;j<3;j++)

           b\[j\]\[i\]=a\[i\]\[j\];

    for(int i=0;i<3;i++)

        for(int j=0;j<3;j++)

           a\[i\]\[j\]=b\[i\]\[j\];

}



int main()

{

    int a\[3\]\[3\]={0};

    cout<<"请输入一个3*3的数组："<<endl;

    for(int i=0;i<3;i++)

    {

        for(int j=0;j<3;j++)

            cin>>a\[i\]\[j\];

    }

    MatrixTranspose(a);

    cout<<"经过转置之后的数组为："<<endl;

    for(int i=0;i<3;i++)

    {

        for(int j=0;j<3;j++)

            cout<<a\[i\]\[j\]<<" ";

        cout<<endl;

    }

    return 0;

}
```
  结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/3-2.png)   然后给出一个数组作为指针进行参数传递的例子： （同样这里使用到了动态数组的声明） 即在参数形参定义是直接定义一个二维指针数组进行接收二维数组的地址 代码：  
```
#include<iostream>



using namespace std;



void MatrixTranspose(int (*a)\[3\],int n)

{

    int (*t)\[3\] = new int\[3\]\[3\];

    for(int i=0;i<n;i++)

        for(int j=0;j<n;j++)

           *(*(t+j)+i)=a\[i\]\[j\];

    for(int i=0;i<n;i++)

        for(int j=0;j<n;j++)

           a\[i\]\[j\]=*(*(t+i)+j);

    delete \[\] t;

}

int main()

{

    int a\[3\]\[3\]={0};

    cout<<"请输入一个3*3的数组："<<endl;

    for(int i=0;i<3;i++)

    {

        for(int j=0;j<3;j++)

            cin>>a\[i\]\[j\];

    }

    MatrixTranspose(a,3);

    cout<<"经过转置之后的数组为："<<endl;

    for(int i=0;i<3;i++)

    {

        for(int j=0;j<3;j++)

            cout<<a\[i\]\[j\]<<" ";

        cout<<endl;

    }

    return 0;

}
```
  结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/4-2.png)