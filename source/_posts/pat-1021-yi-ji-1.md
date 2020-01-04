---
title: Pat_1021（乙级）
url: 1661.html
id: 1661
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 11:30:21
tags:
  - pat
---

1021 个位数统计 （15 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805300404535296

给定一个 k 位整数 N=d​k−1​​10​k−1​​+⋯+d​1​​10​1​​+d​0​​ (0≤d​i​​≤9, i=0,⋯,k−1, d​k−1​​>0)，请编写程序统计每种不同的个位数字出现的次数。例如：给定 N=100311，则有 2 个 0，3 个 1，和 1 个 3。

### 输入格式：

每个输入包含 1 个测试用例，即一个不超过 1000 位的正整数 N。

### 输出格式：

对 N 中每一种不同的个位数字，以 `D:M` 的格式在一行中输出该位数字 `D` 及其在 N 中出现的次数 `M`。要求按 `D` 的升序输出。

### 输入样例：

    100311
    

### 输出样例：

    0:2
    1:3
    3:1

代码：
```
#include<iostream>
#include<string.h>
#include<algorithm>

using namespace std;

struct number{
    int num;
    int counts;
}qwe\[10\];
int main(){
    string sen;
    cin>>sen;
    for(int i=0;i<10;i++){
        qwe\[i\].num = i;
        qwe\[i\].counts = 0;
    }
    for(int i=0;i<sen.length();i++){
        switch(sen\[i\]){
            case '0':{
                qwe\[sen\[i\]-'0'\].counts++;
            };break;
            case '1':{
                qwe\[sen\[i\]-'0'\].counts++;
            };break;
            case '2':{
                qwe\[sen\[i\]-'0'\].counts++;
            };break;
            case '3':{
                qwe\[sen\[i\]-'0'\].counts++;
            };break;
            case '4':{
                qwe\[sen\[i\]-'0'\].counts++;
            };break;
            case '5':{
                qwe\[sen\[i\]-'0'\].counts++;
            };break;
            case '6':{
                qwe\[sen\[i\]-'0'\].counts++;
            };break;
            case '7':{
                qwe\[sen\[i\]-'0'\].counts++;
            };break;
            case '8':{
                qwe\[sen\[i\]-'0'\].counts++;
            };break;
            case '9':{
                qwe\[sen\[i\]-'0'\].counts++;
            };break;
        }
    }
    for(int i=0;i<10;i++){
        if(qwe\[i\].counts != 0){
            cout<<qwe\[i\].num<<":"<<qwe\[i\].counts<<endl;
        }
    }
    return 0;
}
```