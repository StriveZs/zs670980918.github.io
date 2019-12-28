---
title: Pat_1030（乙级）
url: 1680.html
id: 1680
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 11:42:44
tags:
---

1030 完美数列 （25 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805291311284224)

给定一个正整数数列，和正整数 p，设这个数列中的最大值是 M，最小值是 m，如果 M≤mp，则称这个数列是完美数列。 现在给定参数 p 和一些正整数，请你从中选择尽可能多的数构成一个完美数列。

### 输入格式：

输入第一行给出两个正整数 N 和 p，其中 N（≤10​5​​）是输入的正整数的个数，p（≤10​9​​）是给定的参数。第二行给出 N 个正整数，每个数不超过 10​9​​。

### 输出格式：

在一行中输出最多可以选择多少个数可以用它们组成一个完美数列。

### 输入样例：

    10 8
    2 3 20 4 5 1 6 7 8 9
    

### 输出样例：

    8

代码：

#include<iostream>
#include<algorithm>

using namespace std;

bool cmp(int a,int b){
    return a<b;
}
int main(){
    long int num,q;
    cin>>num>>q;
    long int li\[num\];
    for(int i=0;i<num;i++){
        cin>>li\[i\];
    }
    sort(li,li+num,cmp);
    int temp,maxnum = 0;
    for(int i=0;i+maxnum<=num;i++){
        for(temp=i+maxnum;temp<num;temp++){
            long int mq = li\[i\] * q;
            if(li\[temp\]<=mq){
                maxnum = temp+1-i;
            }
            else{
                break;
            }
        }
    }
    cout<<maxnum<<endl;
    return 0;
}