---
title: Pat_1040（乙级）
url: 1702.html
id: 1702
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 18:15:25
tags:
  - pat
---

1040 有几个PAT （25 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805282389999616)

字符串 `APPAPT` 中包含了两个单词 `PAT`，其中第一个 `PAT` 是第 2 位(`P`)，第 4 位(`A`)，第 6 位(`T`)；第二个 `PAT` 是第 3 位(`P`)，第 4 位(`A`)，第 6 位(`T`)。 现给定字符串，问一共可以形成多少个 `PAT`？

### 输入格式：

输入只有一行，包含一个字符串，长度不超过10​5​​，只包含 `P`、`A`、`T` 三种字母。

### 输出格式：

在一行中输出给定字符串中包含多少个 `PAT`。由于结果可能比较大，只输出对 1000000007 取余数的结果。

### 输入样例：

    APPAPT
    

### 输出样例：

    2

代码：
```
#include<iostream>
#include<string.h>

using namespace std;

int main(){
    string s1;
    cin>>s1;
    long int sum=0,num1=0,num2=0;
    for(int i=s1.length()-1;i>=0;i--){
        if(s1\[i\] == 'T'){
            num2++;
        }
        else if(s1\[i\] == 'A'){
            num1 = num1+num2;
        }
        else if(s1\[i\] == 'P'){
            sum = num1 + sum;
        }
    }
    cout<<sum%1000000007<<endl;
    return 0;
}
```