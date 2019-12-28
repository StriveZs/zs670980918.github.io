---
title: Pat_1057（乙级）
url: 1737.html
id: 1737
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-18 10:43:28
tags:
---

1057 数零壹 （20 分) [原文地址](https://pintia.cn/problem-sets/994805260223102976/problems/994805270914383872)

给定一串长度不超过 10​5​​ 的字符串，本题要求你将其中所有英文字母的序号（字母 a-z 对应序号 1-26，不分大小写）相加，得到整数 N，然后再分析一下 N 的二进制表示中有多少 0、多少 1。例如给定字符串 `PAT (Basic)`，其字母序号之和为：16+1+20+2+1+19+9+3=71，而 71 的二进制是 1000111，即有 3 个 0、4 个 1。

### 输入格式：

输入在一行中给出长度不超过 10​5​​、以回车结束的字符串。

### 输出格式：

在一行中先后输出 0 的个数和 1 的个数，其间以空格分隔。

### 输入样例：

    PAT (Basic)
    

### 输出样例：

    3 4

代码：

#include<iostream>
#include<map>
#include<string.h>
#include<algorithm>

using namespace std;

map<char,int> dir;
//计算二进制
string IntToBinary(int t){
    string s1="";
    while(t > 0){
        int temp,temp1;
        temp = t % 2;
        s1 += (temp + '0');
        t = t / 2;
    }
    reverse(s1.begin(),s1.end());
    return s1;
}

int main(){
    dir\['A'\] = 1;dir\['B'\] = 2;dir\['C'\] = 3;dir\['D'\] = 4;dir\['E'\] = 5;dir\['F'\] = 6;dir\['G'\] = 7;dir\['H'\] = 8;dir\['I'\] = 9;dir\['J'\] = 10;dir\['K'\] = 11;dir\['L'\] = 12;
    dir\['M'\] = 13;dir\['N'\] = 14;dir\['O'\] = 15;dir\['P'\] = 16;dir\['Q'\] = 17;dir\['R'\] = 18;dir\['S'\] = 19;dir\['T'\] = 20;dir\['U'\] = 21;dir\['V'\] = 22;dir\['W'\] = 23;
    dir\['X'\] = 24;dir\['Y'\] = 25;dir\['Z'\] = 26;
    string s1;
    getline(cin,s1);
    transform(s1.begin(),s1.end(),s1.begin(),::toupper);
    //计算总和
    int sum = 0;
    for(int i=0;i<s1.length();i++){
        if(s1\[i\]>='A' && s1\[i\]<='Z'){
            //cout<<dir\[s1\[i\]\]<<endl;
            sum += dir\[s1\[i\]\];
        }
    }
    string binary = IntToBinary(sum);
    //cout<<sum<<endl;
    cout<<count(binary.begin(),binary.end(),'0')<<" "<<count(binary.begin(),binary.end(),'1')<<endl;
    return 0;
}