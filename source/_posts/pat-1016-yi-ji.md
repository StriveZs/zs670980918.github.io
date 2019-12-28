---
title: Pat_1016（乙级）
url: 1651.html
id: 1651
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 23:15:26
tags:
---

1016 部分A+B （15 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805306310115328

正整数 A 的“D​A​​（为 1 位整数）部分”定义为由 A 中所有 D​A​​ 组成的新整数 P​A​​。例如：给定 A=3862767，D​A​​=6，则 A 的“6 部分”P​A​​ 是 66，因为 A 中有 2 个 6。 现给定 A、D​A​​、B、D​B​​，请编写程序计算 P​A​​+P​B​​。

### 输入格式：

输入在一行中依次给出 A、D​A​​、B、D​B​​，中间以空格分隔，其中 0<A,B<10​10​​。

### 输出格式：

在一行中输出 P​A​​+P​B​​ 的值。

### 输入样例 1：

    3862767 6 13530293 3
    

### 输出样例 1：

    399
    

### 输入样例 2：

    3862767 1 13530293 8
    

### 输出样例 2：

    0

代码：

#include<iostream>
#include<string.h>

using namespace std;

int charToint(char t,int num){
    if(num == 0){
        return 0;
    }
    else{
        int result=0,temp=0,t1;
        temp = t - '0';
        result = temp;
        num--;
        while(num>0){
            result = result*10 + temp;
            num--;
        }
        return result;
    }
}
int main(){
    string A,Da,B,Db;
    int Pa,Pb,numA=0,numB=0;
    cin>>A>>Da>>B>>Db;
    for(int i=0;i<A.length();i++){
        if(A\[i\] == Da\[0\]){
            numA++;
        }
    }
    for(int i=0;i<B.length();i++){
        if(B\[i\] == Db\[0\]){
            numB++;
        }
    }
    //cout<<"test"<<endl;
    Pa = charToint(Da\[0\],numA);
    Pb = charToint(Db\[0\],numB);
    cout<<Pa + Pb<<endl;
    return 0;
}