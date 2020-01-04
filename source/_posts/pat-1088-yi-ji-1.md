---
title: Pat_1088（乙级）
url: 1800.html
id: 1800
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:30:11
tags:
  - pat
---

1088 三人行 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/1038429286185074688)

子曰：“三人行，必有我师焉。择其善者而从之，其不善者而改之。” 本题给定甲、乙、丙三个人的能力值关系为：甲的能力值确定是 2 位正整数；把甲的能力值的 2 个数字调换位置就是乙的能力值；甲乙两人能力差是丙的能力值的 X 倍；乙的能力值是丙的 Y 倍。请你指出谁比你强应“从之”，谁比你弱应“改之”。

### 输入格式：

输入在一行中给出三个数，依次为：M（你自己的能力值）、X 和 Y。三个数字均为不超过 1000 的正整数。

### 输出格式：

在一行中首先输出甲的能力值，随后依次输出甲、乙、丙三人与你的关系：如果其比你强，输出 `Cong`；平等则输出 `Ping`；比你弱则输出 `Gai`。其间以 1 个空格分隔，行首尾不得有多余空格。 注意：如果解不唯一，则以甲的最大解为准进行判断；如果解不存在，则输出 `No Solution`。

### 输入样例 1：

    48 3 7
    

### 输出样例 1：

    48 Ping Cong Gai
    

### 输入样例 2：

    48 11 6
    

### 输出样例 2：

    No Solution

代码：
```
#include<iostream>
#include<cmath>

using namespace std;

void judge(double a,int b){
    if(a > b){
        cout<<"Cong";
    }
    else if(a == b){
        cout<<"Ping";
    }
    else{
        cout<<"Gai";
    }
}

int main(){
    bool flag = true;
    int me,X,Y;
    cin>>me>>X>>Y;
    for(int i=99;i>=10;i--){ // 则以甲的最大解为准进行判断
        int yi = i/10 + (i%10)*10;
        if(abs(i-yi)\*Y == yi\*X){
            double temp = (abs(i-yi)*1.0)/X;
            cout<<i<<" ";
            //cout<<i<<" "<<yi<<" "<<yi*X<<endl;
            judge(i,me);
            cout<<" ";
            judge(yi,me);
            cout<<" ";
            judge(temp,me);
            cout<<endl;
            flag = false;
            break;
        }
    }
    if(flag){
        cout<<"No Solution"<<endl;
    }
    return 0;
}
```