---
title: Pat_1011（乙级）
url: 1641.html
id: 1641
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 23:01:59
tags:
  - pat
---

1011 A+B 和 C （15 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805312417021952

给定区间 \[−2​31​​,2​31​​\] 内的 3 个整数 A、B 和 C，请判断 A+B 是否大于 C。

### 输入格式：

输入第 1 行给出正整数 T (≤10)，是测试用例的个数。随后给出 T 组测试用例，每组占一行，顺序给出 A、B 和 C。整数间以空格分隔。

### 输出格式：

对每组测试用例，在一行中输出 `Case #X: true` 如果 A+B>C，否则输出 `Case #X: false`，其中 `X` 是测试用例的编号（从 1 开始）。

### 输入样例：

    4
    1 2 3
    2 3 4
    2147483647 0 2147483646
    0 -2147483648 -2147483647
    

### 输出样例：

    Case #1: false
    Case #2: true
    Case #3: true
    Case #4: false

代码：
```
#include<iostream>
#include<deque>
#include<string.h>

using namespace std;

struct cunchu{
    long int qwe1;
    long int qwe2;
    long int qwe3;
};

int main(){
    deque<cunchu> qu;
    deque<cunchu>::iterator pos;
    int num,tempA,tempB,tempC,sum,flag;
    cin>>num;
    sum = num;
    while(num>0){
        cunchu q1;
        num--;
        flag = 0;
        cin>>tempA>>tempB>>tempC;
        q1.qwe1 = tempA;
        q1.qwe2 = tempB;
        q1.qwe3 = tempC;
        qu.push_back(q1);
    }
    num = sum;
    for(pos=qu.begin();pos!=qu.end();pos++){
        num--;
        if((\*pos).qwe1+(\*pos).qwe2>(*pos).qwe3){
            cout<<"Case #"<<sum-num<<": true"<<endl;
        }
        else{
           cout<<"Case #"<<sum-num<<": false"<<endl;
        }
    }
    return 0;
}
```