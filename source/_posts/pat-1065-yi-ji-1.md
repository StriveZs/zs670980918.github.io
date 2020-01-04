---
title: Pat_1065（乙级）
url: 1753.html
id: 1753
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:52:53
tags:
  - pat
---

1065 单身狗 （25 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805266942377984)

“单身狗”是中文对于单身人士的一种爱称。本题请你从上万人的大型派对中找出落单的客人，以便给予特殊关爱。

### 输入格式：

输入第一行给出一个正整数 N（≤ 50 000），是已知夫妻/伴侣的对数；随后 N 行，每行给出一对夫妻/伴侣——为方便起见，每人对应一个 ID 号，为 5 位数字（从 00000 到 99999），ID 间以空格分隔；之后给出一个正整数 M（≤ 10 000），为参加派对的总人数；随后一行给出这 M 位客人的 ID，以空格分隔。题目保证无人重婚或脚踩两条船。

### 输出格式：

首先第一行输出落单客人的总人数；随后第二行按 ID 递增顺序列出落单的客人。ID 间用 1 个空格分隔，行的首尾不得有多余空格。

### 输入样例：

    3
    11111 22222
    33333 44444
    55555 66666
    7
    55555 44444 10000 88888 22222 11111 23333
    

### 输出样例：

    5
    10000 23333 44444 55555 88888

代码：
```
#include<iostream>
#include<algorithm>
#include<map>
#include<cstdio>

using namespace std;

//统计如果小于10000则需要补零的个数
int countZero(int t){
    if(t - 10 < 0){
        return 4;
    }
    else if(t - 100 < 0){
        return 3;
    }
    else if(t - 1000 < 0){
        return 2;
    }
    else{
        return 1;
    }
}

int main(){
    map<int,int> dir;
    long int num1,num2,iter=0;
    scanf("%ld",&num1);
    for(long int i=0;i<num1;i++){
        int t1,t2;
        scanf("%d",&t1);
        scanf("%d",&t2);
        dir\[t1\] = t2;
        dir\[t2\] = t1;
    }
    scanf("%ld",&num2);
    int list1\[num2\];
    int loser\[num2\];
    for(long int i=0;i<num2;i++){
        int temp;
        scanf("%d",&temp);
        list1\[i\] = temp;
    }
    for(long int i=0;i<num2;i++){
        if(count(list1,list1+num2,dir\[list1\[i\]\]) == 0){
            loser\[iter\] = list1\[i\];
            iter++;
        }
    }
    sort(loser,loser+iter);
    cout<<iter<<endl;
    int m=0;
    for(long int i=0;i<iter;i++){
        if(i != 0){
            cout<<" ";
        }
        if(loser\[i\] < 10000){
            int q = countZero(loser\[i\]);
            for(int i=0;i<q;i++){
                cout<<0;
            }
        }
        cout<<loser\[i\];
    }
    return 0;
}
```