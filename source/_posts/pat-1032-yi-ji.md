---
title: Pat_1032（乙级）
url: 1684.html
id: 1684
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 11:46:39
tags:
---

1032 挖掘机技术哪家强 （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805289432236032)

为了用事实说明挖掘机技术到底哪家强，PAT 组织了一场挖掘机技能大赛。现请你根据比赛结果统计出技术最强的那个学校。

### 输入格式：

输入在第 1 行给出不超过 10​5​​ 的正整数 N，即参赛人数。随后 N 行，每行给出一位参赛者的信息和成绩，包括其所代表的学校的编号（从 1 开始连续编号）、及其比赛成绩（百分制），中间以空格分隔。

### 输出格式：

在一行中给出总得分最高的学校的编号、及其总分，中间以空格分隔。题目保证答案唯一，没有并列。

### 输入样例：

    6
    3 65
    2 80
    1 100
    2 70
    3 40
    3 0
    

### 输出样例：

    2 150

代码：

#include<iostream>
#include<map>
#include<algorithm>

using namespace std;

int main(){
    map<int,int> list1;
    map<int,int>::iterator pos;
    int num,temp,temp1;
    cin>>num;
    for(int i=0;i<num;i++){
        cin>>temp>>temp1;
        if(list1.count(temp) != 0){
            list1\[temp\] += temp1;
        }
        else{
            list1\[temp\] = temp1;
        }
    }
    int index,maxnum=0;
    for(pos=list1.begin();pos!=list1.end();pos++){
        if(pos->second > maxnum){
            index = pos->first;
            maxnum = pos->second;
        }
    }
    cout<<index<<" "<<list1\[index\]<<endl;
    return 0;
}