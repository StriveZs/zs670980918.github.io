---
title: Pat_1008（乙级）
url: 1635.html
id: 1635
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-11 22:58:10
tags:
---

1008 数组元素循环右移问题 （20 分） 地址：https://pintia.cn/problem-sets/994805260223102976/problems/994805316250615808

一个数组A中存有N（>0）个整数，在不允许使用另外数组的前提下，将每个整数循环向右移M（≥0）个位置，即将A中的数据由（A​0​​A​1​​⋯A​N−1​​）变换为（A​N−M​​⋯A​N−1​​A​0​​A​1​​⋯A​N−M−1​​）（最后M个数循环移至最前面的M个位置）。如果需要考虑程序移动数据的次数尽量少，要如何设计移动的方法？

### 输入格式:

每个输入包含一个测试用例，第1行输入N（1≤N≤100）和M（≥0）；第2行输入N个整数，之间用空格分隔。

### 输出格式:

在一行中输出循环右移M位以后的整数序列，之间用空格分隔，序列结尾不能有多余空格。

### 输入样例:

    6 2
    1 2 3 4 5 6
    

### 输出样例:

    5 6 1 2 3 4

代码：

#include<iostream>
#include<deque>

using namespace std;

int main(){
    deque<int> Queue;
    deque<int>::iterator pos;
    int num,moves,temp,t;
    cin>>num;
    cin>>moves;
    t = num;
    while(t>0){
        cin>>temp;
        Queue.push_back(temp);
        t--;
    }
    while(moves>0){
        temp = Queue.back();
        Queue.pop_back();
        Queue.push_front(temp);
        moves--;
    }
    for(pos = Queue.begin();pos!=Queue.end()-1;pos++)
        cout<<*pos<<" ";
    pos = Queue.end()-1;
    cout<<*pos<<endl;
    return 0;
}