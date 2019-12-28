---
title: Pat_1029（乙级）
url: 1678.html
id: 1678
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 11:41:36
tags:
---

1029 旧键盘 （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805292322111488)

旧键盘上坏了几个键，于是在敲一段文字的时候，对应的字符就不会出现。现在给出应该输入的一段文字、以及实际被输入的文字，请你列出肯定坏掉的那些键。

### 输入格式：

输入在 2 行中分别给出应该输入的文字、以及实际被输入的文字。每段文字是不超过 80 个字符的串，由字母 A-Z（包括大、小写）、数字 0-9、以及下划线 `_`（代表空格）组成。题目保证 2 个字符串均非空。

### 输出格式：

按照发现顺序，在一行中输出坏掉的键。其中英文字母只输出大写，每个坏键只输出一次。题目保证至少有 1 个坏键。

### 输入样例：

    7_This_is_a_test
    _hs_s_a_es
    

### 输出样例：

    7TI

代码：

#include<iostream>
#include<string.h>
#include<algorithm>
#include<vector>

using namespace std;

int main(){
    int index = 0,i=0;
    string s1,s2;
    vector<char> result;
    vector<char>::iterator pos;
    cin>>s1>>s2;
    transform(s1.begin(),s1.end(),s1.begin(),::toupper);
    transform(s2.begin(),s2.end(),s2.begin(),::toupper);
    while(i!=s2.length()){
        if(s1\[index\] != s2\[i\]){
            pos = find(result.begin(),result.end(),s1\[index\]);
            if(pos == result.end()){
                result.push_back(s1\[index\]);
            }
            index++;
        }
        else{
            i++;
            index++;
        }
    }
    if(index != (s1.length()-1)){
        for(int i=index;index<s1.length();index++){
            pos = find(result.begin(),result.end(),s1\[index\]);
            if(pos == result.end()){
                result.push_back(s1\[index\]);
            }
        }
    }
    for(pos=result.begin();pos!=result.end();pos++){
        cout<<*pos;
    }
    cout<<endl;
    return 0;
}