---
title: C++性能分析涉及的算法
url: 693.html
id: 693
categories:
  - C&amp;C++
  - 性能分析
  - 文章页
  - 算法
date: 2018-04-26 22:12:59
tags:
  - C/C++
  - Algorithm
---

![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180425215619.png)   用于测试空间复杂度的算法，顺序查找  在数组中从左至右查找第一个与x相等的元素。如果找到则返回它第一次出现的位置。如果没有则返回-1 顺序查找的两种方法： （1）普通的方法：
```
#include<iostream>

using namespace std;

//整数类型的查找
int sequentialSearch(int a\[\],int n,int x)
{
    int i=0;
    int flag = -1;
    for (i;i<n;i++)
    {
        if(a\[i\] == x)
            {
                flag = i;
                break;
            }
    }
    return flag;
}
//函数重载 针对float类型
int sequentialSearch(float a\[\],int n,float x)
{
    int i=0;
    int flag = -1;
    for (i;i<n;i++)
    {
        if(a\[i\] == x)
            {
                flag = i;
                break;
            }
    }
    return flag;
}

int main()
{
    int a\[10\];
    float b\[10\];
    int n = 5;
    for(int i = 0;i < 10;i++)
    {
        a\[i\] = i;
        b\[i\] = i + 0.1;
    }
    cout<<"对整数使用顺序查找5出现的位置:"<<sequentialSearch(a,10,5)<<endl;
    cout<<"对浮点数使用顺序查找2.1出现的位置:"<<sequentialSearch(b,10,2.1)<<endl;
    return 0;
}
```
结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/7894156.png) 顺序查找的递归实现：
```
#include<iostream>

using namespace std;

//整数类型的查找
int RsequentialSearch(int a\[\],int n,int x)
{
    if(n < 1)
        return -1;
    if(a\[n-1\] == x)
        return n;
    return RsequentialSearch(a,n-1,x);
}
int main()
{
    int a\[10\];
    for(int i = 0;i < 10;i++)
        a\[i\]=i;
    cout<<"对整数使用顺序查找3出现的位置:"<<RsequentialSearch(a,9,3)<<endl;
    return 0;
}
```
结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/882522.png)   时间复杂度的涉及的算法，一个程序的时间复杂度可以通过它进行的for循环次数进行计算。 普通的多项式计算：
```
#include<iostream>
using namespace std;

int ployEval(int coeff\[\],int n,const &x)
{
    int y=1,value=coeff\[0\];
    for (int i = 1;i<= n;i++)
    {
        y *= x;
        value += y*coeff\[i\];
    }
    return value;
}
//coeff\[i\] 为ai
//构造的多项式计算为：a0\*x^4+a1\*x^3+a2\*x^2+a1\*x^1+a0*x^0
int main()
{
    int test;
    int coeff\[5\]={1,2,3,4,5},n=4,x=2;
    test = ployEval(coeff,n,x);
    cout<<"test="<<test<<endl;
    return 0;
}
```
结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/777777.png) 这里看出由于循环次数比较多所以时间复杂度比较大 这里可以使用horner法则进行多项式的拆分即可将 a0\*x^4+a1\*x^3+a2\*x^2+a1\*x^1+a0\*x^0拆分为如下式子： (((((x\*a1)+a0)\*x+a2)\*x+a3)*x+a4)  
```
#include<iostream>
using namespace std;
//利用霍尔法则进行多项式的变化：(((((x\*a1)+a0)\*x+a2)\*x+a3)\*x+a4)
int horner(int coeff\[\],int n,const &x)
{
    int value = coeff\[n\];
    for(int i=1;i<=n;i++)
    {
        value = value * x +coeff\[n-i\];
    }
    return value;
}
int main()
{
    int test,hornertest;
    int coeff\[5\]={1,2,3,4,5},n=4,x=2;

    hornertest = horner(coeff,n,x);
    cout<<"horner apply:"<<hornertest<<endl;
    return 0;
}
```
结果： ![](http://47.100.4.8/wp-content/uploads/2018/04/66666666.png) 跟上面的结果对比发现通过霍尔法则可以将时间复杂度缩短很多   End！~