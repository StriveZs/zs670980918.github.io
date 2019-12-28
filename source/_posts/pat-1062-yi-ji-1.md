---
title: Pat_1062（乙级）
url: 1747.html
id: 1747
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:49:56
tags:
---

1062 最简分数 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805268334886912)

一个分数一般写成两个整数相除的形式：N/M，其中 M 不为0。最简分数是指分子和分母没有公约数的分数表示形式。 现给定两个不相等的正分数 N​1​​/M​1​​ 和 N​2​​/M​2​​，要求你按从小到大的顺序列出它们之间分母为 K 的最简分数。

### 输入格式：

输入在一行中按 N/M 的格式给出两个正分数，随后是一个正整数分母 K，其间以空格分隔。题目保证给出的所有整数都不超过 1000。

### 输出格式：

在一行中按 N/M 的格式列出两个给定分数之间分母为 K 的所有最简分数，按从小到大的顺序，其间以 1 个空格分隔。行首尾不得有多余空格。题目保证至少有 1 个输出。

### 输入样例：

    7/18 13/20 12
    

### 输出样例：

    5/12 7/12

代码：

#include<iostream>
#include<cstdio>

using namespace std;
//辗转相除 求公因子
int judge(int k,int t){
    int c = 0;
    while(k != 0){
        c = t%k;
        t = k;
        k = c;
    }
    return t;
}

int main(){
    int N1,M1,N2,M2,K,temp,t1,t2;
    scanf("%d/%d %d/%d %d",&N1,&M1,&N2,&M2,&K);
    temp = M1 * M2;
    t1 = N1 * M2;
    t2 = N2 * M1;
    if(t1 > t2){
        int t = N1;
        N1 = N2;
        N2 = t;
        t = M1;
        M1 = M2;
        M2 = t;
    }
    int list1\[1000\]={0};
    int num = 0;
    for(int i=0;;i++){
        if(i\*M1 > N1\*K && i\*M2 < K\*N2){
            if(judge(i,K) == 1){
                list1\[num\] = i;
                num++;
            }
        }
        else if(i\*M2 > K\*N2){
            break;
        }
    }
    for(int i=0;i<num;i++){
        if(i == 0){
            cout<<list1\[i\]<<"/"<<K;
        }
        else{
            cout<<" "<<list1\[i\]<<"/"<<K;
        }
    }
    cout<<endl;
    return 0;
}