---
title: Pat_1064（乙级）
url: 1751.html
id: 1751
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:51:56
tags:
---

1064 朋友数 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805267416334336)

如果两个整数各位数字的和是一样的，则被称为是“朋友数”，而那个公共的和就是它们的“朋友证号”。例如 123 和 51 就是朋友数，因为 1+2+3 = 5+1 = 6，而 6 就是它们的朋友证号。给定一些整数，要求你统计一下它们中有多少个不同的朋友证号。

### 输入格式：

输入第一行给出正整数 N。随后一行给出 N 个正整数，数字间以空格分隔。题目保证所有数字小于 10​4​​。

### 输出格式：

首先第一行输出给定数字中不同的朋友证号的个数；随后一行按递增顺序输出这些朋友证号，数字间隔一个空格，且行末不得有多余空格。

### 输入样例：

    8
    123 899 51 998 27 33 36 12
    

### 输出样例：

    4
    3 6 9 26

代码：

#include<iostream>
#include<map>
#include<string.h>

using namespace std;

//将字符串转换为整数并求和
int strToNum(string s1){
    int sum = 0;
    for(int i=0;i<s1.length();i++){
        sum += (s1\[i\] - '0');
    }
    return sum;
}

int main(){
    int num,ls=0;
    cin>>num;
    map<int,int> dir;
    map<int,int>::iterator pos;
    for(int i=0;i<num;i++){
        string s1;
        cin>>s1;
        int temp = strToNum(s1);
        //cout<<temp<<" ";
        if(dir.count(temp) == 0){
            dir\[temp\] = 1;
            ls++;
        }
        else{
            dir\[temp\] += 1;
        }
    }
    //cout<<endl;
    cout<<ls<<endl;
    for(pos=dir.begin();pos!=dir.end();pos++){
        if(pos == dir.begin()){
            cout<<pos->first;
        }
        else{
            cout<<" "<<pos->first;
        }
    }
    cout<<endl;
    return 0;
}