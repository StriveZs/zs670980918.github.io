---
title: Pat_1001（甲级）
url: 1816.html
id: 1816
categories:
  - PAT
  - 乙级
  - 文章页
date: 2019-03-25 23:17:04
tags:
---

1001 A+B Format （20 分) [原文地址](https://pintia.cn/problem-sets/994805342720868352/problems/994805528788582400)

Calculate a+b and output the sum in standard format -- that is, the digits must be separated into groups of three by commas (unless there are less than four digits).

### Input Specification:

Each input file contains one test case. Each case contains a pair of integers a and b where −10​6​​≤a,b≤10​6​​. The numbers are separated by a space.

### Output Specification:

For each test case, you should output the sum of a and b in one line. The sum must be written in the standard format.

### Sample Input:

    -1000000 9
    

### Sample Output:

    -999,991

代码：（这里自己写过一个可以使所有数据进行相加减的大数运算 但是会发生time out 因此这个参考了网上大佬写的，基本上能看懂所以在这里就贴大佬的了）

#include<iostream>
#include<cstdio>
#include<cmath>
#include<cstring>
using namespace std;
int main(){
    int a,b;
    cin>>a>>b;
    int c=a+b;
    if(c<0) cout<<'-';
    c=abs(c);
    char s\[20\];
    sprintf(s,"%d",c);
    int len=strlen(s);
    //if(len<=3) {cout<<s;return 0;}
    int m=len/3,n=len%3,start=0;
    //cout<<"m="<<m<<' '<<"n="<<n<<endl;
    if(n==0) {cout<<s\[0\]<<s\[1\]<<s\[2\];start=3;m--;}
    else if(n==1) {cout<<s\[0\];start=1;}
    else if(n==2) {cout<<s\[0\]<<s\[1\];start=2;}
    while(m!=0){
        cout<<',';
        cout<<s\[start\]<<s\[start+1\]<<s\[start+2\];
        start+=3;
        m--;
    }
    return 0;
}