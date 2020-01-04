---
title: C++ 冒泡排序&折半查找
url: 1114.html
id: 1114
categories:
  - C&amp;C++
  - 文章页
  - 算法
date: 2018-05-02 21:48:31
tags:
  - C/C++
  - 折半查找
  - 冒泡排序
---

![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180502213608.png) 冒泡策略：在一次循环中把最大元素移到序列最右端。 算法代码： 这里我以整型数组为例  数组类型大家可自行定义
```
//冒泡排序
//一次冒泡
void bubble(int a\[\],int n)
{
    for(int i;i<n-1;i++)
        if(a\[i\]>a\[i+1\])
           swap(a\[i\],a\[i+1\]);  //进行值交换的库函数
}
//冒泡排序
void bubbleSort(int a\[\],int n)
{
    for(int i=n;i>1;i--)
        bubble(a,i);
}
```
注意：这里数组的传递要使用指针，否则传递数组值只会最为形参使用，在原值里面不会改变   ![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180502213816.png) 折半查找是在一个有序数组中查找元素x。  一定要是有序的序列 算法思想：设置两个端点一个为左端点一个为有端点，先求出当前端点的中值然后和需要求得的值进行比较如何相等则返回它的序号，如果大于则重置左端点为中值+1 然后继续上面的步骤，如果小于则重置右端点为中值—1然后继续上面的步骤 代码：
```
#include <iostream>
using namespace std;
int binarySearch(int a\[\],int n ,int x)   //折半查找的重要前提是需要的一个已经排序好的序列
{
    int left = 0;  //数据段最左段
    int right = n-1;  //数据段最右端
    while(left <= right)
    {
        int middle = (left + right) / 2;  //计算出当前中值
        if (x == a\[middle\])
            return middle;
        else if(x > a\[middle\])
            left = middle + 1;
        else
            right = middle - 1;
    }
    return -1;
}
int main()
{
    int a\[5\]={1,2,3,4,5};
    int t=-2;
    t = binarySearch(a,5,5);
    if(t == -1)
        cout<<"没有在序列中找到对应的值！"<<endl;
    else
        cout<<"要查找的值在序列中的序号为:"<<t+1<<endl;
    return 0;
}
```
  结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/QQ图片20180502213910.png)