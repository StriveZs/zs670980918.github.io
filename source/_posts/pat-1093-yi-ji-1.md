---
title: Pat_1093（乙级）
url: 1810.html
id: 1810
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 11:35:13
tags:
---

1093 字符串A+B （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/1071785884776722432)

给定两个字符串 A 和 B，本题要求你输出 A+B，即两个字符串的并集。要求先输出 A，再输出 B，但**重复的字符必须被剔除**。

### 输入格式：

输入在两行中分别给出 A 和 B，均为长度不超过 10​6​​的、由可见 ASCII 字符 (即码值为32~126)和空格组成的、由回车标识结束的非空字符串。

### 输出格式：

在一行中输出题面要求的 A 和 B 的和。

### 输入样例：

    This is a sample test
    to show you_How it works
    

### 输出样例：

    This ampletowyu_Hrk

代码：

#include<iostream>
#include<string.h>
#include<vector>
#include<algorithm>

using namespace std;

int main(){
    string s1,s2;
    getline(cin,s1);
    getline(cin,s2);
    vector<char> dir;
    for(int i=0;i<s1.length();i++){
        if(find(dir.begin(),dir.end(),s1\[i\]) == dir.end()){
            cout<<s1\[i\];
            dir.push_back(s1\[i\]);
        }
    }
    for(int i=0;i<s2.length();i++){
        if(find(dir.begin(),dir.end(),s2\[i\]) == dir.end()){
            cout<<s2\[i\];
            dir.push_back(s2\[i\]);
        }
    }
    cout<<endl;
    return 0;
}