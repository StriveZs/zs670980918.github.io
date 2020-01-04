---
title: C++动态内存的使用
url: 1126.html
id: 1126
categories:
  - C&amp;C++
  - C++学习
  - 文章页
date: 2018-05-04 22:17:03
tags:
  - C/C++
  - 动态内存
---

![](http://47.100.4.8/wp-content/uploads/2018/05/图片150.png) 在C++中动态内存分配技术可以保证程序在运行过程中按照实际需要申请适量的内存，使用结果后还会释放，这种在程序运行过程中申请和释放的存储单元也称为堆对象。 在C++程序中建立和删除堆对象使用两个运算符：new和delete   运算符new的功能是动态内存分配，语法形式为： new 数据类型 （初始化参数列表）;   例如：
```
int *t = new int;  //这里是动态的创建了一个整形数据
```
这里需要的注意的是如果格式为：int *t = new int(); 这里的括号为对数据的初始化如果没有则不进行初始化。   使用delete进行对内存的释放。 创建一个动态一维数组：
```
int *t = new int\[5\];  //这里动态声明了一个一维数组
```
释放一个一维动态数组：
```
delete \[\] t;
```
创建一个动态二维数组
```
int (*t)\[5\] = new int \[5\]\[5\];
```
释放：
```
delete \[\] t;
```
一维数组用于字符串连接 （这里使用到了cstring头文件的strlen（）得到字符串长度） 代码：
```
#include<iostream>

#include<cstring>



using namespace std;



int main()

{

    char *string1 = new char\[100\];

    cout<<"输入第一个字符串："<<endl;

    cin.getline(string1,100);

    char *string2 = new char\[100\];

    cout<<"输入第二个字符串："<<endl;

    cin.getline(string2,100);

    char *string3 = new char\[100\];

    //使用string1连接string2

    for(int i=0;i<strlen(string1)+strlen(string2);i++)

        {

            if(i<strlen(string1))

                string3\[i\]=string1\[i\];

            else

                string3\[i\]=string2\[i-strlen(string1)\];

        }

    string3\[strlen(string1)+strlen(string2)\]='\\0';

    cout<<"字符串连接结果为："<<endl;

    cout<<string3<<endl;

    delete \[\] string1;

    delete \[\] string2;

    delete \[\] string3;

    return 0;

}
```
    结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/1-3.png) 这里给出一个使用cstring头文件进行字符串的连接实例： 代码：使用string 声明字符串  + = 是重载的进行字符串连接操作的函数
```
#include<iostream>
using namespace std;

int main()
{
    string string1,string2,string3;
    cout<<"输入两个字符串二者之间用空格分隔:"<<endl;
    cin>>string1>>string2;
    cout<<"前一个字符串合成后一个字符串:"<<endl;
    string3 = string1+string2;
    cout<<string3<<endl;
    return 0;
}
```
  结果： ![](http://47.100.4.8/wp-content/uploads/2018/05/2-3.png)