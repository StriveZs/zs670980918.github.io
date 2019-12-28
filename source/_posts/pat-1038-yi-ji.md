---
title: Pat_1038（乙级）
url: 1698.html
id: 1698
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 18:12:19
tags:
---

1038 统计同成绩学生 （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805284092887040)

本题要求读入 N 名学生的成绩，将获得某一给定分数的学生人数输出。

### 输入格式：

输入在第 1 行给出不超过 10​5​​ 的正整数 N，即学生总人数。随后一行给出 N 名学生的百分制整数成绩，中间以空格分隔。最后一行给出要查询的分数个数 K（不超过 N 的正整数），随后是 K 个分数，中间以空格分隔。

### 输出格式：

在一行中按查询顺序给出得分等于指定分数的学生人数，中间以空格分隔，但行末不得有多余空格。

### 输入样例：

    10
    60 75 90 55 75 99 82 90 75 50
    3 75 90 88
    

### 输出样例：

    3 2 0

代码：

#include<iostream>
#include<cstdio>

using namespace std;

int main(){
    int dir\[10000\]={0};
    int num,temp,m;
    scanf("%d",&num);
    for(int i=0;i<num;i++){
        scanf("%d",&temp);
        dir\[temp\]++;
    }
    scanf("%d",&m);
    for(int i=0;i<m;i++){
        scanf("%d",&temp);
        if(i == m-1){
            cout<<dir\[temp\]<<endl;
        }
        else{
            cout<<dir\[temp\]<<" ";
        }
    }
    return 0;
}