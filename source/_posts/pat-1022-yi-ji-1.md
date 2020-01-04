---
title: Pat_1022（乙级）
url: 1663.html
id: 1663
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 11:32:21
tags:
  - pat
---

1022 D进制的A+B （20 分）[原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805299301433344)

输入两个非负 10 进制整数 A 和 B (≤2​30​​−1)，输出 A+B 的 D (1<D≤10)进制数。

### 输入格式：

输入在一行中依次给出 3 个整数 A、B 和 D。

### 输出格式：

输出 A+B 的 D 进制数。

### 输入样例：

    123 456 8
    

### 输出样例：

    1103

代码：
```
#include<iostream>
#include<stack>

using namespace std;


int main(){
    stack<int> qwe;
    long long A,B,C,D;
    cin>>A>>B>>D;
    C = A + B;
    if(C==0){
        cout<<"0"<<endl;
    }
    else{
        while(C!=0){
           int t = C % D;
           qwe.push(t);
           C = C / D;
        }
        while(!qwe.empty()){
            cout<<qwe.top();
            qwe.pop();
        }
    }
    return 0;
}
```