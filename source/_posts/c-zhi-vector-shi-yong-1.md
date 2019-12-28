---
title: C++之vector使用
url: 1138.html
id: 1138
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-06 22:41:21
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/图片150.png) 使用vector创建数组对象   C++标准库提供了被封装的动态数组—vector，而且这种封装的数组可以具有各种类型。 vector它不是类，它是类的一个模板。 使用vector动态定义数组的形式为： vector<元素类型>数组对象名（数组长度）;   例如： vector<int>array(5);  //创建一个长度为5的动态整形数组对象   与普通数组不同的是，用vector定义的数组对象所有的元素都会被初始化。如果数组的元素类型为基本数据类型，则所有元素都会被以0初始化。如果数组元素为类类型，则会调用类的默认构造函数初始化。   创建数组的元素初值也可以自己选择： 但是只能为相同的初值 vector<元素类型>数组对象名（数组长度,元素初值）; 对vector数组对象元素的访问方式为：数组对象名\[下标表达式\]; 可以使用它的成员函数size（）来得到数组的大小。   计算数组平均值：使用到了size（） 代码：

#include<iostream>

#include<vector>

using namespace std;



double average(const vector<double>&arr)

{

    double sum=0;

    for(int i=0;i<arr.size();i++)

        sum += arr\[i\];

    return sum/arr.size();

}

int main()

{

    int n;

    cout<<"请输入n的值：";

    cin>>n;



    vector<double>arr(n,0);

    cout<<"输入n个数组元素:"<<endl;

    for(int i=0;i<n;i++)

        cin>>arr\[i\];



    cout<<"平均值为："<<average(arr)<<endl;

    return 0;

}

  结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/123123.png)