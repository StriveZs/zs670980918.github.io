---
title: Pat_1047（乙级）
url: 1717.html
id: 1717
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 18:27:21
tags:
---

1047 编程团体赛 （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805277163896832)

编程团体赛的规则为：每个参赛队由若干队员组成；所有队员独立比赛；参赛队的成绩为所有队员的成绩和；成绩最高的队获胜。 现给定所有队员的比赛成绩，请你编写程序找出冠军队。

### 输入格式：

输入第一行给出一个正整数 N（≤10​4​​），即所有参赛队员总数。随后 N 行，每行给出一位队员的成绩，格式为：`队伍编号-队员编号 成绩`，其中`队伍编号`为 1 到 1000 的正整数，`队员编号`为 1 到 10 的正整数，`成绩`为 0 到 100 的整数。

### 输出格式：

在一行中输出冠军队的编号和总成绩，其间以一个空格分隔。注意：题目保证冠军队是唯一的。

### 输入样例：

    6
    3-10 99
    11-5 87
    102-1 0
    102-3 100
    11-9 89
    3-2 61
    

### 输出样例：

    11 176

代码：

#include<iostream>
#include<cstdio>
#include<map>

using namespace std;

int main(){
    map<int,int> dir;
    int num,t1,t2,t3,index=0;
    cin>>num;
    for(int i=0;i<num;i++){
        scanf("%d-%d %d",&t1,&t2,&t3);
        if(dir.count(t1) == 0){
            dir\[t1\] = t3;
        }
        else{
            dir\[t1\] += t3;
        }
        if(dir\[t1\] > dir\[index\]){
            index = t1;
        }
    }
    cout<<index<<" "<<dir\[index\]<<endl;
    return 0;
}