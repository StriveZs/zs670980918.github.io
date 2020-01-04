---
title: Pat_1061（乙级）
url: 1745.html
id: 1745
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:48:50
tags:
  - pat
---

1061 判断题 （15 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805268817231872)

判断题的评判很简单，本题就要求你写个简单的程序帮助老师判题并统计学生们判断题的得分。

### 输入格式：

输入在第一行给出两个不超过 100 的正整数 N 和 M，分别是学生人数和判断题数量。第二行给出 M 个不超过 5 的正整数，是每道题的满分值。第三行给出每道题对应的正确答案，0 代表“非”，1 代表“是”。随后 N 行，每行给出一个学生的解答。数字间均以空格分隔。

### 输出格式：

按照输入的顺序输出每个学生的得分，每个分数占一行。

### 输入样例：

    3 6
    2 1 3 3 4 5
    0 0 1 0 1 1
    0 1 1 0 0 1
    1 0 1 0 1 0
    1 1 0 0 1 1
    

### 输出样例：

    13
    11
    12

代码：
```
#include<iostream>

using namespace std;

struct Answer{
    int fenzhi; //分值
    int answer; //答案
};

int main(){
    int N,M;
    cin>>N>>M;
    Answer ans\[M\];
    for(int i=0;i<M;i++){
        int temp;
        cin>>temp;
        ans\[i\].fenzhi = temp;
    }
    for(int i=0;i<M;i++){
        int temp;
        cin>>temp;
        ans\[i\].answer = temp;
    }
    int student\[N\]={0}; //学生分值计数
    for(int i=0;i<N;i++){
        for(int j=0;j<M;j++){
            int temp = 0;
            cin>>temp;
            if(ans\[j\].answer == temp){
                student\[i\] += ans\[j\].fenzhi;
            }
        }
    }
    for(int i=0;i<N;i++){
        cout<<student\[i\]<<endl;
    }
    return 0;
}
```