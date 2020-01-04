---
title: Pat_1036（乙级）
url: 1694.html
id: 1694
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 18:05:36
tags:
  - pat
---

1036 跟奥巴马一起编程 （15 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805285812551680)

美国总统奥巴马不仅呼吁所有人都学习编程，甚至以身作则编写代码，成为美国历史上首位编写计算机代码的总统。2014 年底，为庆祝“计算机科学教育周”正式启动，奥巴马编写了很简单的计算机代码：在屏幕上画一个正方形。现在你也跟他一起画吧！

### 输入格式：

输入在一行中给出正方形边长 N（3≤N≤20）和组成正方形边的某种字符 C，间隔一个空格。

### 输出格式：

输出由给定字符 C 画出的正方形。但是注意到行间距比列间距大，所以为了让结果看上去更像正方形，我们输出的行数实际上是列数的 50%（四舍五入取整）。

### 输入样例：

    10 a
    

### 输出样例：

    aaaaaaaaaa
    a        a
    a        a
    a        a
    aaaaaaaaaa

代码：
```
#include<iostream>
#include<math.h>

using namespace std;

int main(){
    int num,lie,hang;
    char ch;
    cin>>num;
    cin>>ch;
    lie = round(float(num)/2)-2; //除了上下两行的行数
    hang = num - 2; //空格数
    for(int i=0;i<num;i++){
        if(i == num -1){
            cout<<ch<<endl;
        }
        else{
            cout<<ch;
        }
    }
    for(int i=0;i<lie;i++){
        cout<<ch;
        for(int j=0;j<hang;j++){
            cout<<" ";
        }
        cout<<ch<<endl;
    }
    for(int i=0;i<num;i++){
        if(i == num -1){
            cout<<ch<<endl;
        }
        else{
            cout<<ch;
        }
    }
    return 0;
}
```