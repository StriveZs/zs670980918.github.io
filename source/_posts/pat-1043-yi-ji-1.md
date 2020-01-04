---
title: Pat_1043（乙级）
url: 1708.html
id: 1708
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-12 18:18:08
tags:
  - pat
---

1043 输出PATest （20 分） [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805280074743808)

给定一个长度不超过 10​4​​ 的、仅由英文字母构成的字符串。请将字符重新调整顺序，按 `PATestPATest....` 这样的顺序输出，并忽略其它字符。当然，六种字符的个数不一定是一样多的，若某种字符已经输出完，则余下的字符仍按 PATest 的顺序打印，直到所有字符都被输出。

### 输入格式：

输入在一行中给出一个长度不超过 10​4​​ 的、仅由英文字母构成的非空字符串。

### 输出格式：

在一行中按题目要求输出排序后的字符串。题目保证输出非空。

### 输入样例：

    redlesPayBestPATTopTeePHPereatitAPPT
    

### 输出样例：

    PATestPATestPTetPTePePee

代码：
```
#include<iostream>
#include<string.h>

using namespace std;

int main(){
    string s1;
    cin>>s1;
    int num\_P=0,num\_A=0,num\_T=0,num\_e=0,num\_s=0,num\_t=0;
    for(int i=0;i<s1.length();i++){
        if(s1\[i\] == 'P'){
            num_P++;
        }
        else if(s1\[i\] == 'A'){
            num_A++;
        }
        else if(s1\[i\] == 'T'){
            num_T++;
        }
        else if(s1\[i\] == 'e'){
            num_e++;
        }
        else if(s1\[i\] == 's'){
            num_s++;
        }
        else if(s1\[i\] == 't'){
            num_t++;
        }
    }
    while(num\_P!=0 || num\_A!=0 || num\_T!=0 || num\_e!=0 || num\_s!=0 || num\_t!=0){
        if(num_P > 0){
            cout<<"P";
            num_P--;
        }
        if(num_A > 0){
            cout<<"A";
            num_A--;
        }
        if(num_T > 0){
            cout<<"T";
            num_T--;
        }
        if(num_e > 0){
            cout<<"e";
            num_e--;
        }
        if(num_s > 0){
            cout<<"s";
            num_s--;
        }
        if(num_t > 0){
            cout<<"t";
            num_t--;
        }
    }
    cout<<endl;
    return 0;
}
```