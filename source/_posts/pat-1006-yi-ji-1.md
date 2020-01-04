---
title: Pat_1006（乙级）
url: 1631.html
id: 1631
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 22:55:34
tags:
  - pat
---

1006 换个格式输出整数 （15 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805318855278592

让我们用字母 `B` 来表示“百”、字母 `S` 表示“十”，用 `12...n` 来表示不为零的个位数字 `n`（<10），换个格式来输出任一个不超过 3 位的正整数。例如 `234` 应该被输出为 `BBSSS1234`，因为它有 2 个“百”、3 个“十”、以及个位的 4。

### 输入格式：

每个测试输入包含 1 个测试用例，给出正整数 n（<1000）。

### 输出格式：

每个测试用例的输出占一行，用规定的格式输出 n。

### 输入样例 1：

    234
    

### 输出样例 1：

    BBSSS1234
    

### 输入样例 2：

    23
    

### 输出样例 2：

    SS123

代码：
```
#include<iostream>
#include<string.h>

using namespace std;

int main(){
    string num;
    int temp,temp1,temp2;
    cin>>num;
    if(num.length()==1){
       temp = num\[0\] - '0';
       for(int i=1;i<=temp;i++){
            cout<<i;
       }
       cout<<endl;
    }
    else if(num.length()==2){
        temp = num\[0\] - '0';
        temp1 = num\[1\] - '0';
        for(int i=1;i<=temp;i++){
            cout<<"S";
        }
        for(int i=1;i<=temp1;i++){
            cout<<i;
        }
        cout<<endl;
    }
    else{
        temp = num\[0\] - '0';
        temp1 = num\[1\] - '0';
        temp2 = num\[2\] - '0';
        for(int i=1;i<=temp;i++){
            cout<<"B";
        }
        for(int i=1;i<=temp1;i++){
            cout<<"S";
        }
        for(int i=1;i<=temp2;i++){
            cout<<i;
        }
        cout<<endl;
    }
    return 0;
}
```