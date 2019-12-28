---
title: Pat_1087（乙级）
url: 1798.html
id: 1798
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:28:58
tags:
---

1087 有多少不同的值 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/1038429191091781632)

当自然数 n 依次取 1、2、3、……、N 时，算式 ⌊n/2⌋+⌊n/3⌋+⌊n/5⌋ 有多少个不同的值？（注：⌊x⌋ 为取整函数，表示不超过 x 的最大自然数，即 x 的整数部分。）

### 输入格式：

输入给出一个正整数 N（2≤N≤10​4​​）。

### 输出格式：

在一行中输出题面中算式取到的不同值的个数。

### 输入样例：

    2017
    

### 输出样例：

    1480

代码：

#include<iostream>
#include<vector>
#include<algorithm>
#include<math.h>

using namespace std;

int main(){
    vector<int> dir;
    int n;
    int num = 0;
    cin>>n;
    for(int i=1;i<=n;i++){
        int sum = floor(float(i/2)) + floor(float(i/3)) + floor(float(i/5));
        if(count(dir.begin(),dir.end(),sum) == 0){
            dir.push_back(sum);
            num++;
        }
    }
    cout<<num<<endl;
    return 0;
}