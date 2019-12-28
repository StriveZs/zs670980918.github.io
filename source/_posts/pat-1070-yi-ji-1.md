---
title: Pat_1070（乙级）
url: 1764.html
id: 1764
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:02:15
tags:
---

1070 结绳 （25 分)  [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805264706813952)

给定一段一段的绳子，你需要把它们串成一条绳。每次串连的时候，是把两段绳子对折，再如下图所示套接在一起。这样得到的绳子又被当成是另一段绳子，可以再次对折去跟另一段绳子串连。每次串连后，原来两段绳子的长度就会减半。 ![rope.jpg](https://images.ptausercontent.com/46293e57-aa0e-414b-b5c3-7c4b2d5201e2.jpg) 给定 N 段绳子的长度，你需要找出它们能串成的绳子的最大长度。

### 输入格式：

每个输入包含 1 个测试用例。每个测试用例第 1 行给出正整数 N (2≤N≤10​4​​)；第 2 行给出 N 个正整数，即原始绳段的长度，数字间以空格分隔。所有整数都不超过10​4​​。

### 输出格式：

在一行中输出能够串成的绳子的最大长度。结果向下取整，即取为不超过最大长度的最近整数。

### 输入样例：

    8
    10 15 12 3 4 13 1 15
    

### 输出样例：

    14

代码：

#include<iostream>
#include<algorithm>
#include<cmath>
/*
分析：因为所有长度都要串在一起，每次都等于(旧的绳子长度+新的绳子长度)/2，所以越是早加入绳子长
度中的段，越要对折的次数多，所以既然希望绳子长度是最长的，就必须让长的段对折次数尽可能的短。所以将所
有段从小到大排序，然后从头到尾从小到大分别将每一段依次加入结绳的绳子中，最后得到的结果才会是最长的结果
*/
using namespace std;

int main(){
    int num,index=2,maxLen = 0;
    cin>>num;
    float len\[num\];
    for(int i=0;i<num;i++){
        cin>>len\[i\];
    }
    sort(len,len+num);
    maxLen = floor((len\[0\] + len\[1\])/2);
    while(index < num){
        maxLen = floor((maxLen + len\[index++\])/2);
    }
    cout<<maxLen<<endl;
    return 0;
}