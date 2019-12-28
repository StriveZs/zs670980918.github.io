---
title: Pat_1060（乙级）
url: 1743.html
id: 1743
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:47:27
tags:
---

1060 爱丁顿数 （25 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805269312159744) 英国天文学家爱丁顿很喜欢骑车。据说他为了炫耀自己的骑车功力，还定义了一个“爱丁顿数” E ，即满足有 E 天骑车超过 E 英里的最大整数 E。据说爱丁顿自己的 E 等于87。 现给定某人 N 天的骑车距离，请你算出对应的爱丁顿数 E（≤N）。

### 输入格式：

输入第一行给出一个正整数 N (≤10​5​​)，即连续骑车的天数；第二行给出 N 个非负整数，代表每天的骑车距离。

### 输出格式：

在一行中给出 N 天的爱丁顿数。

### 输入样例：

    10
    6 7 6 9 3 10 8 2 7 8
    

### 输出样例：

    6

代码：

#include<iostream>
#include<algorithm>
#include<math.h>
#include<cstdio>

using namespace std;

bool cmp(int a,int b){
    return a > b;
}

int main(){
    int N,sum=0,aver=0;
    scanf("%d",&N);
    int list1\[N\];
    for(int i=0;i<N;i++){
        scanf("%d",&list1\[i\]);
        sum += list1\[i\];
    }
    aver = 1;
    sort(list1,list1+N,cmp);
    //对排序的结果从大到小访问 如果值小于等于 计数值则结束
    for(int i=0;i<N;i++){
        if(list1\[i\] <= aver){
            break;
        }
        aver++;;
    }
    cout<<--aver<<endl;
    return 0;;
}